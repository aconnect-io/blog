---
layout: post
title:  "My First AWS Contact Centre – Basic Intro"
author: dan
categories: [ connect ]
tags: [ connect , intro]
image: assets/images/Title-Comprehend-Pipeline.png
---

Note: This is a re-print from 30th July 2017 originally posted on my personal blog but moving it to LinkedIn,
This evening I signed up for the Amazon Connect service, if your not sure what that is, it’s a contact Centre solution from Amazon that allows businesses to make and receive customer contact via Telephone/Chat Bot, provide self service features and speak to an agent. You might be thinking, urgh… isn’t everything web based, bots and AI, I’m not going to go into that here, there are plenty of articles around, lets just say human to human contact is not dead yet.

Amazon Connect is new, it’s been under wraps (as “Lily”) and earlier in 2017 it was announced with little fan-fair. Today (30th July 2017) you can only get Connect within US East (N. Virginia) and Asia Pacific (Sydney), I usually see AWS Features roll out to EU_WEST_01 (Ireland) after US_EAST_01 so it’ll be interesting as to why Sydney was next. Anyhoo, this doesn’t stop us from having a play with the service and seeing where Amazon are taking this.



Connect is a PAYG model for pricing, you only pay for the minutes used, it scales automatically and there are no upfront or monthly charges. Do note that you will pay on top for Lambda Execution and S3 storage costs (for call recordings/report storage).



### Creating ‘My Frist AWS Contact Centre’
You access Connect from the aws.amazon.com portal you are then sent to the Connect

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAo1AAAAJDA5YmFhZDExLTc0ZmItNGNiNS05Y2FlLTM3ZGUwZjAzYmY4Mg.png)





Creating a new instance is super easy (scary considering all the man years I’ve personally spent building them). You simply

+ Name your contact centre (Or link via AWS Directory + Services to your on-prem AD)
+ Create an administrator
+ Choose telephony options (Inbound and/or outbound calls)
+ Agree to store data in S3
+ Hit create

From there you have a shell of a contact center, you cannot yet dial until you claim a number.

All the options above can be amended after your instance has been built, except for the Name/Directory. You also get some additional options which look very interesting:



+ Data streaming (Contact Trace Records sent to Kinesis Stream or Firehose)
+ Application Integration (CRM and WFM) Salesforce and ZenDesk also + https://github.com/aws/amazon-connect-streams
+ Contact Flows Security Keys (x.509 cert to encrypt caller entered data)
+ Lex (This allows you to use BOTs built with Amazon Lex and route unanswered queries to your Contact Centre) I’ve linked my demo Lex bot for a future play and blog

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAxsAAAAJDViZWFhNzc4LWI2NmItNDIyZi1iMDk4LWVlZDBhYmU5YzE4Nw.png)

### Getting calls into ‘My First AWS Contect Centre’

Once your instance is created, then you can login to it, again via the aws.amazon.com console but this time you get a URL that you can use to login to to bypass this step, this demo one is https://myfirstawscontactcentre.awsapps.com (Because I’m not using Directory Services I can use the built-in IAM users.

 Ok once logged into my Contact Centre, you get a step by step guide to getting started.

1. Claim a phone number
2. Set open hours
3. Create Queues
4. Create Prompts
5. Create Contact Flows
6. Create Routing Profiles
7. Configure Users

Claiming your phone number was a case of choosing Toll-Free or DID and them choosing from one of the 5 options that i had (Currently you cannot bring your own – based on their job adverts in US, this is a matter of when). Once selected I could dial the number that has the default IVR Menu and was able to route a call to myself. Amazon provide you with a WebRTC based phone that as I’m using Chrome requires no additional plugins and you get quite a nice little softphone.

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAqlAAAAJDg2ZDk4MmE5LTgyYTctNDZkZi1iN2U1LWNmYmFhZGYyZjE4NA.png)


I also got a nice toaster notification from Windows 10

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAs9AAAAJDgxNWJiZThlLTcwMGQtNGMwYy1iYTkxLWEwNzYyZjZmZWFmNw.png)


The last screen grab from the softphone is from the Settings page. I was unable to test out the Desk phone as I don’t have a US number and I didn’t want to fudge it via Twilio or Plivo. Having read the documentation it’s highly likely that this feature connects on demand to the number that you put in here, from their you use the softphone to control the call (Hold, Transfer etc..)

 **Setting hours of operation** is simple, but overly so, if you’ve ever managed a contact centre I’m sure you’ve experienced the complicated mess of open hours by department over the Christmas break, Sales want to do X, Service Y and Niche Team Z. Connect can allow you to do that today by assigning the hours template to the queue, but the hours template is clearly version 1. There is no ability to create schedules, allow for bank holidays, special dates (Company Conference) or plan in advanced holiday closed hours (I’m sure this will come as the product matures)

 After **Placing my first inbound call** into the contact centre I was greeted with a basic IVR Menu that says:

“Press 1 to be put in queue for an agent.

2 to securely enter content.

3 to hear the results of an AWS Lambda data dip.

4 to request a call back.

5 to set a screen pop for the agent.

6 to roll the dice and simulate a and b testing.

7 to adjust the priority of the contact queue.

Or 8 to set call recording behavior.”

As you saw from the screen shots above I had pressed 1 to be placed into a queue so I could show you the agent experience. I didn’t however sit and write out the whole message… I simply got the above text from the Contact Flow Editor which is the place where IVR Menus are created. Amazon have provided you with 7 Prompt Wav Files (Beep and Queue) and 19 Contact Flows to get you started. One of the contact flows was for the Sample inbound flow (For which my DID is pointing to), clicking on this bring up a familiar IVR Builder,

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAA3nAAAAJDFlZjIyMzA5LWI4ODYtNDQ5MC1iYmU1LTIzNGU0MDM3ODExZg.png)



And as you’d expect Get Customer Input element has the text within as the Contact Centre is using TTS (Text to Speak). I’ll spend allot more time with the Contact Flow Builder for a later blog but first impressions are its clean and has the ore mark of being a powerful editor, but its missing some useful feature like real-time data and testing (and please let me click on a line and it stay highlighted!), those with any previous contact centre administration will be able to pick this up with ease. I quickly noticed a few nice features:

+ Ability to use SSML
+ Confgure Lex intents (as well as DTMF of course)
+ Lambda Element
+ Set callback number (for an outbound flow)
+ Dynamic TTS

I did Record my call as when i went through the main menu I also choose 8 (Set Recording Behavior). As mentioned at the start when you create your instance you set S3 as your storage location. All recordings are stored their and are encrypted with KMS. You cannot set the storage class within Connect but you can within with Bucket Management and apply Life-cycle management and replication etc…

Getting access to my call recording is via the Connect UI or I can use the AWS console/API and retrieve them that way.

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAA3nAAAAJDFlZjIyMzA5LWI4ODYtNDQ5MC1iYmU1LTIzNGU0MDM3ODExZg.png)


The playback is very basic, no wave forms, no speech detection, emotion detection, intent detection etc.. etc.. all this will come in time, the question will be via partners or Amazon.

 Having played with Connect for an hour I’m looking forward to understanding more about the product and how it integrates with Lex (maybe Alexa in the future?), Lambda, CRMs and Kinesis.

 Dan
