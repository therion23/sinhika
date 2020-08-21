# SBAgen

SBAgen is a binaural generator. Binaurals work as tinnitus distraction for some. They have been used for more reasons than actual purposes before, including selling waveforms as "drugs".

A load of skepticism is necessary here. However, it is a proven fact that certain waveforms act relaxing towards certain people. Hence, there is no claim that "this works" for anybody, but if it has any effect on you and hopefully your abstraction from tinnitus, then please let us hear from you.

In this project, binaurals are used as underlying waveforms instead of pink noise. Since you can "shape" them as you wish, they are more varied and therefore (in theory) less annoying than plain pink noise - or rainfall, or whatever you have been using up till now.

For more info, please refer to [the SBAgen homepage][1].

## Compiling

Clone https://github.com/DariuszO/sbagen-alsa and enter the folder. To compile without mp3 and ogg support, run:

```
gcc -std=gnu89 -DT_LINUX_ALSA -Wall -g -O2 -o sbagen -fno-omit-frame-pointer sbagen.c -lm -lpthread \`pkg-config --cflags alsa\` \`pkg-config --libs alsa\`
```

## Installing

Copy the sbagen binary to /usr/local/bin and the *contents* of the examples folder to /usr/local/share/sbagen - and that's it!

[1]: http://uazu.net/sbagen/
