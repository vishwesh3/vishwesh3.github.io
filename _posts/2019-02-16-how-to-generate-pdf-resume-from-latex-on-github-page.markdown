---
title: "How to generate PDF resume from latex on github page?"
layout: post
date: 2019-02-16 22:50
image: /assets/images/logo-botlatexx.png
headerImage: true
tag:
  - automate
  - pdf
  - latex
  - github page
category: blog
star: true
author: vishwesh
description: Get PDF files from latex within seconds.
---

_Everyone learn new stuff daily, achieve something new every day, builds new innovative projects now and then and definitely wants to mention them in their resume._ 

But with current tools, the process of updating resume is too time-consuming and most of us avoid until we are looking for a new job 😉. And this experience is even worse for those who maintain resume in latex.
Either setup tex environment locally ([3gb MacTex for Mac](http://www.tug.org/mactex/)) or use third party online sites.  

I am also the one who prefers latex resume. So for every single small change, I have to either rely on online sites like [Sharelatex](https://www.sharelatex.com/). Update `Tex` file there, download code and generated pdf and then upload back to [my GitHub page repo](https://jainkuniya.github.io). Another option for me was to set up [MacTex](http://www.tug.org/mactex/) locally. But having 128GB Mac, I can't manage to devote 3gb to this.

So to make this process seamless, I have developed [BotLatexx](https://botlatexx.github.io/). 
With this no extra work needs to be done in order to maintain an updated copy of your resume on GitHub pages, just make changes on `Tex` file locally and push it to GitHub repo. [BotLatexx](https://botlatexx.github.io/) will take care of everything for you.
 

_Watch the demo on Youtube, how I updated app downloads count to `40k+` in my resume which is hosted on GitHub pages in less than a minute:_
https://www.youtube.com/watch?v=P_5-_v2ttiU


**How it works**

In simple words, it builds your latex project on the cloud and returns your generated PDF.


Here is the user flow:
- You edit your `Tex` file locally.
- Push your code to GitHub repo.
- Check your resume URL, it will consist of your changes. It's MAGIC, it's MAGIC  

<img border="0" align="center"  src="/assets/images/its-magic-its-magic.gif"/>


**Behind the scenes**

Here is what [BotLatexx](https://botlatexx.github.io/) will do for you:

- As soon as you push code to GitHub, [BotLatexx](https://botlatexx.github.io/) will clone it.
- Configure your fonts and `.cls` files to the build system.
- Build your `Latex` project.
- Push back generated `PDF` file to your repo.
  
**Learnings**

- How to handle GitHub webhooks
- Ignore bogus call to the handler from fake webhooks
- Schedule task on the server
- Run tasks in parallel
- Write scripts to perform `git` commands
- Auto retry on failure
- etc etc  
  
_Watch the demo on Youtube, how I updated app download count to `40k+` in my resume which is hosted on GitHub pages in less than a minute:_
https://www.youtube.com/watch?v=P_5-_v2ttiU

**Conclusion**

_"Performing same steps again and again, is the work of bots, let's not snact work from them  😜."_
