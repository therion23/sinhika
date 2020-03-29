# conffiles

All of these belong in /usr/local/etc

## asound.conf

The whole magick in this is threefold:

- one, you split your default output device into two, so you can separately control the volume levels of your music and your noise (which is which is pretty much up to yourself).

- two, you get the advantage of software volume controlling DAC's and other sound devices which do not have hardware volume controls - notably, the pHAT DAC and the HifiBerry it was modelled after.

- three, you get a definition for the OSS layer emulation that you can tinker with yourself if need be.
