# SBAgen

This is an old package that uses OSS as sound layer. However, it is useful in tinnitus abstraction (given that abstraction works for you at all), and more or less the pillar of this project.

SBAgen is a binaural generator, that for some works as tinnitus distraction. Binaurals have been used for more reasons than actual purposes before, including selling waveforms as "drugs".

A load of skepticism is necessary here. However, it is a proven fact that certain waveforms act relaxing towards certain people. Hence, there is no claim that "this works" for anybody, but if it has any effect on you and hopefully your abstraction from tinnitus, then please let us hear from you.

For more info, please refer to [the SBAgen homepage][1].

## Compiling

Clone https://github.com/DariuszO/sbagen-alsa and enter the folder. To compile without mp3 and ogg support, run:

> gcc -std=gnu18 -DT_LINUX_ALSA -Wall -g -O2 -o sbagen -fno-omit-frame-pointer sbagen.c -lm -lpthread \`pkg-config --cflags alsa\` \`pkg-config --libs alsa\`

## Installing

Copy the sbagen binary to /usr/local/bin and the *contents* of the examples folder to /usr/local/share/sbagen - and that's it!

[1]: http://uazu.net/sbagen/
