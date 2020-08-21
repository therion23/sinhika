# MPD setup

## Server

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

The above uses a subset of the so called "audiophile" settings for MPD.

## Clients

If you are ready to roll your own, git clone https://github.com/jcorporation/myMPD and build it - it is fickle, but your best option for both desktop and handheld. If you add "Restart=always" to the "Service" part of its systemd script, you will barely notice it is gone. In case you intend to control Sinhika from a handheld device running Android, creating a shortcut for it inside Chrome is recommended - full screen and slightly more snappy than opening Chrome itself.

A good alternative for Android is M.A.L.P. - https://play.google.com/store/apps/details?id=org.gateshipone.malp - it has the advantage of handling more than one server.

Do not be tempted to install the MPD client for Kodi. Not only does it break all the design rules, it is also incredibly slow. Please try one or more of the above suggestions instead.
