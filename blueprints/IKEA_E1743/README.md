# IKEA E1743 – Smooth Dimming + Adaptive Lighting

A Home Assistant automation blueprint for the **IKEA TRÅDFRI E1743**, using Zigbee2MQTT with smooth dimming and optional Adaptive Lighting integration.

## Installation

[![Import Blueprint into Home Assistant](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2FCarlovdv%2FHA-Blueprints%2Fblob%2Fmain%2Fblueprints%2FIKEA_E1743%2FIKEA_E1743_-_Smooth_Dimming_%2B_Adaptive_Lighting.yaml)

Click **Import Blueprint** to add this blueprint directly to your Home Assistant installation.

## Features

- Smooth dimming using Zigbee2MQTT `brightness_move`
- Short press for on/off or toggle
- Long press to brighten or dim continuously
- Automatic dimming stop on button release
- Optional Adaptive Lighting integration
- Manual brightness override support
- Compatible with individual bulbs and Zigbee2MQTT groups
- No additional Home Assistant helpers required

## Button controls

| Button | Short press | Long press |
|---|---|---|
| Top | Turn on / Toggle | Brighten |
| Bottom | Turn off / Toggle | Dim |
| Release | — | Stop dimming |

## Requirements

- Home Assistant
- Zigbee2MQTT with MQTT integration
- IKEA TRÅDFRI E1743
- Compatible dimmable Zigbee lights
- [Adaptive Lighting](https://github.com/basnijholt/adaptive-lighting) (optional)

## Configuration

After importing, create an automation using the blueprint.

| Setting | Description |
|---|---|
| Controller | Zigbee2MQTT friendly name of the switch |
| MQTT base topic | Defaults to `zigbee2mqtt` |
| Target light | Home Assistant light entity |
| Zigbee2MQTT target | Friendly name of the target light or group |
| Short press mode | On/off or toggle |
| Dimming speed | Brightness change per second |
| Adaptive Lighting | Optional profile switch |

## Adaptive Lighting

When dimming starts, the blueprint marks brightness as manually controlled.

For compatible Adaptive Lighting configurations, this allows manual brightness changes to be respected while automatic colour-temperature adjustments can continue.

Recommended setting:

```yaml
take_over_control_mode: pause_changed
```

## How it works

The blueprint uses Zigbee2MQTT brightness movement commands.

When holding the top button:

```json
{"brightness_move": 50}
```

When holding the bottom button:

```json
{"brightness_move": -50}
```

When releasing either button:

```json
{"brightness_move": "stop"}
```

This allows compatible bulbs to dim smoothly without repeated Home Assistant brightness updates.

## Credits

- [Home Assistant](https://www.home-assistant.io/)
- [Zigbee2MQTT](https://www.zigbee2mqtt.io/)
- [Adaptive Lighting](https://github.com/basnijholt/adaptive-lighting)

## License

See the repository license, if provided.