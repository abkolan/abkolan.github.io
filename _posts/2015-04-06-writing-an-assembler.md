---
layout:     post
title:      Writing an assembler
date:       2015-04-06 23:31:20
summary:    Writing an assembler and an emulator for DCPU
categories: c# assembler 
---

Writing an assembler was something I always wanted to do for quite sometime now and finally wrote one. 

###Understanding an Assembler

An assembler is a system software program that takes a low level language like an assembly language that looks like this.

    SET I, 0x8000
    SET X, data
    :loop
    IFE [X], 0x0000
    SET PC, end
    SET A, [X]
    BOR A, 0x7000
    SET [I],A
    ADD X, 0x0001
    ADD I, 0x0001
    SET PC, loop
     
    :end
    SET PC, end
     
    :data
    DAT "Hello, World!",0

To machine code that looks like this


    0x7cc1 0x8000 0x7c61 0x0011 0x8572 0x7f81 0x000f 0x2c01 0x7c0b 0x7000 0x01c1 0x8862 0x88c2 0x7f81 0x0004 0x7f81 0x000f 0x0048 0x0065 0x006c 0x006c 0x006f 0x002c 0x0020 0x0057 0x006f 0x0072 0x006c 0x0064 0x0021 0x0000


Took two days for me to get this up and running, the most part of the time was spent on understanding the DCPU 16 spec. Here is the [end result](https://github.com/abkolan/dcpu16).