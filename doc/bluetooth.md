# Bluetooth support

Bluetooth support - even without PulseAudio - is quite possible, however, in its current state, Sinhika only supports a single Bluetooth output device. If you have two or more output devices you frequently alternate between, it gets clumsy and messy.

However, you should definitely feel free to venture further than the below and send us some good ideas we can implement and add.

CAVEAT EMPTOR - This "works", but there are a lot of shortcomings - for one, hardware buttons are not supported, and MPD might go tits up when you disconnect an active Bluetooth device. This is work in progress, of course - bear with us, or even better, send us some suggestions!

## Prerequisites

The following is [based on a writeup by user guidol][1] at the Armbian forums - i have removed a couple of unnecessary steps.

First of all you want to grab all the dependencies:
```
apt-get install libasound2 libasound2-dev dh-autoreconf libortp-dev bluez bluez-tools libbluetooth-dev libusb-dev libglib2.0-dev libudev-dev libical-dev libreadline-dev libsbc1 libsbc-dev bluetooth libfdk-aac-dev libdbus-1-dev
```

Then clone bluealsa and set up the build environment:

```
git clone https://github.com/Arkq/bluez-alsa
cd bluez-alsa
autoreconf --install
```

## Building

```
mkdir build
cd build
../configure --enable-aac --enable-ofono
make
sudo make install
```

Certain aarch64 systems require "--with-alsaplugindir=/usr/lib/aarch64-linux-gnu/alsa-lib" added to the configure parameters above.

## Pairing

Pairing - my favourite pastime (a joke fallen completely flat when translated from Danish).

```
sudo bluetoothctl
power on
scan on
```
(.. wait ..)

Put your headset or speakers into pairing mode, and look for them coming up in bluetoothctl. You are looking for a line like this:

```
[NEW] Device 20:74:CF:51:F0:AD Titanium by AfterShokz
```

These two strings are absolutely necessary for this to work. First of all, let's do some bonding. Still inside bluetoothctl:

```
pair 20:74:CF:51:F0:AD
trust 20:74:CF:51:F0:AD
```

If you don't get any error messages, hit ctrl-D or type "exit". If you get a message somewhat like "no agent registered", linux does not recognise your Bluetooth device.

## Configuring

Since we already molested /etc/asound.conf, let's give it another section. Add this at the top, and remember to replace the hardware address with your own:

```
#################################################################
# Bluetooth                                                     #
#################################################################

defaults.bluealsa {
     interface "hci0"            # host Bluetooth adapter
     device "20:74:CF:51:F0:AD"  # Bluetooth headset MAC address
     profile "a2dp"
}
```

Now, edit /etc/mpd.conf so we can pick the Bluetooth device as output:

```
audio_output {
        type                  "alsa"
        name                  "BT Headset"
        device                "bluealsa"
        mixer_type            "software" # This needs fixing
        auto_resample         "no"
        auto_format           "no"
        auto_channels         "no"
        replay_gain_handler   "none"
}
```

Restart MPD, and you will most likely notice sound coming out of both your default device and your Bluetooth device. If you have mpc installed (which is a mighty fine idea), try this:

```
mpc outputs
```

From there, it's just a matter of "mpc disable 1" and "mpc enable 2", or however your devices are enumerated by MPD. Those friendly names you gave the devices come in handy now .. right?

[1]: https://forum.armbian.com/topic/6480-bluealsa-bluetooth-audio-using-alsa-not-pulseaudio/?do=findComment&comment=102525
