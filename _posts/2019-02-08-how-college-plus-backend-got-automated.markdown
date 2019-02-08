---
title: "How College Plus backend got automated?"
layout: post
date: 2019-02-08 23:44
image: /assets/images/college-plus-logo.webp
headerImage: true
tag:
  - automate
  - backend
  - software
category: blog
star: true
author: vishwesh
description: From ~12 hrs of manual work to 1 min.
---

*Everyone of us remember our firsts, the first success, first failure, first medal, first trek. I know where are you going now, hold on! Today I'm going to talk about my first project in my development journey.* [College Plus](/project-college-plus/). 😍 I learned Android development while working on it.

_Watch the demo on Youtube:_
https://www.youtube.com/watch?v=SlszrEz5KJg

College Plus Android app provides information about mess menu, lecture schedule, bus time table etc to college students.

Here is the link if you want to explore or use it:

<a href="http://bit.ly/college-plus" target="_blank">
  <img width="180" height="70" border="0" align="center"  src="/assets/images/play-store.png"/>
</a>

Following were the challenges I faced while developing College Plus:

**Challenge 1**

I knew that mess menu, lecture schedule will change from time to time. And it will become too hard to maintain an app with updated on play store. So keeping this in mind, a dedicated server was deployed which is called by app n order to fetch the latest data. And ya it worked. I was very happy to see that the app which I developed in my first year got adopted by the majority of the college 💚.

**Challenge 2**

After a few days, I realized that it is taking a long time to manually update data from PDF (which are shared by college authorities) to an externally hosted database. Mess menu usually get changed every two months, the lecture schedule gets changed every semester i.e 4 months. Sometimes it was taking ~12 hrs to manually update hundreds of entries in the database. Data entry is one of the most boring work and nobody was volunteering to do it.

I talked to a few people to solve this, all suggested to create a portal for admin and ask college authorities to directly update in the database. But this was again a lot of coding work and most importantly coordinate with appropriate authorities.

One fine day, a thought came to my mind why shouldn't we automate this process.
I mean let's write a script which converts PDF to `JSON` and then pushes it to the database.

And the next day of this, College Plus was again back to work 😅.

**Here is how the whole process got executed**

* Migrated old PHP server to Python, Django.
* Created a sample HTML page to upload PDF files.

The main challenge for me was to convert PDF to `JSON` which is a memory consuming task on a free server resource available to me 😜.

So

- HTML page sends an upload file request to the server.
- Server saves file.
- Create a new task to process each file and add it to the queue.
- Return response to the upload request.

And now the real work:

- For each task server does pre-process of each file i.e
  - Split PDF into multiple files each having 1 or 2 pages each.
  - Remove unwanted stuff, so that size reduces.
- Get `JSON` data from the PDF file.
- Clean up data.
- Push this data to the database.
- Notify app users.

**System Design**

<a href="https://www.youtube.com/watch?v=SlszrEz5KJg" target="_blank">
  <img border="0" align="center"  src="/assets/images/college-plus-backend-system-design.png"/>
</a>

Files are uploaded via a web portal. The system verifies that files are uploaded by authenticated users. Then preprocess file by splitting the file into multiple files for fast parallel processing and add the task into the queue. Now the different thread which is running in background founds that there is a new task to execute, it picks up and gets `JSON` from PDF. Now the system removes the noises from the `JSON` data and pushes to the database.

Now to scale this system, background worker instances are increased to handle multiple requests.

_Watch the demo on Youtube:_
https://www.youtube.com/watch?v=SlszrEz5KJg

**Learnings**

- Initiate the background process.
- Manage multiple threads.
- Handle queue data structure.
- Handle PDF -> `JSON` conversion gracefully and retry on failure.
- etc etc

**Conclusion**

_"Never think that it is of no use, everything has its own importance, just wait for right time."_
