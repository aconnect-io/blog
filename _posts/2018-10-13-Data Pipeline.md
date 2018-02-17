---
layout: post
title:  "Data Pipeline"
author: dan
categories: [ connect ]
tags: [ connect , data, kenesis]
image: assets/images/connect.jpg
---
In 2011 Marc Andreessen wrote an article in the WSJ titled 'Why software is eating the world' and this is now evolving into Artificial Intelligence will eat software. AI is a hot topic right now with the experts, markets and society wrestling with what is means to many industries. Amazon have been using AI for over 20 years to drive their goal of being **_Earth's Most Customer Centric Company_**, and so it's no surprise that they have a range of AI services already that are being used for a vast array business services and even responsible for the creation of new companies. This article, however, is not to discuss the AI Services that Amazon offers for the Contact Centre. This article is about how Amazon Connect can help feed your companies data hunger which in-turn supports your company for its AI Adoption and data driven decision making.

For any company to put its customer first and provide a great customer experience you need data... and we're not just talking about the account specific data regarding the customer's use of your services, we're talking about the behaviors of your customers, what they like, what they don't like, their routines and needs, and how they use your services... the more personal the experiences you provide for your customer, the more likely they are to return/spend and advocate for your services. In order to provide these journeys you need to know as much as possible about your customer, especially when and how they interacted with your company.

### It's all about the data:
How many different ways can your customer interact with your company?

1, 2, 5, 10?

And of these ways, how many stream data to a place where your data communities can consume them in near real-time?

I'm sure the answers to these questions are very varied, we'll have some companies that do not collect the data centrally, others that process the data weekly/daily and some like LinkedIn who process the data in near real-time and provide personalized home pages based on their AI Algorithms and Machine Learning (Link). Imagine your own company and how you could use the data in your own AI Algorithms, if you're a Bank you'll be able to spot fraud with a higher degree of accuracy, reducing the POS frustrations or false positives, or a Telecoms company and its ability to provide more personalized services to the customer. The key here that spans across verticals is data, without having access to your own data you're not able to provide these improvements in customer experiences and capitalize on your customers' true worth.

### Any-channel?
Over the past few years we've seen an explosion of Voice Enabled devices from Amazon, Google, Microsoft and Apple. I'm not sure what we officially call this next wave of computing, Zero UI? Ambient Computing? VoiceFirst? one thing i'm certain on is that the Voice UI is here and here to stay. It doesn't satisfy all use cases and so it will complement the current range of customer channels, but certainly lowers the bar to entry and its ease of use it very natural. With another channel means another set of data to ingest and analyze and use to provide that personalized experienced. Amazon Connect provides that Alexa Experience within the Contact Centre via LEX, you're now able to understand your customers intent and that is very rich data!

### Measure your Data Pipeline?
Having the X many customer contact channels plus the Voice User Interfaces + internal and external systems, means if you don't have a data strategy you'll find it hard to really benefit from the data. I'm no data scientist, however I do think we could, and probably should, measure the data pipelines. What I mean by measuring your data pipeline is:

>**How long does it take from event to being actionable and relatable?**

For example, when your customer makes a purchase via the website, phones up to talk to your IVR, talks to an agent, accesses your Alexa Skill etc... how long does it take for the data created by those systems to be accessible by your AIs / data community and other support systems?

### Using Amazon Connect in your Data Strategy
Amazon is well regarded as a leader in using data to great effect and supports their drive to be Earth's Most Customer Centric Company. Part of that customer experience is managed by their Customer Service Centres for their brands such as Zappos, Audible and Amazon Retail. Their Customer Service Centres use an in-house built product called, Amazon Connect as the underlying call centre technology. Amazon Connect provides Telephony and IVR self service features to customers along with ChatBots. The platform is hosted on Amazon Web Services (AWS) which, as you'd expect, integrates nicely into the other AWS Services to provide a platform that will grow in features and functionality over time. On the data side Amazon Connect integrates into Amazon's real-time data streaming service called Kinesis. Once your data is in Kinesis you're then able to move and manipulate on that via a wide range of other AWS Services, along with providing that information to your AI Services.

### An Example Data Flow from Connect
I wouldn't feel right unless I was able to draw something to make it real for you.

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAprAAAAJGQyYTBhMGUxLTcyM2UtNDM3OS1hYTljLWYyMzg5ZmZlMzkzNQ.png)



What we have here is a data pipeline for Amazon Connect Contact Trace Records. This architecture has several benefits. At various stages of the journey for the data you're able to perform many different types of actions. Within Lambda for example you can split the data to multiple destinations, transform the data, supplement it and perform action such as send a text message / email or perform customer action (the possibilities are plentiful!) Once the data is in your Data Warehouse (S3 / Redshift) you're then able to run large scale analytics, join data from the different sources and feed other systems including your data community.

The exam question on measure?

>**For the solution we built it was taking around 2 minutes for the data to get from Connect into Redshift**

In our data pipeline we are also splitting the data within Lambda to feed DynamoDB. And some of the delay is being generated by Connect itself sending the data to Kinesis Streams. I'd not be surprised if this improves greatly over time as Connect matures.

### Data Strategy..
It'll come as no surprise that there are several ways to get the information from point A to point B. In the example above we use a particular pattern. Based on your requirements you might choose to do this:

![](https://media.licdn.com/mpr/mpr/AAIA_wDGAAAAAQAAAAAAAAuCAAAAJDlmNGJhYzEzLWJkYTgtNGU1Mi04YTYwLTZkZmE0YmMyYjFkMg.png)


From here you can then choose to use Amazon Athena to query the S3 files, or use Amazon Glue to move the data into a different database, or run Kinesis Analytics on the streaming data. You have many options and the devil is in the detail based on your use case. However, by using Amazon Connect you're able to integrate the data into your data pipeline and gain insight and business value with near real-time processing. The integration provided by Connect is likely to open up opportunities you've not yet considered or been able to act upon.

### Conclusion
By using Amazon Connect as your contact centre product, not only are you getting a product that offers great features, but one that also supports your data strategy.



Kr, Dan
