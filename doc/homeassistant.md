# Home Assistant integration

There are a lot of README's in this project. If you have at least followed the one from [conffiles](../conffiles) then you should be up to speed with this one.

There is also an abundant lack of setting up Sinhika real easily, so here's the least strainful way, which does not require a degree in rocket science - you simply have to follow this step by step.

## Prerequisites

- A functional Home Assistant installation. TAKE NOTE: This has ONLY been tested with a venv installation (https://www.home-assistant.io/docs/installation/virtualenv/) - anything else might or might not work.

- The ability to run Sinhika on the same machine (not entirely necessary, as long as you know how to set up SSH keypairs).

- Following [the ALSA setup](../conffiles/README.md) - which is mostly documented

- Following [the MPD setup](../conffiles/MPD.md) - which is partially documented

- Following [the SBAgen setup](../conffiles/SBA.md) - which is not documented yet at all

## Tools of the trade

Okay, so you got the asound.conf in place, you got MPD running, it is time to create your own user interface.

First of all, it would be so much easier if you run Home Assistant as your own user. Also, make sure your user has passwordless sudo rights, as in:

```bash
%sudo ALL=(ALL) NOPASSWD: ALL
```

("%sudo" might be "%admin" or "%staff", depending on your flavour).

Second, you want to go to your Profile in Home Assistant and enable Advanced Mode. You will learn why later.

## Let the fun begin

Unless you tinkered too much with /etc/mpd.conf (apart from inserting the audio device definition), you should - in a typical scenario - have an MPD instance running on port 6600. This is a good thing, so let's kick off with setting it up in Home Assistant.

configuration.yaml:

```
media_player:
  - platform: mpd
    host: 192.168.x.x
    port: 6600
    name: Music on Sinhika
```

This gives you the entity media_player.music_on_sinhika which has some very simple media controls. Reload and slap one into your Lovelace layout.

Now, head to a shell prompt, and run alsamixer. The leftmost bar is usually your master volume - it can be called "default", "sysdefault", "Master", "Speakers" and possibly a whole lot of other things you would not name a pet (or a significant other). Make note of this name - i will refer to it as Master from here.

Back to configuration.yaml:

```
sensor:
  - platform: command_line
    name: ALSA Master
    command: amixer -M sget Master | grep "Front Left:" | cut -d "[" -f 2 | cut -d "%" -f 1
    scan_interval: 5
  - platform: command_line
    name: ALSA MPD
    command: amixer -M sget MPD | grep "Front Left:" | cut -d "[" -f 2 | cut -d "%" -f 1
    scan_interval: 5
  - platform: command_line
    name: ALSA SBA
    command: amixer -M sget SBA | grep "Front Left:" | cut -d "[" -f 2 | cut -d "%" -f 1
    scan_interval: 5
```

This sets up three sensors to expose the volume levels you want to be able to mix in a Sinhika. scan_interval is really only important if you think of changing volumes outside of Home Assistant - setting it lower would possibly give an unnecessary load on your server - you choose.

More configuration.yaml:

```
shell_command:
  set_speaker_volume: amixer set Master - '{{ states.input_number.volume_master.state | int}}'% -M
  set_mpd_volume: amixer set MPD - '{{ states.input_number.volume_mpd.state | int}}'% -M
  set_sba_volume: amixer set SBA - '{{ states.input_number.volume_sba.state | int}}'% -M
```

Where the sensors are for reading from ALSA, the above commands are for writing to ALSA. Mapped (logarithmic) volumes are used here, just remove the trailing "-M" if you prefer raw volumes.

We are half way done!

Go to Configurations -> Helpers and add three:

- Name: Master
- Minimum value: 0
- Maximum value: 100
- Display mode: Slider
- Step size: 5
- Unit of measurement: %
- Entity ID: input_number.volume_master

Next:

- Name: MPD
- Minimum value: 0
- Maximum value: 100
- Display mode: Slider
- Step size: 5
- Unit of measurement: %
- Entity ID: input_number.volume_mpd

And a third:

- Name: SBA
- Minimum value: 0
- Maximum value: 100
- Display mode: Slider
- Step size: 5
- Unit of measurement: %
- Entity ID: input_number.volume_sba

These are the sliders you can drop into Lovelace. Note that you can set the maximum and minimum volumes anywhere between 0 and 100 - for instance, setting maximum for Master at 40 will, given a decent output device, be pretty much enough for comfortable listening without further damage to your ears. Also, it has the side effect of being easier to navigate on touch devices.

Note also that you can only rename the entities after creating them, saving, and then editing them. Ho hum.

As if that wasn't enough, make a folder in your Home Assistant config folder, name it python_scripts and slap this into a file inside it, naming it set_state.py

```python
#==================================================================================================
#  python_scripts/set_state.py
#==================================================================================================

#--------------------------------------------------------------------------------------------------
# Set the state or other attributes for the entity specified in the Automation Action
#--------------------------------------------------------------------------------------------------

inputEntity = data.get('entity_id')
if inputEntity is None:
    logger.warning("===== entity_id is required if you want to set something.")
else:
    inputStateObject = hass.states.get(inputEntity)
    inputState = inputStateObject.state
    inputAttributesObject = inputStateObject.attributes.copy()

    for item in data:
        newAttribute = data.get(item)
        logger.debug("===== item = {0}; value = {1}".format(item,newAttribute))
        if item == 'entity_id':
            continue            # already handled
        elif item == 'state':
            inputState = newAttribute
        else:
            inputAttributesObject[item] = newAttribute

    hass.states.set(inputEntity, inputState, inputAttributesObject)
```

This is a quick and dirty hack that lets you copy the state from one sensor or entity to another. They are really only for cosmetics, however, it is quite handy that ones ALSA and Home Assistant volume sliders are in sync.

Finally, you need some Automations. and these get a bit tricky if you are not too familiar with Home Assistant. You need to add three of them, replace "master" with "mpd" and "sba" in your copies:

  - Name: ALSA Master
  - Trigger type: State
  - Entity: sensor.alsa_master

And in actions, click the triple dot, choose "edit as YAML", and paste this:

```
data_template:
  entity_id: input_number.volume_master
  state: '{{states(''sensor.alsa_master'') }}'
service: python_script.set_state
```

To make sense of everything when you (re)start Home Assistant, some initial values have to be grabbed. This can be done real easily by creating an Automation with the trigger type of Home Assistant and event Start.

- Action: Call service, Service: automation.trigger, Name: automation.alsa_master
- Action: Call service, Service: automation.trigger, Name: automation.alsa_mpd
- Action: Call service, Service: automation.trigger, Name: automation.alsa_sba

## Lovelace

You can create a card of Entities here, and add:

- input_number.volume_master
- input_number.volume_mpd
- input_number.volume_sba

The narrower your min-to-max gap, the easier it is to navigate on touch devices.

Yeah, it's not simple, but got a better success rate than me writing a web interface.
