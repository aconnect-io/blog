---
layout: post
title:  "Amazon Connect + Serverless = ❤"
author: dan
categories: [ connect ]
tags: [ connect , serverless, dynamoDB ]
image: assets/images/amazon-connect-logo.png
---

In this post we are going to be looking at the Contact Control Panel (CCP aka, the Softphone), Connect Steams API and how we build a fully Serverless Contact Centre solution, to say I am excited and impressed is an understatement. I've always loved building things right from an early age (Meccano!) and during the past 10 years it's likely that I've spent 80% + of my effort on building the part of the iceberg that no-one sees and thus only providing 20% of my time on business value, but with AWS and Amazon Connect that is totally flipped on its head (and some more)

**TL:DR** Embedding CCP into your WebApp via iFrame, using Connect Streams API to then connect your App to Connect via CCP, Hosting Website on S3 and using DynamoDB JavaScript SDK (Via VPC Endpoint!) for CRM Data = A contact centre solution with Agent Front-End, fully Serverless, effortless Scalability and rapid development. Here is a working prototype as GIF:


![](https://s3.amazonaws.com/aconnect.guru/aConnect%20GIF.gif)


In Part 1 we explored the CCP UI (On the left of the above image), CCP is hosted in its own Frame (Web Browser Window) however you have the ability to embed this within your WebApp via iFrame

    // This is the API files from https://github.com/aws/amazon-connect-streams
    ﻿<script src="amazon-connect-v1.2.0.js" type="text/javascript"></script>

    // You must set a div with the id of 'containerDiv'. Y﻿ou don't have
    // ﻿to make it visiable if you have embeded your own Controls
          <div style="height:465px;width:320px" id="containerDiv">
    </div>

    // The below script passes your URL into the Connect Streams API that
    // ﻿generates the iFrame.﻿
    <script>
    ﻿connect.core.initCCP(containerDiv,
    {ccpUrl:"https://INSTANCE-NAME.awsapps.com/connect/ccp#/",
    loginPopup:false,
    softphone:{allowFramedSoftphone:true}
    });
    </script>

    // NOTE: You need to enable your Application URL within Connect's
    //﻿ Application Integration﻿ menu see 'whitelisting' on the github repo

    // This is all within your HTML file, the order of the scripts matter﻿
﻿
Once you have the iFrame embedded and the amazon-connect-vX.Y.Z.js file loaded within your HTML page then you can start to work with the Streams API. The github highlevel architecture documentation provides this very useful reference image:

![](https://s3.amazonaws.com/aconnect.guru/aConnect%20GIF.gif)


What you can see from this is that the Phone/CCP is mandatory to tunnel the connections back to Connect and thus you need to have CCP working even if your not going to display the UI.

Amazon have done a reasonable job in documenting the API guide on github, I'm being critical as its not written for a new starter and so you won't find a step by step guide to get you up and going. I hope to get time and do a Pull Request for some demo files for new starters.

I've tried to use most of the key features of CCP in my Prototype as you can see here in more detail:

![](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAA1GAAAAJGM5NmVmNmE0LTZhMjAtNDA3NS04YTc0LTFjNjYyNDFmOTBjOQ.png)




1 - This is embedding of the CCP UI as detailed above.

2 - We have several features here. The **Hello Daniel**, code is using the Agent events to pull the name of the logged in user, **Security PASS**, is driven off of a Connect variable, if PASS = Green, if FAIL = RED. The sample buttons are **CALL BOB**, which when pressed will dial a fixed number that i coded, and **Set to Available**, will move the agent from a NonRoutable state to a Routable state and finally we have **Agent State = BUSY**, this is just pulling the agents current state. So if we look at this technically we have, read from agent profile, using a variable to drive UI, using UI to dial out from the phone, using UI to change state and finally reading from current state. There are probably more scenarios but based on this I could easier build my WebApp to not require the CCP UI.

    // HTML Code for Hello Daniel
    <h2><p id="name">Please login</p></h2>

    // Script code for Hello Daniel
    connect.agent(function(agent) {
      console.log("get agent name");
      var name = agent.getName();
      name = ("Hello " + name + ", how are you today?");
      console.log(name);
      document.getElementById("name").innerHTML = name;
    });
    // HTML Code for Call Bob (With thanks to Joe-aws from the Forums
    <button type="button" onclick="bob()">Call Bob</button>﻿

    // Script Code for Call Bob (With thanks to Joe-aws from the Forums
    function bob() {
      connect.agent(function(agent) {
        var myEndPoint = connect.Endpoint.byPhoneNumber("+12345678901");
        agent.connect(myEndPoint, {

          success: function() {
            alert('success');
          },
          failure: function() {
            alert('error');
          }
        });
      });
    };
﻿﻿


3 - Here we get a little outside of the scope of Connect, but with this section it completes what could be a very valid business case using Connect and Serverless. At the top we have **CRM Box** and at the bottom we have an external API to google MAPS. The CRM Box, is driven when the Contact arrives, it uses Variables passed from Connect to CCP, we query those variables within our WebApp, and then use them to Query DynamoDB and return the full account information. I've said it before but 3rd time lucky... **this is the WebApp making the DynamoDB call!** I'm so excited by this, can you tell :) The **Google Maps** call is again driven from the Variables provided by Connect via CCP and the Contact Event Stream. This was to help you peak into what else you can do with your own WebApp driven off of Connect

    // HTML for Google Maps
    <p id="maps">
    <iframe width="150" height="150" frameborder="0" style="border:0"></iframe></P>
    // Script for Google Maps
    connect.contact(function(contact) {
      console.log("Maps API, Get Attribute");
       refresh()
      var Location = contact.getAttributes().Location.value;
      console.log(Location);
      var maps = ("<iframe width='150' height='150' frameborder='0' style='border:0' src='https://www.google.com/maps/embed/v1/place?key=YOURKEYHERE=" + Location + "' allowfullscreen></iframe>");
      console.log("Maps url is " + maps);
      document.getElementById("maps").innerHTML = maps;
      });

    // Yes the eagle eyed person will have spotted that I don't need the iFrame
    // ﻿in the HTML, this is a prototype and I wanted the the UI stay quickly
    // look and feel the same with a map present or not﻿


I've had loads of fun building this, and I'm just blown away by how much can be created in a short space of time. Don't get me wrong its not as easy as click, click done, there are DynamoDB database designs to consider, security, contact flows, UI, data movements etc. etc. but to get a POC up and running :) then using Amazon Connect with 'Serverless' (S3 + Lambda + DynamoDB) is just phenomenal!



### Tidbits:

+ I used the very new (16th Aug 2017) DyanmoDB VPC Endpoint https://aws.amazon.com/blogs/aws/new-vpc-endpoints-for-dynamodb/
+ When setting your DynamoDB Endpoint you use the URL like this endpoint: 'https://dynamodb.us-east-1.amazonaws.com',
+ CCP requires HTTPS, it will load in HTTP and you'll get call arrival, but media will not work unless its HTTPS
+ The order/location of your scripts matter for CCP

Thanks!
