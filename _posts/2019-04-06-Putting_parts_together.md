---
layout: post
title: From 0 to remote GPU server (part 2)
subtitle: Putting the parts together
image: /img/hdwr_p2.jpg
tags: Hardware

---

Alright, so we have bought all the part. How do we put them together?

Blog post is probably not the optimal medium to talk about this, and youtube videos might be a more informative illustration. On the other hand, motherboard and part manuals should be your best friends during the process of assembling your mighty GPU server. So in compromise, I will share some of the links to videos which have been the most helpful to me during my first steps of assembling, but I will also carry on with the blog post and outline lessons learned after this experience, and things I would do differently right now. 

[This video](https://www.youtube.com/watch?v=IhX0fOUYd8Q) is very useful and exhaustive. It is probably the most popular video about building PC on youtube. I also liked [this one](https://www.youtube.com/watch?v=dA-JzXV49YY). Aside from these two, I only watched a couple of specialized videos which talk about how to install a few of my parts.

## Step-by-step plan

I found it very helpful to have a full sequential outline of which parts will connect where and how, before I even started unpacking everything. I googled around a bit, and there are a few variations of proposed steps. I have chosen to follow the one below. 

1. CPU to motherboard
2. RAM to motherboard
3. PSU to case
4. I/O shield to case
5. Motherboard to case
6. CPU cooler installed
7. SSD/HDD to case
8. Mount all cables
9. GPU to motherboard

And you have it! 

Let's talk about these one by one.

## 1. CPU to motherboard

Not to stress you out, but this is the step which can cause the most expensive mistake - breaking the CPU. First good idea is be careful not to touch the surface of CPU at all (only the sides). The second good idea is to be very gentle while placing CPU on motherboard. But you also need to make sure that it locked correctly. I was trying to very softly move CPU to any of the four sides to be sure that it is firmly locked in place. If it is not correctly placed, pressing it down with locks will break it. And it will probably damage motherboard as well. 

A paradox here is that after being very gentle, you will need to exert quite a bit of force to pull down those levers which lock CPU in place. I have noticed a number of first-build bloggers complaining that it was a bit scary to push those levels to such extent. I felt the same, but I was already familiar with this problem, and I was sure that CPU is positioned correctly, so I just went forward and all ended well. 

Finally, don't forget to check your motherboard manual here. It can be that there is a specific order in which CPU  holding levers need to be locked. 

## 2. RAM to motherboard

This is considerably easier. Also, there is little gap in RAM blocks which would not even allow you to insert the RAM DIMM on the wrong side (unless you are very strong). However, you can accidentally insert RAM blocks in the wrong order. If you do not fill all available slots on the motherboard, check the manual to see which slots should be occupied when using your specific number of RAM DIMMs. 

The key here is to un-lock the clipper by pressing on it on one or both sides (depending on the motherboard) of the RAM slot, and then gently insert the RAM piece, trying to maintain equal pressure along the whole connection with motherboard (easier said than done). Clippers should then jump back to lock the piece themselves.

I had an issue where some RAM blocks were not fully inserted on one edge, but fully inserted on another edge. Now to check that this is not the case I always push a bit on one side and on another side separately, when I think that RAM block is fully in. 

## 3. PSU to case

Put your case sideways and place PSU in its designated position (usually at the bottom of the case). You may need to move it through specific opening at the side of the case, or simply place at the bottom of the case, depending on case design. 

Don't screw any screws yet. Having flexibility with PSU position will be helpful when you will be connecting it to motherboard, CPU, GPUs, etc. 

## 4. I/O shield to case

I/O shield is a small part which comes with your case. Its purpose is to cover gaps between direct USB, LAN and other connections to motherboard and case. This is for protection of what is inside the case, to some extent.  

This is very small step, but easily overlooked. I overlooked it initially. The annoying part is that if you add motherboard to the case without I/O shield, you cannot add I/O shield later. At least in my case it was impossible, and I had to undo everything up until this step, once I noticed I missed it.

## 5. Motherboard to case

Alright, let's put that motherboard to the case! There will be 6-10 screws to screw. Easy step. Just follow the manual. 

## 6. CPU cooler installed

This is where the benefits of large case may start to kick in. Liquid cooler will have a radiator, which you will have to find some place on the side of the case. Air cooler will hopefully be not too tall for your case width (actually, compatibility of all parts should have been ensured before buying parts, so hopefully there is nothing to hope for at this stage!). 

This step might be a bit scary initially, because you will most probably have to deal with thermal paste here. The unanimous rule I have heard is that less is more. You should probably aim to have a size of grain or pea worth of thermal paste in the center of your CPU. Secondly, I was surprised that you have to screw the screws in specific order (you necessarily need to go diagonally). Retrospectively, that makes a lot of sense, as it helps for thermal paste to be spread out more evenly. Also, this is a good lesson that you should always read manuals! Common sense just cannot get you all the way here. 

I messed something up and needed to undo the cooler part. That sounds and looks worse than it is. But if you ever need to clean up thermal paste, then alcohol pads work quite well. 

## 7. SSD/HDD to case

HDD will probably be held in a small drawer within the case. SSD can be in a similar drawer, could be attached to the case in parallel, or could connect directly to motherboard. It depends on the case and which specific SSD did you buy. 

Nothing too much worth mentioning here.

## 8. Mount all cables

This is going to be a test of how much do you care about the future, and your short-term vs long-term reward balancing. 

Cable management is very important, especially in cases where you are planning to keep adding new parts (for example, another GPU) later on. Proper cable management will help you in the future. It is also not just about being tidy or untidy. Jungle of cables in the wrong place may make your cooling fans less efficient, if cables block air flow. If cables are touching something they are not supposed to touch, I have heard stories of cables starting to melt (though that sounds a bit too extreme). Advice is to take your time with this step.

At this step you can connect case fan cables to motherboard, CPU to PSU, CPU fans to motherboard, motherboard to PSU, and probably a few other cables that I have already forgotten about.

## 9. GPU to motherboard

For a dessert, insert you GPU(s) into PCIe connections. 

Firstly, make sure that all plastic stickers are removed from GPU. There can be a lot of those, and some are small. Then you also need to unscrew and take out PCIe connection blocks at the side of the case. Once that's done, gently insert GPU into PCIe connection. There will probably be locks similar to the ones you have dealt with during RAM step. Screw GPU to the side of the case. Connect it via cable to PSU. The fact that you did not firmly attached PSU yet might be useful here, as it will hopefully be a bit more convenient and flexible.

Once all GPUs are in, finish fixing in PSU as well. 

## Conclusion

Connect PSU to electric power, flip PSU switch from 0 to 1 (my guess is that a lot of people forget this in their first build, me including, and then stress out when nothing works), and press the power button. First good sign would be that case fans kicks in. That means power is flowing from PSU to motherboard. Second good sign is that GPU lights up (usually Nvidia GPUs have some lighting decoration). Third good sign is that something appears on the screen. 

Yeah, about the screen... This is probably the first time I mention it, but it will be needed for installations. Whoops, sorry about that. Hopefully you can borrow it somehow for a brief period of time. Idea in this series is that we are building GPU server - so headless machine without screen, keyboard or mouse. Those unfortunately will be needed temporarily during the software installation process. 

But that is the topic of the next blog post!

### Debugging thoughts

If there are some issues, than you could try a few things out to identify what is causing the problem. 

* If case fans don't work, there might be issue with PSU, or how it is connected (unless some PC parts like GPU, CPU cooler, etc. lights up)
* If fans work, but some parts do not light up (when they should), there is a specific issue with how those parts are connected (or parts could be faulty)
* If everything seems to work, but you see nothing on screen, then you have potential problem with RAM (either inserted incorrectly, or RAM sticks are faulty). Advice is to check whether you can see something on the screen when you use only single RAM DIMM (connect it to required slot according to manual).
* If you immediately connected multiple GPUs, but screen does not work, try connecting screen to different GPUs, or try running the set up with a single GPU in first PCIe connection.
* If you have another PC, there is always a possibility to swap parts one by one and eliminate possibility of faulty parts like this (or identify a faulty part, which would be a step forward towards fully functioning set up!).

### Upgrading

I was searching on the web for how to add second GPU to PC, and did not find a clear answer. That's because it is probably obvious to everyone, except me. If you are like me, then the following paragraph might be useful.

There is almost nothing in addition that needs to be done when you are upgrading! Just turn-off PC, unplug electricity cable, turn off PSU (just in case), open case, insert new GPU in the same way that you inserted first (so you have to connect it to PSU as well). One tricky part could be that there some small flips in your motherboard will turns on and off some PCIe connections. Make sure that second connection where you have just installed your GPU is on. And that's it! Once you fire up your machine again, you should have 2 GPUs functioning!

The same goes to adding more RAM. Just unplug everything, add RAM sticks to appropriate connections, connect everything back up. Boom, you have more RAM!





  







