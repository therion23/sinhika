# MPD setup

On most flavours, you can simply "apt install mpd" (and while you are at it, "apt install mpc").

After you configured softvol (you have, haven't you?), it is time to edit /etc/mpd.conf like this:

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
