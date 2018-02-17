---
layout: post
title:  "CCaaS - Architectures for 1 to 10,000s of Agents using Amazon Connect... It grows with you!"
author: dan
categories: [ connect ]
tags: [ connect , Architecture, eco-system]
image: assets/images/post-arch-1.png
featured: true
---
Contact Centers are known as big and complex systems, that take years to deploy and only the wealthy can afford market leading features... Amazon is trying to break that trend with Amazon Connect, in fact you can get a basic Contact Centre working in under 15 minutes!

>But don't think this is some kind of second class version... this is the same solution as the Enterprises use,

### Simple Architecture
![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAsuAAAAJDMyOWRhNzJmLTkwNjEtNGYyOS1hYzAzLTA1NTlhOTVhNTAzZg.png)
Here you can see what this looks like from an Architecture point of view... pretty simple right... But don't think this is some kind of second class version... this is the same solution as the Enterprises use, running on the same highly available AWS Infrastructure, that scales on-demand and you only pay for what you use! You get Telephony (0800 and 01/02x numbers) along with IVR Menus, Call Queues etc... and best of all you can add features to this as you grow.

This is perfect for

+ Small production contact centers (IT Helpdesk / HR etc..)
+ Organisations that are wanting to test and learn at pace

### Basic Architecture
Once you grow and learn with the solution you'll find more use cases for greater features and will start to drive your own backlog of work... you may end up with something like this:

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAA1wAAAAJDYyNjViYjM4LTI1NGYtNGQ3YS1iODkyLWY3OTAwOGUyMDlmNQ.png)


Ok, so we've added a few extra components here, but you get some pretty impressive features:

**S3**: This is used to Store Call Recordings, you have the option to Record Customer/ Client or both and store these from minutes to indefinitely. This is stored in Open format so you can add tools later to analyze the information or just simply listen to them via playback.

**S3**: You also use S3 to save Call Reports, like the call recordings you can save as many reports for as long as you like. And using a AWS service called Athena, you're able to query these flat files on demand at anytime!

**Lambda** is a special service I highly recommend you learn about.
Lambda: Lambda allows code to be executed on demand, what the code does is up to the developer building it, Lambda is a special service I highly recommend you learn about. In this scenario, we can use Lambda to affect the Customer Journey by Setting the music type, providing information to the caller, playing SSML (SSML is that sexy smooth voice experience from Alexa)... and it can integrate into many other AWS Services, here we are calling the DynamoDB Database.

**DynamoDB**: This is a NoSQL database from Amazon. You can store your customer orders in here, store account information, have an administration database to affect special routing etc.. When used in the Architecture above, we are able to use the Callers ANI (Phone Number) which is sent from Connect, to Lambda, which looks up in the database the callers order and provides the caller with personalized information! (Self Service) The information is Dynamic and Connect can handle that with its built in Text to Speech Engine (so no need for complicated IVR routing). You can also provide the caller options to update the information and Lambda can affect that in DynamoDB for you..

### More Advanced Architecture
>The great thing here is you get to see the value on a rapid development cycle

Ok, by now you can see how you can start small and build on your investment. The great thing here is you get to see the value on a rapid development cycle, and you'll start to drive your own wish-list as you see more value opportunities. So let's up the ante just a little...

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAycAAAAJGE2MjcwMjc2LTQ3YmQtNDc3MS1iZmJkLTRkODU3ZjgxNzcxYQ.png)

Whilst this looks like a significant advancement, it's still fairly contained. So let's build on the previous some more.

**S3**: This time we add a custom Administration Portal for your 'Ops Team' so that they can affect the routing via toggle buttons, they can close routing ad-hoc, play special messages (that they type into the portal) to respond to increasing demands etc..

**Lambda**: As previously, however this time we also connect to SNS, Simple Notification Service. This allows us to send Mobile Notification, SMS, E-Mails etc.. this can be DURING the contact (Top Lambda) or AFTER the contact (Bottom Lambda). In the bottom Lambda you can also do additional post processing of information to join data, run processes etc based on the result of the contact.

**LEX**: This is the AI engine that drives Alexa. You're able to provide natural conversational interactions for the whole journey or just parts of the journey... think when your customer connects with you, the first thing they hear/see is:

>#### Welcome to ACME Company, How can I help?

Note I say hear/see... this is because LEX is a Voice AND Text Chatbot service, code once and you can reuse that Chatbot within Connect (even export it to Alexa) and integrate it with your website / slack etc...

**Kinesis Streams**: This provides real-time streaming data from Connect of all the Contact Trace Records (CTRs).. these are the results of the contacts from Connect. The data sits in streams waiting for Lambda to do something.

**Lambda**: As explained above, this provides post processing of the records and can perform actions, like a post contact survey maybe, and sends the data onto Firehose

**Kinesis Firehose**: Firehose is a variant on Streams which is much more for batch type data movement, and is needed to feed Redshift

**Redshift**: This is Amazon's Enterprise Data Warehouse solution, you're able to run queries on massive amounts of data, this is where your data scientists will live. And the great thing is they will have Connect records within minutes of the record being generated.



### Summary
As you can see,

+ You're able to start small and grow with Amazon Connect
+ No two implementations will be the same, there will be a solution for you!
+ Most of this is built on server-less technology which greatly reduces your operational overheads... the only item with Servers here was Redshift and that can be replaced with other options, based on requirements.

I hope this was useful... any comments/suggestion or questions, please let me know

Kr, Dan
