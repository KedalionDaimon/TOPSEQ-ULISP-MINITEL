TOPSEQ SYSTEM / ULISP 4.7 ON ARDUINO MEGA2560 DRIVING A FRENCH MINITEL

by Nino Ivanov, April 2025

This is a modification of David Johnson-Davies' uLisp interpreter for Arduino MEGA2560 AVR-based microcontroller boards running on French Minitel-terminals, endowed with a (simplistic) "symbolic artificial intelligence". (Check www.ulisp.com for one of the most amazing Lisp systems running on devices from Arduino UNO to Teensy 4.1 boards and many more, like ESP32 varieties etc. Absolutely amazing!)

The .ino-file is ready to flash on an Arduino MEGA2560 board and will give you the uLisp interpreter straight with an "artificial intelligence" that I call a "topic sequencer" and that will "just work" on a Minitel. (The variant topseq...lisp gives you a variant that will run on conventional systems like ECL, SBCL, GCL etc.; the variant ulisptopseq...lisp gives you the variant that could be manually pasted into uLisp on the Arduino MEGA2560, should you prefer to manually enter the system into uLisp, rather than to pre-load it as an .ino-file.)

How the "topic sequencer" works and what it does, as you activate it with (RUN) from within uLisp:

1. You enter sentences as lists of symbols, populating thereby its "knowledge base".

2. Any sentence is assumed to have as "topic" its very first word. It is left to the user how this is handled, whether through careful arrangement of the sentences, or by bluntly stating a first word as topic.

3. Any sentence entered that contains as part of the lists of symbols a symbol in parentheses will cause the system to search the knowledge base for sentences that begin with the word in parentheses (i.e., that have it as topic).

So, in consequence, both the lists:

(JOHN LOVES MARY)

and

(JOHN LOVES (MARY))

will enter the element (JOHN LOVES MARY) into the knowledge base, however, the latter variant will also search for any sentences starting with (MARY) and print them, like (MARY ENJOYS FLOWERS) and (MARY AND JOHN ENJOY WALKS IN SOLITUDE ALONG THE COASTLINE). Through this "discussion", the "conversation" of sorts can be seen as "guided" in a "reasonable" direction - the assumption behind this system is that "thinking" is nothing else than the suitable correlation of concepts that are deemed "of importance" for some situation at hand.

As this is a very small memory board, it only allows for 20 sentences in the knowledge base, but nicely demonstrates said principal idea: that is, there may appear to be a small measure of intelligence simply in associating topics of discussion and proposing notions concerning these topics.

The modifications concerning the Minitel are few, but most importantly, the Minitel operates its serial port at 5V level, thus allowing a direct connection to all sorts of microcontrollers without a voltage regulator. The pinout of the serial port connector on the back of the Minitel is 1(RX/TX) - 2 - 3(GND) - 4 - 5(TX/RX). The default setting is 1200 baud, 7 data bits, even parity, 1 stop bit.

Natively, the Minitel operates in "Videotex" display and does not feature a "nice" backspace. It can be brought to ASCII mode (80 columns x 25 rows) with Fnct-T A and echo can be turned off with Fnct-T E. However, aesthetically more pleasing may be the Videotex mode (Fnct-T V) (40 columns x 25 rows and brighter characters). It "scrolls strangely", too, in that scrolling does not cause a movement of the entire previous text (the very idea of "scrolling"), but instead, once the screen is full, simply the screen is overwritten from top to bottom again, without clearing what was written before. - However, if a byte with decimal value 12 (hexadecimal C) is written to the Minicom, it automatically clears the entire screen. Also, the default "enter" character is CR (rather than Unix' LF, and not CR-LF, either).

To bind the curly braces of the Minitel's keyboard to Backspace and the Clear Screen byte, to adjust the enter character, to slow down printing, to set up the serial port settings and to turn off echo were the modifications done to this version of uLisp featured here.

A video demonstration can be found here:

https://youtu.be/rHo8G7E47J8

(In essence, this is a simplified reimplementation of the idea behind the system presented in

https://github.com/KedalionDaimon/SerendipitousReminder

under this account.)



