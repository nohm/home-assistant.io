---
layout: page
title: "QwikSwitch QSUSB Hub"
description: "Instructions how to integrate the QwikSwitch QSUSB Hub into Home Assistant."
date: 2016-05-04 00:00
sidebar: true
comments: false
sharing: true
footer: true
logo: qwikswitch.png
ha_category: Hub
featured: false
ha_release: "0.20"
---


The `qwikswitch` component is the main component to integrate various [QwikSwitch](http://www.qwikswitch.co.za/) devices with Home Assistant.

Loading the `qwikswitch` component will automatically adds all devices from the QS Mobile application. QS Mobile controls the QSUSB Modem device.

Currently QwikSwitch relays and LED dimmers are supported (tested). QwikSwitch relay devices can be [switches](/components/switch.qwikswitch/) or [lights](/components/light.qwikswitch/) in Home-Assistant. If the device name in the QSUSB app ends with ` Switch` it will be created as a switch, otherwise as a light.

Example configuration:

```yaml
# Example configuration.yaml entry
qwikswitch:
   url: 'http://127.0.0.1:2020'
```

Configuration variables:

- **url** (*Required*): The URL including the port of your QwikSwitch hub.

### {% linkable_title QwikSwitch Buttons %}

QwikSwitch devices (i.e. transmitter buttons) will fire events on the Home Assistant bus. These events can then be used as triggers for any `automation` action, as follows:

```yaml
automation:
  - alias: Action - Respond to button press
    trigger:
      platform: event
      event_type: qwikswitch.button.@12df34
```

`event_type` names should be in the format **qwikswitch.button.@__ID__**. where **@__ID__** will be captured in the Home Assistant log when pressing the button. Alternatively, you can also access the listen API call by going to 'http://127.0.0.1:2020/&listen' and then pressing the button.

Currently Event will be created for the following commands (cmd) value in the Listen packet:
- `TOGGLE` - Normal QwikSwitch Transmitter button
- `SCENE EXE` - QwikSwitch Scene Transmitter buttons
- `LEVEL` - QwikSwitch OFF Transmitter buttons

Technically this could work for Keyfobs, door sensors, and PIR transmitters as well.
