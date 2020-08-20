# Documentation

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
