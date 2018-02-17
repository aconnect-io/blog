---
layout: post
title:  "Amazon Connects' Quick-Start packages could be the start of an 'App' eco-system for Contact Centers"
author: dan
categories: [ connect ]
tags: [ connect ]
image: assets/images/post-quick-1.png
---

In middle of last week Amazon Connect changed gears and is starting to demonstrate just how disruptive the technology is going to be, by enabling 3rd party integrations to be deployed via push button templates.

Amazon Web Services has an approach called 'Quick-Start' this approach uses pre-defined solutions that AWS Customers can run within their own accounts with a push button approach, and Amazon announced a few solutions that have been made available for Amazon Connect:

![Reference Architecture ]({{ "/blog/assets/images/post-quick-1.png" | absolute_url }})

These 5 are going to be just the start of what I feel will be many many more. Whilst the quick-start approach is not new, it's certain to be new to the enterprise contact center space and when you stop and consider what's happening here, you can really start to see how Amazon Connect is going to differentiate itself in a busy CCaaS Market.

### What is a 'Quick-start'...

Best said by Amazon..

>Quick Starts are built by AWS solutions architects and partners to help you deploy popular solutions on AWS, based on AWS best practices for security and high availability.

What you actually get a text file, this file is called a CloudFormation Template and it has all the information within, that is required to build the solution. When running the Cloud Formation Template within your AWS Account, it's highly likely that you'll be asked to input some information that is unique to your instillation.

For example, the Pindrop installation is going to ask for your API Key, other installations will ask for more, it depends on the solution being built. Once you input what you need, the script can run and all the infrastructure is built for the solution you need.

### How quick is quick...
Building the infrastructure for these 5 quick-starts will take minutes with the exception of the 'Amazon Connect' one which will take a-little longer as it's building a Redshift cluster, which is an Enterprise Data Warehouse product.

#### But...

Once these are built there is still configuration and integrations to be designed and completed.

For Example, let's assume your using a Voice Analytics API, you get an API Key, run the Quick-start and your ready to use it. You still need to configure Amazon Connect to consume the service within the Contact Flows. This will always need to happen and trying to automate this is likely a challenge never to be won as there are just too many use cases.

### What is the value...
By being able to utilize and build upon the power of AWS, Amazon Connect is able to provide benefits to the customers like never seen before in the CCaaS arena.

+ **Push button deployment for 3rd party integrations. (Caveat, planning and post installation configuration is still required)**

This means your barrier to entry is lower to try market leading products, long sales cycles are greatly reduced as you will be able to switch to another provider as you see fit (unless of course you signed a long contract)

+ **Pay as you use pricing model becomes closer to reality**

Depending on the 3rd party integration you'll use, it's likely many will offer a pay per use model, especially the API companies and as the majority of the solutions will be using 'server-less' technology, this means you don't pay anything when you're not using it.

The pay as you use model means you'll be able to track the cost for each contact should you wish to (though this would require good planning !)

Multi-year contracts, with high on-boarding costs will be the abnormal, providing you with you 'type 2' decisions.

+ **Right solution for the right job**

Choose the right product for the right job, have 2 or 3! I'd never advocate for over complexity, however you may need X solution for 80% of your contacts and Y solution for the other 20%, then you can make that happen (Similarly should Deptartment A want it and willing to pay, maybe now they can)

Likewise, if you only want to do high touch Voice Analytics on high value calls, then by tagging this in Connect, you can use you premium 3rd party solutions for only what you need.

+ **Test and Learn / Proof of Concepts**

By using Quick-Start packages you'll be able to test out market leading services within a shorter space of time than ever before. You'll be able to learn what products and services work best for you and use those in your production environment.

For large enterprises, with relatively little cost you can create meaningful Proof of Concepts, which reduces your risk of migrating workloads.


+ **Server-less for the most part**

Amazon will drive Technology Partners to use Server-Less technology as best as they can (my take!). Reason for this is that it fits in with the Amazon Connect model of being able to scale on-demand, no servers to patch/manage which means low operational overheads.

### The Architecture...

What might not be perfectly clear here is that these 'quick-start' services, in most part, are going to be SaaS offerings, that's great, we all love SaaS, as a result what is actually deployed in your AWS Account is a gateway service to the 3rd parties' service. This means the architecture for these solutions, as shown from the Amazon Connect site, is over the Internet

![Reference Architecture ]({{ "/blog/assets/images/post-quick-2.png" | absolute_url }})

This is not new, but may require some hearts and minds to shift.


### What needs to improve

These quick-starts will be based on proven technology patterns and security best practices, they remove a good amount of heavy and provide standard supported patterns. In future versions I'd expect they will start to include operational excellence features, like monitoring, troubleshooting, service alerting and maybe SLAs? The great thing about using Cloud Formation is that should the code get updated to add, say Cloud Watch Alarms (To alert of errors) you simply update the current Code, AWS knows what's changed and only updates that portion.

I'm sure their are more items that can be added and evolve as this deployment service evolves.

***

The 'APP' style eco-system is very much in its infancy, I have no knowledge weather this will develop further, it is my belief that this will mature and evolve over the coming years to automate even more of the manual effort required to integrate these systems.

Thanks, Dan
