---
layout: post
title:  All steps I did when my iPhone died!
date: 2025-11-30 21:00:00
description: 
tags: phone Youtube Apple
categories: Lifestyle
thumbnail: assets/img/blog/30.jpg
---
I had an iPhone 11 for more than 4 years, which died!
I talked with my sister through WhatsApp video call, but suddenly after we finished, my phone turned off.
At first, I thought it was out of charge and plugged it in.
After 30 minutes, I tried to turn it on, but it did not work. I got concerned, but I thought it was a simple crash.

{% include figure_half.html path="assets/img/blog/31.webp" class="img-fluid rounded z-depth-1" width="40%" caption="" %}
 
I searched a bit and found that a force restart can solve many challenges. For a force restart, I followed this link: [Apple website](https://support.apple.com/en-ca/116940?iphone-authentication-type=iphone-with-face-id). Simply, a hard restart on iPhone needs you to press and quickly release the volume up button. Then press and quickly release the volume down button. Finally, press and hold the side button until you see the Apple logo (this might take longer than 10 seconds).
Unfortunately, it did not work.
 
Then I found that I should connect my iPhone to my Mac and try to update it manually. I did and pressed the update button, but the update process did not complete and showed Error 4013. Error 4013 generally means the connection between the phone and computer was interrupted during the boot process. While this can be a bad cable, on iPhones stuck in a boot loop it is frequently caused by a specific hardware sensor shorting out. Therefore, I changed my cable, changed the port, and even restarted my Mac, but nothing changed.

{% include figure_half.html path="assets/img/blog/32.jpg" class="img-fluid rounded z-depth-1" width="40%" caption="" %}
 
Then I read on the Apple website that my macOS should be updated as well! So, I started to update it [Link](https://support.apple.com/en-us/109057). When my Mac update finished, I found that even recognizing my iPhone was harder than before! I even tried to do it through iTunes [YouTube](https://www.youtube.com/watch?v=BcBGD3SbFcs), but it did not work! Ah!
 
After a little search and asking Gemini, I learned that maybe ReiBoot software could help me, so I installed it.
I followed some videos like: [YouTube](https://www.youtube.com/watch?v=Klny7K6ecKo&t=208s). It could not bring back my phone from recovery mode and asked for upgrading. Tenorshare ReiBoot has a “One-Click Exit Recovery Mode” feature that is free to use. However, based on the Error 4013 I received earlier, ReiBoot likely could NOT fix my problem. 

{% include figure_half.html path="assets/img/blog/33.webp" class="img-fluid rounded z-depth-1" width="60%" caption="" %}

Before paying for premium, I found there is a free software named 3uTools for this. I followed some videos again to install it [YouTube1](https://www.youtube.com/watch?v=1s6Fi5_77pQ), [YouTube2](https://www.youtube.com/watch?v=cE4Tit_e6kE). In order to preserve data inside the phone, I needed to follow **Smart Flash > Select Firmware > Check “Retain User Data” > Flash**. I faced some interruption and errors.

{% include figure_half.html path="assets/img/blog/34.avif" class="img-fluid rounded z-depth-1" width="25%" caption="" %}
 
Then I downloaded the iOS firmware manually through [ipsw website](https://ipsw.me/iPhone12,1). On this website, you will see a list of iOS versions. Only click the ones in GREEN (this means it is “Signed” or currently allowed by Apple). I came back to 3uTools and imported the downloaded file.
 
It tried to flash and recover my phone, but at 21% it showed device disconnection and stopped. It happened over and over while the device was connected and the cable was the same. I searched about the reason and learned: when the phone tries to “transition” (restart) to install the update, it sends power to all its sensors. One of those sensors (likely the Earpiece Flex / FaceID sensor) is short-circuited (probably from a tiny drop of moisture in the past). And the conclusion was that I cannot fix this myself with a laptop. I need to physically bypass the short circuit and do a hardware repair. I looked around my home to find a local independent repair shop or Apple store, but it was the weekend, and I gave up spending more money on that as well.
 
Finally, I decided to order an iPhone 15 with my SIM card provider! In the future, I will try to recover my data if it becomes possible.

{% include figure_half.html path="assets/img/blog/35.png" class="img-fluid rounded z-depth-1" width="60%" caption="" %}
 
The following videos were also helpful in the recovery process: [YouTube1](https://www.youtube.com/watch?v=JyGT5hHWGgY&t=477s), [YouTube2](https://www.youtube.com/watch?v=iIchFgJJXNA)
 
Now that I am writing this blog post, I am only sad because of my photos. I wrote this post to be a little bit helpful for someone else to do the same process as I did, maybe it helps.

{% include figure_half.html path="assets/img/blog/36.jpeg" class="img-fluid rounded z-depth-1" width="" caption="" %}