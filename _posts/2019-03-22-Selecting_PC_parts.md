---
layout: post
title: From 0 to remote GPU server (part 1)
subtitle: Selecting PC parts
image: /img/MB_link.png
tags: Hardware
---

In this blog post I am going to describe the process I went through while selecting PC parts for my GPU server. Target audience is people who pretty much know nothing about PC parts. If you have already built at least once PC, there will probably be nothing new for you here. But if you are just like me not so long ago, then this resource can be quite useful.

## General advice

Before we dive into individual parts, let's talk about a few general advices. 

Firstly, you will need to somehow track this whole selection process. If you have done at least one related google search, you probably already know about [PCPartPicker](https://pcpartpicker.com/). If not, I have just saved you one google search (not much, but, hey, its something!). This site has a free service, which allows you to search through a ton of different PC parts based on specified preferences on specs and prices. But most importantly, you can save selected parts into a PC-build, and you will get compatibility across selected components automatically verified. This is extremely useful, because some parts do not work together. For example, different motherboards only accept specific CPUs. The site essentially ensures you will not make a mistake of buying incompatible build. Its secondary utility is providing price comparisons across different buying options (like amazon, newegg, etc.), as well as conveniently summing the prices of your whole build. I have found those prices to be a bit stale and not 100% reliable, but still useful.

I would advice to just immediately login and create account, because [PCPartPicker](https://pcpartpicker.com/) will probably be your friend thoughout the whole part selection process. I made a mistake of creating my build as a guest, and accidentally lost it when my wifi disconnected.

Secondly, I was overwhelmed by the myriad of different selection opportunities for each part. Sometimes the decision which exactly part to choose could appear completely random, especially if you do not have strong preferences for, let's say a CPU cooler. Often, even if you have specific preferences, you will still be left with 10s or 100s parts to choose from which meet your requirements. To simplify the process, I used a rule of thumb to help me decide which single part to eventually select - take the one with the most positive reviews. Positivity is obvious criteria. But I also wanted the part to be popular. The logic here is that if something does not work for me w.r.t. that part, I will more easily find help online. Popular parts will more likely have specific youtube videos which explain how to install them, or, if I have some further problems, it's a higher chance that someone will already have a discussion going how to debug and solve my specific issue. 

Lastly, credit where credit's due, and I have to cite one of the best blog posts about selecting PC parts with a leaning towards building multi-GPU equipped machine - [Tim Dettmers: A Full Hardware Guide to Deep Learning](http://timdettmers.com/2018/12/16/deep-learning-hardware-guide/). Original post was written in 2015, but it has just been updated at the end of 2018, so I would invite everyone to read it again (or for the first time) - there are a ton of good advices there. Original post helped me a lot as well, while building my first GPU server. 

In the following discussion I am not going to specify exact parts I was buying. The purpose of the post is rather to familiarize the novice reader with required hardware, and to present some advices and thoughts on trade-offs. This is as opposed to simply outlining final solution. Some blogs do that, and at the end of the post I will provide the links to my favorite ones. 

## All the parts we will need 

We will look to choose the following parts:

* Motherboard
* CPU + CPU cooler
* GPU(s)
* PSU
* RAM
* HDD and/or SSD
* Case

**Motherboard** is a part to which all other parts connect. **CPU** performs majority of non-deep-learning (i.e. not GPU based) computation (running Python script in majority of use cases would be performed by CPU). As someone once explained it very nicely - CPU is a rock we tricked into thinking. **CPU cooler** is, well, cooling CPU, to offset CPU generated heat once CPU converts electricity into computation. **GPU** used to be primarily focused on displaying high quality video for games, but now is actively used to do deep learning (where the job of GPU is mostly to perform matrix multiplications). **PSU** distributes electricity from electrical power socket to motherboard and other parts which need additional electricity. **RAM** is your PC's fast but small memory. **SSD** is your PC's slow but larger memory. **HDD** is your PC's slowest but largest memory. **Case** is where you keep all these parts.

Notice I do not have screen as a separate part here. That's because I will talk about building GPU server to which will connect remotely from our main PC with screen, keyboard and mouse. This one will be so called headless PC.

Now let's dive into each of these parts one by one.



## Motherboard

Motherboard will determine what kind of architecture is possible. The key requirement for me was that it would be able to support 4 GPUs. As I have figured out while thinking that I will add a few GPUs to my main PC, this may not be possible. Motherboards have some number of PCIe connections installed, and each GPU will require separate PCIe connection. So if there is only a single PCIe connection, you can only have one GPU on that motherboard. So here is the first selection criteria - motherboard should have at least 4 PCIe connections. Those connections are also evaluated from x16 to x1. This determines theoretical bandwidth of how much data could be transfered in 1s to and from GPU. This may sound as very important, given that moving data to and from GPU is a potential bottleneck in deep learning computation. But as far as I know, if GPU is connected to x8 PCIe, then performance hit is minimal. Note that this discussion focuses on capacity numbers. Physical size of PCIe connections should all be as x16, because GPUs are all expecting x16 physical size connection. You can just look at longest PCIe connection, and that one will correspond to x16. There should be at least 3 more connections as long as the longest one. 

Those connections should be appropriately spaced out. I know this does not sound concrete at all, but you will see that some motherboards have PCIe connections closer to each other, and some have further. The further the better. That's because GPUs usually take 2 slots of PCIe connections in terms of their width, so if you have PCIe connections too close to each other, one GPU will block connection for the other. This is not unsolvable, you could use extensions to connect GPUs to motherboard, but why bother on your first build?

![MB](/img/MB.png)



Above is an example of my motherboard. Widely separated yellow connections at the top (in blue box) are PCIe connections. As you can see, they are all of the same length (so physically x16), and are not too close to each other. 

From my perspective, that was the main requirement for the motherboard. In retrospect, I could have also required on-board wifi adapter (so that wifi would work immediately after some default drivers installation). My board did not have that and I had a bit of a problem with adding ad-hoc wifi adapted and installing its drivers. On the other hand, on-board-debugger (seen in top left of the board above) was a very nice addition to the board which I was not expecting or even thinking about. It was flashing on some error codes during my initial attempts to get my PC to work, and manual was explaining some likely problems of my set up (this way I identified that my RAM was not fully pushed into the motherboard, as an example).

The second thing to realize is that motherboard will determine what kind of CPU you can buy. This will be highlighted by socket type (a code which looks like LGA 2011-3). So you can choose motherboard, and select from compatible CPUs, or choose CPU and select from compatible motherboard, or iterate two steps until convergence. 

So here we are with our main requirements:

* 4 PCIe connections, x16 in physical size, preferably widely separated

* Compatible with chosen CPU

* Onboard wireless (optional)

* Board debugger (optional)

  

## CPU

First question - Intel of AMD (two main producers of CPUs, but Intel dominates). I have chosen Intel. Reasoning was that Intel is more dominant player, and I was afraid that some libraries will be specifically optimized for Intel by default (their MKL and BLAS, LAPACK), and I will have troubles to fully understanding whether I have any bottlenecks and how to overcome them with AMD CPU. This may be totally false impression though! And consensus is probably that AMD is better bang for the buck at the moment. But I just wanted to minimize potential problems with my first build. 

Second question - i{5,7} or Xeon. I think I have made a mistake here by choosing Xeon. I was under the impression that Xeon is more oriented to parallel execution, and i{5,7} are more focused on fast but smaller number of cores. Hence I was thinking that I will pay less for combined multi-core computation if I buy Xeon. Later research revealed that to not necessarily be true, and Xeon CPUs are probably getting price bump for Error Correcting Code (ECC) memory (essentially they are less likely to fail). Given that participating in Kaggle competitions is not mission critical, I would now say that ECC memory is not necessary. Lesson learned - I need to go ahead and actually check various claims I see on internet (specifically here - that Xeon is cheaper on per compute power basis).

CPU was the only part where I actually found some better search tools than [PCPartPicker](https://pcpartpicker.com/). I would recommend checking out [Intel's own search](https://ark.intel.com/content/www/us/en/ark/search/featurefilter.html?productType=873), which unsurprisingly has very detailed search capabilities. [PCPartPicker](https://pcpartpicker.com/) was unable to condition on PCIe lanes in CPU, which I wanted to ensure is high enough. Now if you have read [Tim Dettmers: A Full Hardware Guide to Deep Learning](http://timdettmers.com/2018/12/16/deep-learning-hardware-guide/), you will know that CPU PCIe lanes are not his favorite things. However, Tim acknowledges that if you have 4 GPUs (and this was kind of my end goal), you would need at least 4 * 8 = 32 lanes. This is lower bound. Wifi adapted, SSD may also consume PCIe lanes, if they are connected via PCIe. So just to sleep calmly at night I required at least 40 PCIe lanes in my search. 

Then another important thing to keep in mind is that CPUs have limit to how much RAM can they support. If you are buying powerful motherboard with 8 RAM slots, that' potentially 128 Gb of RAM available to you (8 * 16 Gb = 128 Gb). In that case, make sure your CPU will be powerful enough to support that kind of RAM as well. 

Then there is just the optimization left with your budget vs number of cores and vs processor speed.

My search conditions could be seen below.

![CPU choice](/img/CPU_choice2.png)

CPU considerations:

* Lower bound on PCIe lanes around 40 for 4 GPU system

* Match memory to the one available in your motherboard

* Optimize speed and number of cores based on your budget

  

## CPU cooler

Liquid or air, that's the question here. My answer was liquid. Air coolers can be very massive, and may not fit into a small case (we will talk about cases later). I was thinking that there will be more trouble to install massive parts onto the motherboard, as they will start blocking my view of the rest of the motherboard as well. So once again, given this was my first build, I went with a liquid AIO (all-in-one) cooler option which appeared to be less likely to cause some problems down the road of the build process. 

Secondly, behavior of air cooler is to push hot air away from CPU. But this happens inside the case. It can be a problem when we will also have 4 hot GPUs in the same case! Water cooling is a better option here, because it to some extent brings the hot CPU air outside of the case. (Warning, this is a personal interpretation of how coolers work, so can be wrong!).

Lastly, liquid coolers should be at least somewhat more efficient than air coolers. Though this is probably not too relevant here, if you are not over-clocking your CPU. 

Air cooling would be cheaper though. And liquid cooler can experience a pump break, and leak water onto the motherboard. 

Summa summarum, I went with liquid AIO cooler, but I think this decision is not very important. 



## GPUs

Alright, now we're talking! This is probably the most important decision. It will be the most expensive as well. We are doing all this "build-business" to embrace the power of GPUs, so let's not mess it up here (like I did, to some extent). Recommendation is to buy RTX 2018 Ti. 

I, unfortunately, bought GTX 1080 Ti. [Nvidia has ended their production](https://www.pcmag.com/news/364813/report-nvidia-ends-gtx-1080-ti-gpu-production), so I bought 1 card (as I did not want to go all in and buy all 4 in one go), and a few months later I found some nonsensically high prices in secondary market. That  actually saved me from buying this card again. The problem with GTX 1080 Ti (which I realized too late) is that it does not support half precision. Oh well, you live and you learn. 

So then I bought RTX 2080 Ti. Sounds good so far... but! I managed to buy a super wide card (taking up three side case slots), as shown in the picture below.

![GPU](/img/rtx2.png)

Typically GPU width is only 2 expansion slots. I missed this one being having 3 expansion slots instead, because I though that is impossible! Now this card is blocking one of the PCIe connections, which means I cannot have 4 GPUs on my motherboard. To solve this, I will later try to take the GPUs out of the case via PCIe risers. Will probably write a post about that as well, once this is done. 

If you think my fails ended there, that's very nice of you, but you are unfortunately wrong. As I have learned from updated post of [Tim Dettmers: A Full Hardware Guide to Deep Learning](http://timdettmers.com/2018/12/16/deep-learning-hardware-guide/) - you should buy blower style GPUs, if you want to have 4 of them side by side in the same case, as otherwise they will most likely overheat (with air cooling, which is what I bought). Actually, very good explanation of air vs blower fans is [here](https://www.youtube.com/watch?v=0domMRFG1Rw). I again hope that solution of "GPUs out of the case" will come to the rescue. If I manage to take GPUs outside of the case, I could spread them out more widely in space, and air cooling should do a good enough job to keep all 4 appropriately cooled. 

Eventually, this is what I would do, if I could travel back into the past:

* Buy 4 RTX 2080 Ti

* Blower style fan

* Width of 2

  

## PSU

Don't save money here. Buy high efficiency PSU (gold or platinum). That is good from two perspectives - your electricity bills will be smaller, and also PSU will probably work longer before needing a replacement. How much watts? RTX 2080 Ti consumes 250W. So 4 of those will be 1000W. Then let's give 200W to CPU, 200W for other components, and we have 1400W. So I bought 1600W just to be safe. As you can read in [this blog post](http://l7.curtisnorthcutt.com/build-pro-deep-learning-workstation), too weak PSU can be a point of failure of the whole build. 

* 1600W gold or platinum PSU

  

## RAM

This is relatively straightforward decision. You will need DDR4 type memory (DDR4 just stand for latest technology of RAM). You will also see DDR4-XXXX, where following 4 numbers supposedly relate to memory speed in Mhz. But as [this](https://www.youtube.com/watch?v=D_Yt4vSZKVk) video explains (which I again actually noticed in Tim's blog), there is no practical benefit of buying RAM with Mhz speed above 2400. This simply will not improve anything, unless you will fiddle substantially with BIOS. 

One advice, however, would be to buy 16Gb per piece (RAM prices are called DIMMs), as opposed to 8Gb per DIMM. This does not have any instantaneous monetary savings, and actually can be a bit more expensive. But chances are that eventually you will want to max out on all possible RAM that your motherboard allows, if you start with 8Gb RAM pieces, those will need to be replaced. 

Controlling for these metrics, price variation mostly depends on decoration of DIMMs. 

* DDR4-(2400-3000) 16Gb RAM DIMMs

* (Optional) RGB decoration, if you want to have Christmas tree at your place all year round

  

## SSD/HDD

HDD (Hard Disk Drive) is slow (~100Mb/s read/write speed), but cheap. Primary purpose for HDD will be to hold all your datasets. SSD (Solid State Drive) is more expensive, but considerably faster (can be more than 500Mb/s read/write speed). This is where you would keep the dataset of project you are working on at the moment. 

Note that there is an option to buy just HDD or just SSD. It depends on how you are planning to use the machine. If intended use is focused on computational power, and you are not planning to keep around the graveyard of old datasets (at least not on this particular build), than you are good to go with SSD alone. Just make sure that SSD will be sufficient for your largest dataset. Typically SSDs are of at most 1Tb.

HDD decision is quite easy. Just choose desirable storage capacity, and also consider RPM (but I admit I have not looked too closely at how impact RPM number is on performance). I will not talk much more about HDDs, because seems like they will soon be obsolete and replaced by SSDs. 

SSD is a bit more nuanced. There is the same capacity choice, of course. But then there is also different options on how SSD connects to motherboard. Two most common ways to connect are SATA and PCIe. As things are often in life, one option is slower and cheaper (SATA), while another is faster and pricier (PCIe). But additional consideration here is also whether your motherboard will have remaining PCIe connection, after you install all intended GPUs. If there is no PCIe, you cannot use PCIe connecting SSD. SATA connection is almost guaranteed to exist on any motherboard you buy, since this is relatively old (classical, to put it in a nicer way) and wide-spread connection type. 

Another term you will see if you venture on the search for the best SSD is M.2. This refers to form factor of SSD. What is a form factor? one may ask. That's kind of the description of physical size and shape of SSD. If form factor is 2.5'', then you know you will deal with little black thin box. This form factor also implies that SSD will be connecting to motherboard via SATA connection and via cable. Form factor can be PCIe, which will mean you will connect SSD similarly like you connect GPU. M.2., however, will either connect in PCIe, or in SATA mode (its unfortunately not up to you, it is either one OR another), and SSD will be small green chip which will be inserted directly into motherboard through a specialized connection (will be noted M.2 in motherboard manual).

Finally, NVMe (Non-Volatile Memory express) enters the stage. This actually refers to newest storage protocol that SSD could use. Turns our SSDs were kind of using a knock-off of HDDs protocol, to some extent. And NVMe is a new protocol, which is optimized specifically for SSDs, having in mind also that they will be connecting via PCIe, and not SATA. So yes, you guessed it right, for some additional price, you can get even faster SSD, which uses NVMe protocol.

After all this complicated terminology

* Safest bet is 1Tb SATA SSD

  

## Case

Final decision = easy decision. Case type needs to matched to your motherboard type. After that, you will typically have a choice of Mid Tower vs Full Tower. I would recommend Full Tower. In fact, I would simply recommend as large as possible motherboard compatible case. You can never get into trouble if your case is large. There is no such thing as too-large case. On the other hand, you can get into various problems if the case is too small (for your GPUs, for CPU cooler, etc.). 

Second benefit of larger case is that it is easier to assemble all parts. You have more room for movements of your screwdriver. You do not have to solve the puzzle of how to position different parts so that they would not be blocking each other and you could easily access all other connections on motherboard. 

Last benefit of bigger case is that it will have more fans (so better cooling). In a similar way, since there will be more  air volume inside the case, you will have less problems with overheating (by analogy, AC takes more time to heat a larger room). 



### That's all!

Thanks for reading till then end! 

For broader understanding and different perspectives, I would also recommend to look at [this](https://medium.com/yanda/building-your-own-deep-learning-dream-machine-4f02ccdb0460), [this](https://medium.com/the-mission/how-to-build-the-perfect-deep-learning-computer-and-save-thousands-of-dollars-9ec3b2eb4ce2) and [this](https://blog.slavv.com/the-1700-great-deep-learning-box-assembly-setup-and-benchmarks-148c5ebe6415) blog posts. Maybe also [this](https://towardsdatascience.com/assemble-an-amazing-deep-learning-machine-at-home-for-less-than-1-500-ef046d21b179) and [this](https://towardsdatascience.com/build-and-setup-your-own-deep-learning-server-from-scratch-e771dacaa252).



  








