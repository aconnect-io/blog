---
layout: post
title:  "5 killer features that I hope to see in Amazon Connect"
author: dan
categories: [ connect ]
tags: [ connect , strategy ]
image: assets/images/amazon-connect-logo.png
featured: true
---
There is no doubt that Amazon Connect is on a trajectory to become a powerhouse in the contact centre space. In true Amazon style the product has been released in MVP (Minimum Viable Product) stages, which allows Amazon to test and learn, get customer feedback to help shape and drive the product backlog, after all they are on a Mission to be _**Earth's most customer centric company**_.

Connect is almost year old, being released on 28th March 2017 ([Amazon Release](https://aws.amazon.com/about-aws/whats-new/2017/03/introducing-amazon-connect/)) and in the last year Amazon have been building and releasing features that allow you to see how they are thinking about the product and the potential it has. Being released with what seemed to be a light feature set (A single API for example, no Voicemail), controls the use cases for Connect and allows for more focused development cycles. That said including the ability to make Lambda calls is a killer feature and takes Connect out of the walled garden and opens up the contact centre for extremely rich data integrations to allow for _**Personal, Natural and Dynamic**_ customer integrations.


> If you're new to Connect and would like to know more, checkout this very informative video by Amazon's Chris Bergin

<iframe width="140" height="79" src="https://www.youtube.com/embed/xOkcpF_4ZvI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

With such a good bedrock of a platform, what are the 5 killer features that I'd like to see in no particular order...


## Per Second Billing

AWS is well known for  [price cutting](https://aws.amazon.com/blogs/aws/category/price-reduction/) and Connect comes with a very transparent and easy to follow [pricing strategy](https://aws.amazon.com/connect/pricing/) with no set-up fees or monthly commitments, no per agent costs... BUT... AWS is a pioneer in the pay for what you use economy. From their very first service for storage S3 over a decade ago. Recently Amazon held true to this in big way by changing the Pricing of Ec2 (Servers) from Per Minute to [Per Second billing](https://aws.amazon.com/blogs/aws/new-per-second-billing-for-ec2-instances-and-ebs-volumes/).

Contact centres have always been on a Per minute model I believe Connect could get to per second, and this would be a significant cost saving for Companies.

## Alexa Integration

Amazon are [doubling down](https://www.cnet.com/news/amazon-fourth-quarter-results-2017-prime-holiday-alexa/) on Alexa and there is no secret that the whole voice eco-system has undergone a paradigm shift in the last few years. All the big tech companies are trying to impress with their voice experiences that wow and delight our every-day lives. Alexa is used everyday in our home to assist with Cooking, Homework, Home Automation & Entertainment and my youngest enjoys putting items on the shopping list, she's 4!

Amazon Connect when released also had integration with [LEX](https://aws.amazon.com/lex/) which is the Natural Language Understanding (NLU) engine that drives A**lex**a. Lex provides a chat bot experiences within Connect... Alexa style.

However today the only way to interact with Connect is via Telephony, this is both expensive and doesn't sit with Amazon's vision.

Developing on Alexa has synergies with Connect, in that they both integrate with AWS via Lambda and thus a well designed system can start to use the same logic, so you code once for both systems or at least share you work between the two. In addition to this you're able to [export your LEX bot into Alexa](https://aws.amazon.com/about-aws/whats-new/2017/09/export-your-amazon-lex-chatbot-to-the-alexa-skills-kit/)

> However, currently we cannot use Alexa to integrate with the ACD Features of Connect, in that we cannot speak with a real human.

Having this integration would need to be carefully considered but also a very natural progression. Let's assume you're traveling in your semi-autonomous vehicle and it breaks down, you ask Alexa to invoke your breakdown insurance, using the GPS of the car Alexa is able to tell the control centre where you are and advises that help with be with you in 30 minutes, you get text message with the confirmation & registration of the assigned support personnel. However you ask Alexa to speak with the control centre and she connects you to a human who has full context of your interaction and is able to quickly help you.

What a great experience that would be for the Customer AND Agent.

In addition to the customer experience, is the cost savings... as more and more people are turning to voice assistants having to switch to the PSTN is costly for the Customer and Business, using Alexa _**should**_ mean for that interaction only the Connect cost is applicable, and for household brands this will means savings of Millions per year.

## Voice Authentication

The balance between usability and security is an art and getting this wrong can make or break your business. When we call our bank today we are asked different questions to that of a mobile app (!in fact we are asked questions!, We just need to look at my iOS App). This level of complexity is outdated. It adds to Customer frustrations in addition to security failures which drives additional call volume, average handle time AND agent pressure.

Slowly we are seeing improvement in Voice biometrics and [Pindrop did a demo on stage](https://www.forbes.com/sites/alexkonrad/2018/01/25/pindrop-passport-looks-to-power-the-voice-economy/#2e69ec5f4319) whereby the CIO of Pindrop, Vijay Balasubramaniyan, made a purchase and then his colleague tried to do the same transaction but 'alexa' denied the request.

Pindrop have a solution for Connect which is currently in [Preview](hhttps://aws.amazon.com/quickstart/connect/pindrop/).

Current solutions provide a 'risk score' using 1000+ different indicators that the IVR and/or Agent can use to Authenticate the customer. As this improves over the years with solutions like [Passport](https://www.pindrop.com/solutions/authentication/) this will reduce inbound phone fraud and customer frustrations... will we get to 100% confidence on 95%+ of interactions?



## Global resilience


Designing enterprise scale systems is hard, building them in your own Data Centres is very hard and in today's world it doesn't differentiate yourself from the competition. Using a Cloud Computing solutions like AWS, G-Cloud and Azure gives you incredible amount of options to get it right (and wrong!)

Enter Werner and this instant classic:

![Everything fails all the time](/blog/assets/images/5-killer-1.jpg)

Amazon Connect is 'server-less' in that you have no servers to manage, patch or ensure they are up and working. Amazon do all that heavy lifting for you! and they do that all within a Region.

A Region is a Geo-graphic location such as London / Paris / Oregon and these Regions have Availability Zones  (AZs) and AZ = A Data Centre... so a Region is highly available and thus so is Amazon Connect.

> Learn more by reading this amazing post by Amazon's Adrian Hornsby, [The quest for availability.](https://hackernoon.com/the-quest-for-availability-771fa8a94a7c)

However... the bar is always rising and so we need to plan for failure of a Region. Amazon have been releasing some features to support this in stages over the last few months but right now its very manual.

I hope Amazon are working towards the goal of seamless synchronization between regions. This is not such a crazy ask, as AWS have been raising the bar on their flagship DynamoDB solution that now supports [Global Tables](https://aws.amazon.com/blogs/aws/new-for-amazon-dynamodb-global-tables-and-on-demand-backup/).


## The App economy

Amazon have already started to release [quick starts](https://aws.amazon.com/quickstart/connect/) which I've talked about before [here](https://aconnect.io/blog/connect/2017/11/13/Quick-Starts.html).

Getting this right is going to commoditize the contact centre which has been going through a slow and painful transition over the last few years. I'm sure there is already a huge amount of work on the table for Amazon and this one will get allot more love and attention in the coming months/years.


****

Amazon Connect is well poised to disrupt, but Contact Centres are a mesh of complex processes, people and technologies, yes 'voice' is on the decline and has been for many years, this is being replaced by increasing customer demands and with Connect, AWS and its partners, are well poised to be a key enabler in any companies strategy.

Please feel free to get in-touch or leave a comment below!

Thanks
