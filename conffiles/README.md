# conffiles

## asound.conf

The whole magick in this is threefold:

- one, you split your default output device into two, so you can separately control the volume levels of your music and your noise (which is which is pretty much up to yourself).

- two, you get the advantage of software volume controlling DAC's and other sound devices which do not have hardware volume controls - notably, the pHAT DAC and the HifiBerry it was modelled after.

- three, you get a definition for the OSS layer emulation that you can tinker with yourself if need be.

Put this in /etc/asound.conf and then

    sudo /etc/init.d/alsa-utils restart
    speaker-test
(hit ctrl-c)
    speaker-test -D mpd
(hit ctrl-c)

Then they should both show up in alsamixer.

## rc.local

Append this to your /etc/rc.local - it fixes a problem MPD has with binding a specific port to both IPv6 and IPv4.
