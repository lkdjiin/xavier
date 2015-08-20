---
layout: post
title: Find the Size of an Arduino Program
comments: true
---

If I want to find the size and the memory need of an Arduino program, how do I
do that? And why would I know their size?

<img src="{{site.baseurl}}/public/images/640-arduino-avr.jpg" class="" />

## Where is the program hidden?

The program, in elf format, is located in a hidden folder. You may find that its
size is quite impressive. This is not its final size into the Arduino.

```bash
$ \ls -lh .build/uno/firmware.elf 
-rwxr-xr-x 1 xavier xavier 40K août  19 21:01 .build/uno/firmware.elf
```

*A hidden folder is a folder whose name starts with a dot. One say «hidden»
because on Linux and OS X they are invisible by default.*

## How to find the memory needs of an Arduino program

We are going to use the program `avr-size`:

```bash
$ avr-size -dC .build/uno/firmware.elf 
AVR Memory Usage
----------------
Device: Unknown

Program:    2786 bytes
(.text + .data + .bootloader)

Data:         34 bytes
(.data + .bss + .noinit)
```

Here I'm using 34 bytes of RAM, for a total of 2786 bytes into the
microcontroller.

The switch `-d` gives us the values in decimal. The switch `-C` specify the
report's format from `avr-size`. See `avr-size --help` for other formats.

## Why

ATMEL microcontrollers have different size of memory (for the program and for
the RAM). For example the ATtiny13 has 1 Kb for the program and 64 bytes of
RAM, while the ATtiny85 has 8 Kb for the program and 512 bytes for the RAM.

For those programs who are intended to leave the Arduino platform, to end in a
microcontroller, knowing the memory size helps to know if it's interesting
to spend time and energy to optimise these programs.
