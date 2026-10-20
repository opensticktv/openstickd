# openstickd

The OpenStick device daemon. One process owns device state; the launcher, the local web UI, Home Assistant and the HomeKit and Matter bridges all talk to it.

Status: design only. Implementation language is open ([decision 0007](https://github.com/opensticktv/openstick/blob/main/decisions/0007-daemon-language.md)).

## Responsibilities

- Settings and profiles
- App registry: reads app manifests, launches and stops apps
- Local API: REST plus WebSocket, advertised over mDNS as `_openstick._tcp` ([draft spec](api/openapi.yaml))
- HDMI-CEC: power, input switch, volume, one-touch-play on cast
- Bridges: HomeKit Television accessory, Matter video player
- On-screen notifications (Home Assistant notify service)
- Guest mode and sender pairing

See [docs/security.md](docs/security.md) for how the local API is protected.
