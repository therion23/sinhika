# SBAgen

This is an old package that uses OSS as sound layer. However, it is useful and rather essential in tinnitus abstraction, and more or less the pillar of this project.

SBAgen is a binaural generator, that for some works as tinnitus distraction. Binaurals have been used for more reasons than actual purposes before, including selling waveforms as "drugs".

A load of skepticism is necessary here. However, it is a proven fact that certain waveforms act relaxing towards certain people. Hence, there is no claim that "this works" for anybody, but if it has any effect on you and hopefully your abstraction from tinnitus, then please let us hear from you.

For more info, please refer to [the SBAgen homepage][1]

## Compiling

Grab the tarball from the above link. Unpack and enter the directory.

Now, if you want integrated mp3 and ogg playback support, you must apply the two diffs (or edit the files by hand). Also, you will need to pick up a couple of dependencies through apt or whatever your package manager is:

- libvorbisidec-dev
- libogg-dev
- libmad0-dev

Then, edit the build script. Uncomment the line that corresponds to your gcc version. If you prepared the files for mp3 and ogg playback in the above step, you will also need to uncomment those two lines in the script.

Run the build script. You will most likely get a couple of warnings, but nothing that cannot be ignored. Copy the sbagen binary to /usr/local/bin and the *contents* of the examples folder to /usr/local/share/sbagen - and that's it!

[1]: http://uazu.net/sbagen/
