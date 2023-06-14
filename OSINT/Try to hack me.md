>My friend `brayannoob` gave me a ctf challenge and told me `Try to hack me`.
------------------------
A google search on brayannoob did not yield any interesting results, so I decided to switch search engines. Upon using Bing, a [github account](https://github.com/brayannoob) was among the first results, very interesting. The repositories within this github we see a n00bzCTF-2022 writeup. With relevance on our side, this is clearly related to the challenge. Exploring the newest repository, BrayanResearch, I uncovered user credentials from an older edit of the README.md file: 
```
<!-- ACCOUNT CREDENTIALS -->|
<!-- USERNAME - @brayanduarte.noob -->|
<!-- PASSWORD - Brayann00b@2023 -->
# THANK YOU :love:
```
Other edits also give light to potential usernames:
```
<!-- username : @brayan24 -->
```
and in the current readme:
```
<!-- username : brayan234 -->
```
We have potential usernames and a password, but which service these are for? It is not so clear.

This github repo supplies a demo, providing a link to replit.com. After searching for a little bit, we come across [this user.](https://replit.com/@brayanduartenoo). Using the provided password, I was able to log in and "hack" this account! However, after searching for quite some time, I was unable to find the flag. Reviewing the CTF discord channel, there is an announcement that breaching this account was unintended for the challenge. I suppose this little adventure may serve to emphasize how easy it might be to accidentally leak credentials on github or other services!

From the discord message we know the password login is irrelevant, time to think on the hints provided in the prompt again. Looking at the `Try to hack me` part, it makes me think of the popular web service TryHackMe. After looking through usernames we stumble upon a certain username from our list: [brayan234](https://tryhackme.com/p/brayan234). Looking at this account, it appears we didn't need to log in at all! The flag is presented right in the user info section.
`n00bz{y0u_p4ss3d_th3_ch4ll3ng3_c0ngr4tul4t10ns_7c48179d2b7547938409152641cf8e}`
