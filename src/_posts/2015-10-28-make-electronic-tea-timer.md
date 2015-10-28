---
layout: post
title: Make an electronic tea timer
comments: true
---

Here is a project I'm running for several weeks. The objective was to make my
first *real thing*, with the help of an arduino. This thing is an *electronic
tea timer*.

<img src="{{site.baseurl}}/public/images/hourglass.jpg" class="" />

A what? Indeed it's simply a timer. But I think that the term *electronic tea
timer* is better, isn't it ;) When I'm brewing some tea, 9 times out of 10 I
forget the time limit for the infusion and end up with an undrinkable beverage.
So I wanted a simple timer with two buttons, a buzzer and a LED.
A button starts a 3 minute countdown, for green tea, and the other one starts a 5
minute countdown for black tea. At the end the whole thing makes plenty of
beeps and blinks until I puts it off. Something really simple, isn't it?
But I didn't want to use a whole arduino in this project, while a 0.60€ tiny
micro controller might do the trick.

So I would have to learn how to program the ATtiny micro controllers from Atmel.
Why those ones? Because they are close to the ATmega328, the one into the
arduino. And I already know some things about this chip.

First, I created a prototype of that *sound hourglass* with the arduino.
Just to be sure I knew how to do. The schematic could be something like that:

<img src="{{site.baseurl}}/public/images/proto-tea-timer.png" class="" />

Finally I use only one LED, but in the prototype there was two. Using this
prototype I soon realized that a single LED was enough.

Next step was to make the timer with an ATtiny45. Why this one precisely?
Because 1) I owned one and 2) there is a plethora of tutorials to program an
ATtiny45 using an arduino as a programmer. If you are not aware of the term,
**to program** a micro controller is more or less to transfer its program into its
memory
from a computer. For both sides to communicate, one need an interface called a
**programmer**. There is many ways to do this, I wanted to use an arduino as a
base programmer, to have nothing new to buy. You'll find a good tutorial here:
[Program an ATtiny44/45/84/85 with Arduino](http://www.instructables.com/id/Program-an-ATtiny44458485-with-Arduino/).

It was relatively easy to make a programmer for the ATtiny45 using an arduino:

<img src="{{site.baseurl}}/public/images/hello-world-attiny45.png" class="" />

As I was going to program a lot of micro controllers, I preferred make a shield.
First a temporary one:

<img src="{{site.baseurl}}/public/images/arduino-temp-shield.jpg" class="" />

Then a permanent:

<img src="{{site.baseurl}}/public/images/arduino-shield-attiny45.jpg" class="" />

I was too eager to make the shield, so I reversed the direction of the DIP
socket. That is why the wires are so long: I didn't want to desolder it. Anyway
it works fine ;)

So I was able to program an ATtiny45 (4K of ROM) using an arduino **AND** the
Arduino IDE. It was a good start, but it wasn't enough. First I didn't
want to use the Arduino IDE, for reproducibility and automation issues. And
then I was pretty sure that the code of my *tea timer* could fit into an
ATtiny13, who have only 1K of ROM, and is almost two times cheaper than an
ATtiny45.

To be continued…
