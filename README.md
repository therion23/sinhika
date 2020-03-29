# sinhika

A framework and patchwork to possibly abstract from tinnitus.

## Platform requirements

The whole idea started out on a Raspberry Pi 1 Model B running the Raspbian flavour of Linux. It is a single core 700MHz ARMv6 based system with 512MB RAM, and can fairly much run a dual MPD server if you roll your own.

Realistically, you would like a little bit more. The Raspberry Pi Zero W was used for a couple of years as reference platform, and with a stripped down home rolled MPD, it runs a dual instance with no problems.

Sound device wise, technically, the only requirement is ALSA compatibility. A large part of the "trick" to this is to split an ALSA device into separate software devices with separate volume controls - exactly like BeOS showed us ages ago, and Windows 10 attempts to do.

## Software requirements

Depending on your sense of adventure, there are different requirements.

For any Debian based Linux distribution, we will soon offer a metapackage to keep your flavour up to date.
