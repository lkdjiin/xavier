---
layout: post
title: Make an electronic tea timer part 2
comments: true
---

[Read part 1](/2015/10/28/make-electronic-tea-timer/)

Now that I am able to program an ATtiny45 with the help of the Arduino IDE, I
want to do the same without the IDE. For this, I have to switch from the Arduino language to C, using the `avr-gcc` cross compiler and the `avrdude` tool.

I will also show you the difference in size between a program written in the
Arduino language and the same program written in C.

The program is for two buttons and two LEDs. Button A turns on or off the LED A and button B turns on or off the LED B. Press a button will change the state of its LED. This program was my *hello world!*

Here it is in Arduino language (`sketch/sketch.ino`):

```c
void setup() {
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  digitalWrite(3, HIGH);
  digitalWrite(4, HIGH);
  pinMode(0, INPUT_PULLUP);
  pinMode(1, INPUT_PULLUP);
}

void loop() {

  if(digitalRead(0) == LOW) {
    delay(10);
    while(digitalRead(0) != HIGH) ;
    delay(10);
    digitalWrite(3, bitRead(PORTB, 3) ^ HIGH);
  }

  if(digitalRead(1) == LOW) {
    delay(10);
    while(digitalRead(1) != HIGH) ;
    delay(10);
    digitalWrite(4, bitRead(PORTB, 4) ^ HIGH);
  }
}
```

The folder just contains two sub folders:

    $ dirtree
    .
    ├── build
    └── sketch

I compile it with the help of the IDE:

    $ ~/local/bin/arduino-1.6.5/arduino --verify sketch/sketch.ino
    --pref build.path=build
    Picked up JAVA_TOOL_OPTIONS: 
    Loading configuration...
    Initializing packages...
    Preparing boards...
    Verifying...

One can check the size of the executable using `avr-size`. It's 972 octets:

    $ avr-size -d build/sketch.cpp.hex 
       text	   data	    bss	    dec	    hex	filename
          0	    972	      0	    972	    3cc	build/sketch.cpp.hex

Now the same program, but this time written in C (`main.c`):

```c
#include <avr/io.h>
#define F_CPU 1000000UL
#include <util/delay.h>

int main(void)
{
  DDRB |= 1 << 4 | 1 << 3;
  PORTB |= 1 << 4 | 1 << 3;
  DDRB &= ~(1 << 0 | 1 << 1);
  PORTB |= (1 << 0 | 1 << 1);

  while(1) {

    if(!(PINB & (1 << 0))) {
      _delay_ms(10);
      while(!(PINB & (1 << 0))) ;
      _delay_ms(10);
      PORTB ^= (1 << 3);
    }

    if(!(PINB & (1 << 1))) {
      _delay_ms(10);
      while(!(PINB & (1 << 1))) ;
      _delay_ms(10);
      PORTB ^= (1 << 4);
    }
  }
}
```

The compile tool chain is a bit longer:

    $ avr-gcc -O -mmcu=attiny45 -c main.c
    $ avr-gcc -mmcu=attiny45 -o main.elf main.o
    $ avr-objcopy -O ihex main.elf main.hex

Even with an optimization option at the bare minimum, the difference in size is…
astronomical:

    $ avr-size -d main.hex 
       text	   data	    bss	    dec	    hex	filename
          0	    158	      0	    158	     9e	main.hex

To transfer the binary into the micro processor I don't need the Arduino IDE
anymore. I put the ATtiny45 on the [programmer shield](/2015/10/28/make-electronic-tea-timer/) that I made last time and I use `avrdude`:

```
avrdude -p attiny45 -P /dev/ttyUSB0 -c arduino -U flash:w:main.hex -b 19200
```

Next time I will show you the code for the electronic tea timer, its Makefile,
and so forth.

[Read part 1](/2015/10/28/make-electronic-tea-timer/)

