---
layout: post
title:  "Amazon Comprehend & Amazon Transcribe... how could you use with Amazon Connect - Part 1 of 2"
author: dan
categories: [ connect ]
tags: [ connect , comprehend, APIs]
image: assets/images/Title-Comprehend-Pipeline.png
---
Last month at the annual AWS Re:Invent in Vegas a sleuth of announcements were made within the AI / Machine Learning arena... 2 of those announcements will further lay groundwork for Amazon Connect in becoming a serious competitor within the enterprise CCaaS space, and shows Amazon's intent in signing large enterprises' workloads onto AWS.

**Introducing:** Amazon Comprehend API & Amazon Transcribe API


Amazon Comprehend

>*is a natural language processing (NLP) service that uses machine learning to find insights and relationships in text. Amazon Comprehend identifies the language of the text; extracts key phrases, places, people, brands, or events; understands how positive or negative the text is; and automatically organizes a collection of text files by topic.*

Amazon Transcribe

>*is an automatic speech recognition (ASR) service that makes it easy for developers to add speech to text capability to their applications. Using the Amazon Transcribe API, you can analyze audio files stored in Amazon S3 and have the service return a text file of the transcribed speech.*

So for layman like me, and related to the Contact Centre you can...

![Reference Architecture ]({{ "/blog/assets/images/post-comprehend-4.jpg" | absolute_url }})

Note: The API uses are not limited to the CCaaS use case, any text can be used.

In this first post we'll look at the **Comprehend API** for the sole reason in that Transcribe is still in preview and yours truly doesn't have access yet :( (Hint hint Amazon :)

### Comprehend API

Comprehend comes with 5 Methods.

1 - Topics

2 - Dominant Language

3 - Entities

4 - Key Phrases

5 - Detect Sentiment

The first Method is different to the others, this is used for large file analysis on detecting topics... this is less relevant to CCaaS and thus if you want to know more, go here. The other 4 are part of the NLP suite and come in both single and batch API Methods.

**Dominant Language:** Provides the API some text and it will reply with the language being used, as of writing today (27/12/17) there are 100 languages listed.

![Reference Architecture ]({{ "/blog/assets/images/post-comprehend-1.png" | absolute_url }})

Entities: This is able to pull out from the text key items of interest such as DATES | PERSON | ORGANISATION | LOCATION [full list here](http://docs.aws.amazon.com/comprehend/latest/dg/how-entities.html?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3B7w%2FdiVevSMq4Cc9ZnbfIFw%3D%3D)

![Reference Architecture ]({{ "/blog/assets/images/post-comprehend-2.png" | absolute_url }})

**Key Phrases:** By using this method you're able to pull out key phrases within the text. This can be useful for finding feedback loops as to why the customer couldn't self service, checking your business processes, improve customer experience and many many more examples that are likely yet to be known.

![Reference Architecture ]({{ "/blog/assets/images/post-comprehend-3.png" | absolute_url }})

**Detect Sentiment:** This Method will analyze the whole context of the text and provide a sentiment score for Negative, Neutral, Positive or Mixed. It also provides the Dominant Sentiment in the reply. As this one is fairly easy to demo, we take a deeper look below.

### Deeper look at the DETECT SENTIMENT Methods:
Here is an example from Twitter where i used the Twython API to pull back some tweets for a Airline company. In the results you can see:

DATE, TWEET, SENTIMENT *{Negative / Neutral / Positive / Mixed}*

    Response
    [
    "Wed Dec 27 17:36:50 +0000 2017,@*** once again I'm disappointed by the farce of a service provided to me. I'm at Nairobi airport pls get in touch asap,NEGATIVE",
    "Wed Dec 27 17:35:28 +0000 2017,@*** See my other tweets, or indeed my email that unfortunately went without response,NEGATIVE",
    "Wed Dec 27 17:34:29 +0000 2017,@*** They tell me it’s because I got the ticket through you!!! @qatarairways,NEUTRAL",
    "Wed Dec 27 17:33:02 +0000 2017,@*** But @qatarairways  told me if I have to speak to you!!,NEUTRAL",
    "Wed Dec 27 17:32:53 +0000 2017,@*** wow, the self bag drop is just fantastic!  Only been waiting 25 minutes so far #blatentcostcuttingexercise,POSITIVE",
    "Wed Dec 27 17:32:25 +0000 2017,@*** #CityBagsLuggage are letting you down. They also ignore emails and the telephone. Seems that lots of other frustrated customers have had the same problems. Lots of terrible reviews of #CityBagsLuggage on Google and Twitter.,NEGATIVE",
    "Wed Dec 27 17:31:44 +0000 2017,@*** No it’s a problem with a return flight booking. This is the message I keep getting. Please send details so we can deal with this privately. https://t.co/V0eUA1LyhL,NEUTRAL",
    "Wed Dec 27 17:31:27 +0000 2017,@*** Hi Alex the flight was Short-haul from Heathrow. https://t.co/EiZp4Kh7q4,NEUTRAL",
    "Wed Dec 27 17:29:07 +0000 2017,@*** Done Thanks👌👌,NEUTRAL",
    "Wed Dec 27 17:28:59 +0000 2017,@*** I sent you two DMs and nobody is replying to me. Your website does not allow me to file a complaint. What is going on? #customerrightsviolated #nonsense,NEUTRAL",
    "Wed Dec 27 17:27:18 +0000 2017,@*** Not to worry, I will include a screen shot of the flight i'm referring to on my complaint email to HQ.,NEUTRAL",
    "Wed Dec 27 17:26:55 +0000 2017,@*** DM sent with all the information you requested. Thanks for the prompt response and look forward to hearing from you soon.,NEUTRAL",
    "Wed Dec 27 17:26:02 +0000 2017,@*** Nice bit of attitude to a customer.My Nov query was re: the route, today I refer to BA flight actually being sold online.,NEUTRAL",
    "Wed Dec 27 17:25:19 +0000 2017,@*** Thank you....landed :),POSITIVE",
    "Wed Dec 27 17:25:00 +0000 2017,@*** Yes I have and they say in their own sites the flight is not available at that price, that it is a mistake of the website but I feel misleaded and tricked into buying a more expensive flight. If the flight is advertised at that price I should be able to buy it.,NEGATIVE"
]```

I chose an airline as they always have feedback on twitter and would be a good example for a real use-case for Comprehend. The script to do this took just over 1 second (1053ms) and that included going to Twitter, getting the latest tweets, storing it in my Python code, and then one by one going to Comprehend to get the Sentiment and storing the results in S3.

A few of the results are interesting...

>*"wow, the self bag drop is just fantastic! Only been waiting 25 minutes so far #blatentcostcuttingexercise, POSITIVE "

^ So it seems Comprehend cannot quite yet recognize sarcasm.. and that's something us brits are very good at.

```Done Thanks👌👌, NEUTRAL"```

^ This one is likely to be a very common reply in the world of messaging, In my view this should have been POSITIVE. I'm sure it's only a matter of time before Amazon train the machine learning capabilities to understand emoji's. (The same happens with #hastags, the word is not used/valued in the analysis it seems from the limited testing i did)

Found this during testing one, I agree on the MIXED Sentiment:

```"@*** We got in eventually so all good. Just a shame it was a B-gate and then not enough passport scanners open. Flight was good though.,MIXED",```

**It's not all so definitive....**

The Sentiment response is only the dominant sentiment... with the API reply you don't just get the dominant answer, you get the scores also... so you can make up your own determination and use the data as you see fit.

```"Sentiment": "POSITIVE",
    "SentimentScore": {
        "Mixed": 0.05284206196665764,
        "Negative": 0.011428894475102425,
        "Neutral": 0.02409430593252182,
        "Positive": 0.9116346836090088
    }
```

### Costs:

For the official pricing go here. Using the example, for 10,000 tweets you're looking at $3 (Topic Modelling is charged differently, see the [link](https://aws.amazon.com/comprehend/pricing/?lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3B7w%2FdiVevSMq4Cc9ZnbfIFw%3D%3D) for official pricing)

### That's all for now....

Working with the Comprehend API is straight forward and the documentation is excellant, both on the business use cases of the API and the technical implementation. As this is 'aaS' and driven by Amazon's Machine Learning technologies, the accuracy and performance will only get better over time and you have to do nothing to take advantage of that. It's going to be interesting to see what companies will build with this.

Hopefully, access to the Transcribe API will be approved soon(ish) so we can take a look at the Transcribe API.

Thanks

Dan
