---
layout: post
title: From 0 to remote GPU server (part 0)
subtitle: Introduction
image: /img/hdwr_intro.jpg
tags: Hardware
---

The purpose of this introductory post is to outline the structure of a few blog post series. These posts will describe my journey in going from having no experience in hardware at all to building remote GPU server. Well, I guess it is a bit generous to call a PC with 2 GPUs - a GPU server, but if I had more resources, it would be easily scalable to 4 GPUs. 

Ok, there are hundreds of blogs with titles like "Building your PC from parts", which is actually also a bulk of my story as well. So why write another blog? A few reasons. One, I have not seen a comprehensive blog which describes the full story from selecting PC parts, to building PC, to installing software, etc. Probably there are quite a few of those already, but given that I have not found any I liked, I thought there is some empty space to fill here. Secondly, and more personally, I want to start my blog where I mostly talk about machine learning (ML). And recently I have spent quite a bit of time figuring out ML tools side. Hence why not launch the blog with this?

Without further ado, here is the outline of this blog series:

- Introduction (part 0)
- Selecting PC parts (part 1)
- Building PC from parts (part 2)
- Installing software (part 3)
- Remote connection set up (part 4)

At the time of writing, I have completed all these parts. So those posts are guaranteed to come out. I am also considering now the possibility to place my GPUs outside the case, for various reasons. And I will look into benefits of overclocking GPUs from the perspective of deep learning (maybe I have just written a nonsense here, I have not looked into it at all, but my vague understanding is that you can set GPUs to run a bit faster than factory settings sometimes, if you do not have overheating problem). If I complete any of those steps (or some other hardware related steps), I will be adding to this blog series and describing steps taken and results obtained. 

Let me tell you now a few words about each of the different part. This way I hope to make it easier for people to orient themselves to the most relevant pieces of the text, in case they don't want to read everything from start to finish. 

**Selecting PC parts (part 1)** - will describe what kind of parts you need to buy, where to look for them, how to ensure compatibility, etc.

**Building PC from parts (part 2)** - will be about putting the parts together, most common mistakes in building PCs, how to debug in case things don't seem to work as expected, etc.

**Installing software (part 3)** - setting up Ubuntu, installing CUDA, cuDNN, Nvidia drivers. Installing Python, Jupyter notebooks, Pytorch. The goal is to end up with GPU based deep learning library.

**Remote connection set up (part 4)** - working through LAN or SSH. Working with Jupyter notebooks on your remote machine. 

I would like to end this post with a few imaginary questions a reader might have, and answer them from my personal experience. They are all geared towards answering the main questions - why should I build my own GPU server after all?

**Q: Is it cheaper to build it yourself?**

**A:** It really depends. Depends on what exactly you are building, and why are you building it. There is a logical argument why building yourself might actually be more expensive - the act of putting parts together should be quite cheap, as it is not very complicated. Plus, companies buying hardware parts in bulk should get parts cheaper, hence final product might be cheaper even after profit markup. So [you can](https://lambdalabs.com/deep-learning/workstations/4-gpu) buy GPU server ready to go. Nevertheless some people [claim](https://www.reddit.com/r/MachineLearning/comments/ayd01o/p_i_built_lambdas_12500_deep_learning_rig_for_6200/) to have built it considerably cheaper themselves. I think the cheapness argument outlined works more for mass produced PCs, rather than niche deep learning boxes. 

Secondly, if you just want to try out deep learning, then obviously there is no need to spend huge sums up-front to build full infrastructure. A cheaper version would be to try things out on, for example, AWS. But if you are serious about having high and consistent utilization rates across multiples of GPUs, then buying hardware is definitely cheaper then effectively renting it.

**Q: How long does it take to go through all this process?**

**A:** This process took me around 2 months from idea till completion. You are probably bounded only by PC parts delivery wait-times, if you are in a hurry, though.

**Q: Is it fun to go through this whole process?**

**A:** Yes! The moments when something starts working as required are truly happy moments (balances out a bit with stressful moments when things don't work and you start thinking that you have broken something). 

**Q: How much can you learn from this process about how PCs work?**

**A:** Probably depends on how involved do you want to be and how much do you want to understand about different parts and how they all connect together. You can just watch youtube videos, push things into right slots, and be done. Or you can carefully read manuals, try to understand more about different specs of each part, etc. Would this understanding help you to be better at deep learning? Probably not much. But spending a bit of time closer to the silicon is still helpful to become more comfortable around concepts like CPU, RAM, GPU, motherboards (since you are physically handling those parts yourself!). 

**Q: So eventually, why would you build your own GPU server?**

**A:** Everyone's situation is different. I had a few reasons why I decided to do it. Firstly, I decided firmly to start participating in Kaggle competitions, which imply very high GPU utilization rates. So doing it via AWS was out of question. Secondly, I wanted to understand a bit more about the hardware and how it all connects. This was just my curiosity, but learning by doing suddenly became an option. Lastly, I also thought it would be a cool challenge to build it all myself. 
