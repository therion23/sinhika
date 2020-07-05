# sinhika

A framework and patchwork to possibly abstract from tinnitus.

## Before you read on

This is not run by any financial interests. The sinhika project is copyrighted the creators, but free for all to grab a copy and use, as long as the terms stated here are met.

We accept no money, bribes, or anything else. If you want to help, go to your local health department, and give them some kind of awareness what tinnitus is.

## Before you even have anything to read

This documentation is updated frequently. One might even say rapidly. Truth be i lost a lot of my notework, so it goes "oh this bit needs to go in there" and repeat as necessary. You get the idea. As such, this project is very incomplete and even worse documented, however, i promise you that i am working on that with all my spare moments. Okay? Okay!

## Disclaimer

We at Nocturnal Productions take NO responsibility for the outcome of using this program, whatever they might be, neither before nor after you have either 1) read this Disclaimer or 2) attempted to run or use a sinhika or any of its components, hereafter collectively referred to as the Application. Neither do we take responsibility for damages, whatever they are financial, mental or anything else that can be related to the Application. We will warn you, that during the creation of sinhika, some problems and accidental deletion of files have occurred, and although we cannot find any errors left, there might be some left (there always are, aren't there?).

YOU ARE FULLY RESPONSIBLE FOR CHOOSING, INSTALLING, USAGE, AND THE RESULTS OF USE OF THIS SOFTWARE. THE AUTHORS PLACE NO GUARANTEE WHATSOEVER ON THE EXECUTION OR OTHERWISE USAGE OF THE APPLICATION.

Having said that, WE DISALLOW YOU TO USE THIS PROGRAM if You cannot abide to the above disclaimer, whatever Your reasons may be. This program is, although copyrighted by Nocturnal Productions, FREE SOFTWARE, and when You pay nothing, expect nothing!

If you cannot abide to this simple Disclaimer, then i, Bo Krogsgaard, as the responsible author of this project, FORBID you to execute or in other ways use this Application, as *YOU* havent paid *ME* a single dime, pfennig or other monetary unit for your copy.

Alternative version:

This was constructed in good faith for the sole purpose of helping people, not screwing up their computers. If anything bums out in the Application, drop us a note and we will try to fix it as soon as possible, but if your dog dies or you get syphilis (or the other way around), it sure isn't because of the Application.

Basically, if this Application screws up your computer, your life or ANYTHING else, don't blame us. If you invoke sinhika, you agree to paying us twice the amount of what you sue us for in case it does not work on your computer, and furthermore, you also agree to pay us two round trip airplane tickets to a destination of our choice - per team member - within seven (7) days of my request, verbally, written, electronic or otherwise.

Oh, and a sixpack. Per contributor.

Really short version:

We are trying to do you a favour, don't be a dick about it if we fail.

## Synopsis

Tinnitus is hell. If you go to an ear doctor, he or she might go "buy a radio". Facts are, it can come from many things, from a concussion, overexposure to loud noises, neck and/or jaw issues .. you name it. Being led to think tinnitus is a single thing is a complete misconception, however, the symptom is the same - yet perceived so individually.

Now, what a very clever guy (i believe it was Harry Nyquist, but i might be wrong) found out once, was that some frequencies can cancel out eachother. It is not that simple though, but a concept worth trying out in this context. So drawing from that idea, this project sets up a sound card with independent channels for music and distraction frequencies, the latter being binaural patterns or pure pink noise, modulated as you wish.

This does not fix any of your problems. But it might help a little bit.

## Platform requirements

The whole idea started out on a Raspberry Pi 1 Model B running the Raspbian flavour of Linux. It is a single core 700MHz ARMv6 based system with 512MB RAM, and can fairly much run a dual MPD server if you roll your own.

Realistically, you would like a little bit more. The Raspberry Pi Zero W was used for a couple of years as reference platform, and with a stripped down home rolled MPD, it runs a dual instance with no problems.

Sound device wise, technically, the only requirement is ALSA compatibility. A large part of the "trick" to this is to split an ALSA device into separate software devices with separate volume controls - exactly like BeOS showed us ages ago, and Windows 10 attempts to do.

The perl scripts will work with perl 5.10 upwards. The shell scripts should run under any bash at least down to 3.2, and will in the near future be made generic (if they aren't already).

## Software requirements

Depending on your sense of adventure, there are different requirements.

For any Debian based Linux distribution, we will soon offer a metapackage to keep your flavour up to date.
