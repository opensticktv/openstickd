# openstickd

The OpenStick device daemon. One process owns device state; the launcher, the local web UI, Home Assistant and the HomeKit and Matter bridges all talk to it.

Status: design only. Runs as a privileged Android service app on the certified Android TV platform, written in Kotlin ([decision 0008](https://github.com/opensticktv/openstick/blob/main/decisions/0008-certified-base-open-layer.md)).

## Responsibilities

- Settings and profiles
- App registry: reads app manifests, launches and stops apps
- Local API: REST plus WebSocket, advertised over mDNS as `_openstick._tcp` ([draft spec](api/openapi.yaml))
- HDMI-CEC through the platform's HDMI-CEC APIs: power, input switch, volume
- Bridges: HomeKit Television accessory; Matter video player if the platform allows
- On-screen notifications (Home Assistant notify service)
- Guest mode for the open casting receivers

See [docs/security.md](docs/security.md) for how the local API is protected.
