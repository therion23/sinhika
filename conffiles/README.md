# conffiles

## asound.conf.(devicename)

The whole magick in this is twofold:

- one, you split your default output device into two, so you can separately control the volume levels of your music and your noise (which is which is pretty much up to yourself).

- two, you get the advantage of software volume controlling DAC's and other sound devices which do not have hardware volume controls - notably, the pHAT DAC and the HifiBerry it was modelled after.

Modify the appropriate file, copy it to /etc/asound.conf and then

```bash
sudo /etc/init.d/alsa-utils restart
speaker-test
```

(hit ctrl-c)

```bash
speaker-test -D mpd
```  
(hit ctrl-c)

Then they should both show up in alsamixer.

The mpd.conf output section should look a bit like this:

```
audio_output {
        type                    "alsa"
        name                    "Sinhika"
        device                  "mpd"
        mixer_type              "hardware"
        mixer_control           "MPD"
        auto_resample           "no"
        auto_format             "no"
        auto_channels           "no"
        replay_gain_handler     "none"
}
```

## rc.local

Append this to your /etc/rc.local - it fixes a problem MPD has with binding a specific port to both IPv6 and IPv4.
