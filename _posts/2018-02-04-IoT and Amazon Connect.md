---
layout: post
title:  "IoT and Amazon Connect"
author: dan
categories: [ connect ]
tags: [ connect , project ]
image: assets/images/amazon-connect-logo.png
---
Amazon Connect is another building block in the AWS Eco System and in this blog we look at how we link the Amazon IoT Button to drive Amazon Connect...

Why... I hear you say... well, there are going to be many use cases where this will be valuable and many more that yours truly cannot think of. In this Article we look at how we could us this for an in home personal alarm.


### Building a _Demonstration_ Personal Alarm System
The personal alarm, is a device that is used within the home and is well suited for vulnerable people. By pressing a button a call is made over the phone network to a control center where checks are made to understand false positives and call for home visit if required.

However as it's AWS we don't play by the normal rules and we up the ante a-little. Our Set-up looks like this:

![Reference Architecture ]({{ "/blog/assets/images/IoT-Connect.png" | absolute_url }})

The IoT button when pressed calls Lambda Function, this then uses the Connect APIs to make a call to the users' phone number. Connect can then ask the caller if they are ok and press 1 to confirm. Should their be no answer or no button presses then the control centre would need to interject and carry out their response plans.

### What are the Benefits?
By using this system over current systems we may have some benefits for the Consumer and the Supplier, however as this is a demo only, these would need further considerations to weigh up the Pros and Cons of using the technology in this way.

+ \+ No landline needed
+ \+ IoT button good for 2000 clicks
+ \- Requires Wifi
+ \+ Auto Outbound Call
+ \+ Outbound Call with IVR
+ \+ Fully Serverless, Pay as you Use. (reduce suppiler costs = lower costs for customer)

**Bonus:** What if you both had an Alexa Device and you could also 'drop in' on your loved one and make sure everything is ok!

### See a button in action

<iframe width="744" height="419" src="https://www.youtube.com/embed/iwdojaGS49I" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
