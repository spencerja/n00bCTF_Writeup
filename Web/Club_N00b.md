>Can you get in the club? Author: 0xBlue
>
>[http://challs.n00bzunit3d.xyz:8080/](http://challs.n00bzunit3d.xyz:8080/)
-------------
Following the link:
![Pasted image 20230609180928.png](https://github.com/spencerja/n00bCTF_Writeup/blob/main/Web/Images/Pasted%20image%2020230609180928.png)
Only "radical" hackers are allowed, and we are not. Upon checking status, we see the button is not post/cookie data related, but instead redirects to an interesting url:
```
http://challs.n00bzunit3d.xyz:8080/check?secret_phrase=nope
```
We are not on the member list. But perhaps if we change the secret_phrase?
After a couple guesses, we successfully get in with `secret_phrase=radical`.
![Pasted image 20230609181218.png](https://github.com/spencerja/n00bCTF_Writeup/blob/main/Web/Images/Pasted%20image%2020230609181218.png)

`n00bz{see_you_in_the_club_acting_real_nice}`
