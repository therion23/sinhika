# conffiles

## asound.conf.(devicename)

The whole magick in this is twofold:

- one, you split your default output device into two, so you can separately control the volume levels of your music and your noise (which is which is pretty much up to yourself).

- two, you get the advantage of software volume controlling DAC's and other sound devices which do not have hardware volume controls - notably, the pHAT DAC and the HifiBerry it was modelled after.

Modify the appropriate file, copy it to /etc/asound.conf and then

```bash
sudo /etc/init.d/alsa-utils restart
speaker-test -D mpd
(hit ctrl-c)
speaker-test -D sba
(hit ctrl-c)
```

Then they should both show up in alsamixer.

Now, go read [the MPD setup](../doc/MPD.md)

## rc.local

Append this to your /etc/rc.local - it fixes a problem MPD has with binding a specific port to both IPv6 and IPv4.
