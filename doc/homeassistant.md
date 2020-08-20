# Home Assistant integration

There is a lot of README's in this project. If you have at least followed the one up in [../conffiles] then you should be up to speed with this one.

There is also an abundant lack of setting up Sinhika real easily, so here's the least strainful way, which does not require a degree in rocket science - you simply have to follow this step by step.

## Prerequisites

- A functional Home Assistant installation. TAKE NOTE: This has ONLY been tested with a venv installation (https://www.home-assistant.io/docs/installation/virtualenv/) - anything else might or might not work.

- The ability to run Sinhika on the same machine (not entirely necessary, as long as you know how to set up SSH keypairs).

## Tools of the trade

Okay, so you got the asound.conf in place, you got MPD running, it is time to create your own user interface.

First of all, it would be so much easier if you run Home Assistant as your own user. Also, make sure your user has passwordless sudo rights, as in:

```bash
%sudo   ALL=(ALL) NOPASSWD: ALL
```

("sudo" might be "admin" or "staff", depending on your flavour)

Second, you want to go to your Profile in Home Assistant and enable Advanced Mode. You will learn why later.
