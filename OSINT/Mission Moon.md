>A mission, had planned to land on the moon. Can you find where it planned to land on the moon and the name of the lander and rover? Flag is latitude longitude upto one decimal place.
>
> - Note: Flag format - `n00bz{Lander_Rover_latitude_longitude} for eg - n00bz{Examplelander_Examplerover_12.3_45.6}`. Also note that flag is **case sensitive!**
> - Note: Due to a quite big range of answers, to narrow down your search, use the latitude and longitude provided from this site: `blog.jatan.space`
----------------------------
![mission_moon.webp](https://github.com/spencerja/n00bCTF_Writeup/blob/main/OSINT/Images/mission_moon.webp)
This presented image appears to be a 3D rendering of a moon landing plan. The first easy check to be done is a reverse image search in google, and see what articles are discussing this event. 
Very quickly I see an [article that uses the image](https://www.newscientist.com/article/2215704-indias-vikram-moon-lander-appears-to-have-crashed-on-the-moon/) discussing a failed landing for India's moon mission titled Chandrayaan 2. The lander for this mission appears to be called Vikram, and the rover called Pragyan. This info is part of the flag, but we still need to find the exact coordinates of the planned landing. 
With a mission name in mind, I visited the blog.jatan.space site mentioned, and searched for `Chandrayaan 2`. On [this page](https://blog.jatan.space/p/chandrayaan-2-landing-site-in-the-southern-highlands?utm_source=%2Fsearch%2Fvikram%2520chandrayaan-2&utm_medium=reader2) I learned the coordinates planned for the landing: 70.9S, 22.8E. 

Now we can construct and submit the flag as `n00bz{Vikram_Pragyan_70.9_22.8}`.
