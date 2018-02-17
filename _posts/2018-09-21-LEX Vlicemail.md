---
layout: post
title:  "PROTOTYPE Redefining Voice Mail - Amazon Connect"
author: dan
categories: [ connect ]
tags: [ connect , voicemail, LEX, polly]
image: assets/images/connect.jpg
---
I was recently watching the AWS Loft event in London and I found myself somewhat over interested in Voice Mail... Voice Mail, yes Voice Mail! Why.... watch this quick clip to see if you can see the 4 benefits I've called out below (no cheating! :)

<iframe width="744" height="419" src="https://www.youtube.com/embed/ONosR-4Lc4I" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

[Need Sound]

The solution uses several Amazon/AWS Services:

+ Amazon Connect (Call Handling / Routing)
+ Amazon LEX (Natural Language Voice Bot)
+ AWS Lambda (Code execution service)
+ Amazon SNS (Simple Notification Service)

I'm sure there are several very good business reasons why your business uses VoiceMail and by using the above solution you can provide an effective Voice Mail service... but you get some additional benefits:

1. A natural experience for the caller, they feel assured by playing back the details in the confirmation
2. The conversation turned personal, LEX was able to use the callers Name that was captured
3. You get the DATA about the VoiceMail, your now able to data mine/trend analysis and understand why people are leaving voice mails and use that to help improve your business processes (VoiceMail is a costly service from a man power perspective)
4. You can use whatever type of notification service you choose (E-Mail, Text etc... )


I'd love to hear thoughts around things I've missed or additional ideas you can think of.


Kr
Dan


P.s, yes the Voices were from Polly :)
