---
layout: post
mathjax: true
title: CharIoTeer, Smart Last-Mile Delivery Project @MakeZurich
date: 2018-08-05 16:02
tags: ethz projects code hardware
categories:
description: |
    In this post, I will tell you about an IoT device me and my team prototyped at MakeZurich week-long Makerdays. Keep reading if you are a maker, IoT enthusiast or a person interested in using IoT principles in a real world scenario.
---

<!-- Need image here! -->
<div class="img_row" style = "width: 100%;">
  <img class="col three" src="{{ site.baseurl }}/img/mkzh/network.png" alt="" title="LoRaWAN"/>
</div>
<div class="col three caption">
The overview picture of operation of LoRaWAN network ([source](https://www.thethingsnetwork.org))
</div>

In this post, I will tell you about an exciting [IoT](https://en.wikipedia.org/wiki/Internet_of_things) device me and my team prototyped at [MakeZurich week-long makerdays](https://makezurich.ch/). Keep reading if you are a maker, IoT enthusiast or a person interested in using IoT principles in a real world scenario.

## MakeZurich

MakeZurich is the "Civic Tech and LoRaWAN Hackdays for a better city". It is organized jointly with the city administration to explore new ways of solving challenges the city is facing with the help of open networks and civic tech. I missed the first run, that took place last year, because I found out about the event too late. This year, I had it in my calendar and was ready to take part. The event had a smell of a hackathon: difficult and open-ended challenges to be tackled in innovative fashion in too little time in small teams, mostly with people you didn't know before the kickoff. But it was more than that. Rather than hackathon,it were Makerdays or Hackdays. It lasted for full 8 days, and on each day a makerspace was open so that I could just drop by, ask people about technical issues I was having and hack on the prototype and code for our project. In retrospect, I view the event as great learning experience that gave me quick insight into the field of IoT and LoRaWAN. (Big thanks to the organizers for all their work, it showed!)

## LoRaWAN

LoRa what? Myself, I didn't know anything about the [Long Range Wide Area Network](https://www.thethingsnetwork.org/docs/lorawan/) until about one week before the event, but I came to understand that it is a very interesting player in the landscape of wireless communication technologies. It is designed to allow low-powered devices to communicate with Internet-connected applications over long range wirelessly. It is well suited for applications with very low bandwidth, something up to 400 bytes/hour, where individual message should not exceed 12 bytes.

The following picture will give you an idea how a device (node) communicates with internet application via LoRaWAN:

<div class="img_row" style = "width: 100%;">
  <img class="col three" src="{{ site.baseurl }}/img/mkzh/lorawan.png" alt="" title="LoRaWAN"/>
</div>
<div class="col three caption">
The overview picture of operation of device using LoRaWAN
</div>

As you see, the communication is handed over to an internet protocol once the message was received by a gateway. LoRa, being long range technology, enables each device to emit messages to the distance of about 20+km in rural and about 2-5km in urban settings. Whether a message is successfully received and passed to an application depends on whether there is a gateway present in that range that is ready to receive.

All this is nice but it becomes practically very powerful thanks to [*The Things Network* (TTN)](https://www.thethingsnetwork.org/) initiative that implements an [open source backend](https://account.thethingsnetwork.org/users/login) that handles messaging between nodes and applications and that is available for anyone to use. Even more interestingly, the gateways, intermediary infrastructure for The Things Network, are mostly deployed by the users themselves. This is possible because they are cheap (~250 Eur), small, simple, and can serve many nodes in large area.

If this sounds too good to be true, check the map of coverage of Zurich below. What this means, is that I can drop my LoRa capable sensor node anywhere in the large area of Zurich and have it send me measurements to my application without having to even think about the infrastructure. Cool isn't it? (It is possible thanks to the [ZH TTN community](https://www.thethingsnetwork.org/community/zurich/) which is very active. Hat tip to them!)

<div class="img_row" style = "width: 80%;">
  <img class="col three" src="{{ site.baseurl }}/img/mkzh/zhcoverage.png" alt="" title="Zurich Coverage"/>
</div>
<div class="col three caption">
The Things Network LoRaWAN coverage in Zurich
</div>

The devices and gateways operate in unlicensed spectrum of 868Mhz (Europe), meaning that anyone who wants to can deploy his own LoRaWAN network. The Things Network currently supports *Class A* device type, which means that each device can send a message to gateway at any time, but it can receive a response only at predefined intervals after sending.

Some of the [limitations](https://www.thethingsnetwork.org/docs/lorawan/limitations.html) of a LoRaWAN network include the restricted payload size and narrow bandwidth. Additionally, the TTN mandates fair usage policy with 30 seconds of airtime per day (this translates to about 20-500 messages per day, depending on message's payload and bandwidth) and only 10 messages to the device from application per day (aka downlink messages).

If you want to dig deeper into how LoRaWAN and The Things Network work, visit the highly readable [documentation of TTN](https://www.thethingsnetwork.org/docs/).

## The Challenge

The MakeZurich Makerdays revolved around 7 challenges that were crafted with the participation of the city administration (you can see all of them [here](https://speakerdeck.com/gonzalocasas/make-zurich-vol-ii-kick-off)). These are real-world challenges that the city is facing and that it is seeking solutions for. Our team, made up of an internet entrepreneur, project manager, data scientist and me, chose to work on a challenge termed "Conquering The Last Mile". We were working closely with a Swiss company providing logistic services, mainly last-mile bicycle package delivery, in many cities in Switzerland.


<div class="img_row" style = "width: 70%;">
  <img class="col three" src="{{ site.baseurl }}/img/mkzh/meonbike.jpg" alt="" title="Me On Bike"/>
</div>
<div class="col three caption">
Me doing a test drive on a last-mile delivery cargo bike.  
</div>

During MakeZurich, we focused on particular problem of deliveries of packages containing sensitive biological material, for example between pharmacies and hospitals. In such scenario, it is crucial to monitor, among others, the temperature of the package contents to be able to prove that the material has stayed in required temperature range throughout the time of the delivery. Further, one can think of scenario when the deliveries are rescheduled on the fly depending on location of other drivers, their availability and the predicted time when the sensitive delivery will go stale.

Solutions to temperature monitoring of sensitive mobile packages exist, but they require the personnel of the pharmacy to always put a single-use device in the package before it is sealed. This is time consuming, error prone and unnecessarily costly.

## The Prototype

Each group received a "challenge box" with some hardware that was potentially useful for work on the challenge. In the week we had to work on a prototype, I hacked together an Arduino based device that simultaneously measures temperature inside and outside of the package, humidity, package orientation and its geographical location, mostly using this hardware. I especially enjoyed writing C++ code for data collection, processing and messaging on the microcontroller and I had great fun brushing up my soldering and 3D printing skills.

<div class="img_row">
	<img class="col two" src="{{ site.baseurl }}/img/mkzh/hw2.jpg">
	<img class="col one" src="{{ site.baseurl }}/img/mkzh/hw1.jpg">
</div>
<div class="col three caption">
The prototype of a device that makes last-mile delivery smart
</div>


### Talking with The Things Network

Previously, I wrote about the limitations on payload size imposed by the LoRa or TTN.  In practice, this means, one has to think a bit about what information needs to be transmitted and how often. Sending data as plain text or `JSON` is a no-go, therefore I encoded the messages as bytes. The message is then decoded in the online application using reverse of operations that were used for encoding. Let's look at an example for the GPS data:

#### Encoder

{% gist e42e59461f7847fc9e5eac06caeac098 add_buffer_gps.cpp %}

#### Decoder

{% gist e42e59461f7847fc9e5eac06caeac098 decode_gps.js %}

#### Sending the Payload

Once we have a way to to encode and interpret the data, we can start sending some measurements. Thanks to the `TheThingsNetwork` library, this is fairly simple. Here is a bare-bones example:

{% gist e42e59461f7847fc9e5eac06caeac098 ttn_example.cpp %}

#### Received Data

As a result, our application will receive a message from the device (node) enriched by metadata provided by the gateway(s) that picked up the message. Below is an example of a datapoint:

{% gist e42e59461f7847fc9e5eac06caeac098 datapoint.json %}

### Visualizing the Data

Once the data was received by the application, it can be fed into visualizations, machine learning application or stored in a database. Here is a [website](https://ttn-milesahead.herokuapp.com/) (set up by [@njam](https://github.com/njam)) that visualizes the measurement points on a map, color-coded by the temperature as measured by the in-package sensor.

<div class="img_row" style = "width: 80%;">
  <a href="https://ttn-milesahead.herokuapp.com/"><img class="col three" src="{{ site.baseurl }}/img/mkzh/vis.png" alt="" title="Visualization App"/></a>
</div>
<div class="col three caption">
Visualization of temperature data together with their GPS location
</div>

### Printing the Case

I wanted to have a nice casing for the project to work as tight protective enclosure and to make it all together look neat. To design the case (starting from a [template](https://www.thingiverse.com/thing:78032)) I used [OpenSCAD](http://www.openscad.org/). I sliced the `stl` files to `gcode` using [CURA](https://ultimaker.com/en/products/ultimaker-cura-software) and printed them on a 3D printer from [Teil3](https://www.teil3.ch/shop/3d-drucker.html) (it worked perfectly, respect to them).

<div class="img_row" style = "width: 80%;">
  <img class="col three" src="{{ site.baseurl }}/img/mkzh/hw_scad.png" alt="" title="HW in SCAD"/>
</div>
<div class="col three caption">
Design of the simple casing
</div>

### Test Drive

Once the prototype was ready, we did some test rides with temperature critical items and collected real world data.

<div class="img_row">
	<img class="col two" src="{{ site.baseurl }}/img/mkzh/beer_box.png" alt="" title="Me On Bike"/>
	<img class="col one" src="{{ site.baseurl }}/img/mkzh/driver.jpg" alt="" title="Driver"/>
</div>
<div class="col three caption">
Collecting data in the wide open
</div>


## Conclusion

During MakeZurich our team prototyped a microcontroller based device that can make last-mile delivery smarter. We call it CharIoTeer. In just one week, we came up with fully functioning prototype that is portable and communicates its measurements over LoRa and The Things Network. For me, the project was great opportunity to work hard, have fun and quickly pick up practical skills in LoRaWAN and electronics prototyping, mainly by interacting with other people and asking lot of questions. I am excited about digging deeper into the domain of IoT, with focus on Industrial IoT and machine to machine communication. What about implementing IoT paradigm in a biology lab to achieve unparalleled throughput, big data harvesting, end-to-end process control and automate decision making? Sounds both feasible and fun to me:)

---
## Resources

You will find the full source code, design files and additional description and advice at [the project's repository on GitHub](https://github.com/martinholub/mkzh-charioteer)

## References

- [Teil3 - 3D Printers](https://www.teil3.ch/index.html)
- [The Things Network Uno](https://www.thethingsnetwork.org/docs/devices/uno/)
- [TTN Documentation](https://www.thethingsnetwork.org/docs/)
- [Zurich TTN Community](https://www.thethingsnetwork.org/community/zurich/)
