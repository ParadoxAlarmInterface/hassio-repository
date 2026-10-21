<div align="left">
    <div style="display: flex;">
        <a href="https://discord.gg/6KaXFtg39r">
            <img alt="Discord" src="https://img.shields.io/discord/1310653159596888064">
        </a>
        <a href="https://hub.docker.com/r/paradoxalarminterface/pai">
            <img alt="Docker Arch" src="https://img.shields.io/badge/docker_arch-amd64%7Carmv7%7Carm64-green?logo=docker">
            <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/paradoxalarminterface/pai?logo=docker">
        </a>
        <img alt="GitHub" src="https://img.shields.io/github/license/ParadoxAlarmInterface/pai">
    </div>
</div>

# PAI - Paradox Alarm Interface (Development version)

Connects supported Paradox SP/MG/EVO panels to Home Assistant through MQTT.
This experimental add-on runs the rolling **PAI `dev` image** on
**amd64, aarch64 or armv7**. It may contain breaking changes and is not recommended
for production alarm systems. Back up your configuration before updating.

The rolling image can change independently of this add-on's configuration schema
and field guidance; consult the
[development branch](https://github.com/ParadoxAlarmInterface/pai/tree/dev)
for changes not yet included in a stable release.

## Configuration

Set options on the add-on's **Configuration** tab, then restart the add-on.
Optional settings may require showing unused options or editing in YAML mode.
English field labels include examples, units and warnings. Existing defaults and
legacy validation are retained; expected PAI ranges are explained without adding
stricter checks to existing fields.

| Connection | Settings |
| --- | --- |
| Serial | `CONNECTION_TYPE: Serial`, `SERIAL_PORT`, `SERIAL_BAUD`. Use the panel's required baud rate. Enable `SERIAL_ENCRYPTED` only for supported full-AES EVO serial connections. |
| IP150 / IP100 | `CONNECTION_TYPE: IP`, host, port and module password. Firmware support varies; see [connection methods](https://github.com/ParadoxAlarmInterface/pai/wiki/Connection-methods). |
| PRT3 | `CONNECTION_TYPE: PRT3`, `PRT3_SERIAL_PORT`, `PRT3_SERIAL_BAUD` (**9600 or 19200 only**, matching the DIP switches). Set area/zone/user counts and communication timeout as needed. |

For PRT3, keep `PRT3_USER_CODE` quoted to preserve leading zeros: empty means
quick-arm only; otherwise use 1-6 digits. PRT3 does not support zone bypass,
direct PGM control or panel time synchronization.

MQTT and Home Assistant discovery are enabled by default. Configure broker
credentials; do not keep the example password. The schema also exposes MQTT
TLS, transport/protocol, QoS, entity naming, challenge authorization, notification
filters and IP-interface bind settings.

### Passwords and codes

Credential fields use masked password inputs. Quote numeric-looking credentials
in YAML to preserve leading zeros.

| Field | Expected format / length |
| --- | --- |
| `PASSWORD` | Native SP/MG/EVO: normally 4 hexadecimal characters; short values are zero-padded and empty values remain supported. MG6250: 1-255 UTF-8 bytes. No shared schema length limit, since these formats differ. |
| `PRT3_USER_CODE` | Empty or 1-6 decimal digits; schema length is 0-6. |
| `IP_CONNECTION_PASSWORD`, `IP_INTERFACE_PASSWORD` | Module/Babyware password; no universal length limit enforced by PAI. |
| `MQTT_HOMEASSISTANT_CODE` | Home Assistant entity code, not the PC password; empty disables the code. No fixed length. |
| MQTT password, API keys/tokens, challenge secret | Broker/service-specific; no fixed schema length. |

## Updating an existing development installation

- Back up the add-on and retain your existing panel, MQTT and `LIMITS` settings.
- `armhf` and `i386` are no longer supported by the published image.
- Rename `MQTT_DEFINITIONS_TOPIC` to **`MQTT_DEFINITION_TOPIC`** if configured;
  the old spelling remains accepted for saved configurations but is ignored by PAI.
- Event levels are `DEBUG`, `INFO`, `WARN`, `ERROR` or `CRITICAL`.
- Before using notification allow/ignore regex lists, clear that interface's
  `*_EVENT_FILTERS` list. The two filter modes cannot be combined.
- If enabling Babyware access, use a unique host port per instance and restrict
  access to trusted clients. It is disabled by default.

## Limitations

| Setting / feature | Limitation in this add-on |
| --- | --- |
| `MODULE_PGM_ADDRESSES` | Not exposed: the current PAI implementation requires integer dictionary keys, but `/data/options.json` converts keys to strings. |
| `PRT3_UTILITY_KEYS`, `MQTT_TOGGLE_CODES` | Not exposed: Supervisor schemas cannot validate arbitrary dictionary keys. PRT3 utility-key discovery buttons therefore cannot be configured here. |
| Command aliases and `LIMITS` | Only the keys listed in the schema are accepted; arbitrary new keys are discarded by Supervisor. |
| Event allow/ignore lists | Use regular-expression strings. Tuple-style numeric event pairs are not represented by the schema. |
| PRT3 baud / user code | Supervisor checks the baud range and code length; PAI additionally requires exactly 9600 or 19200 and digits only. |
| Signal | Requires D-Bus and Python dependencies absent from the stock image. Enabling the option alone is insufficient. |
| MG6250 | Username configuration is available, but released support is limited to login/decryption, not usable monitoring/control. |
| MQTT bind / log file | The stock image overrides `MQTT_BIND_ADDRESS`, `MQTT_BIND_PORT` and `LOGGING_FILE` via environment variables. |

The add-on reads `/data/options.json`, not a `pai.conf` in Home Assistant's
configuration directory. For unsupported dictionary settings, use a standalone
PAI installation with a native configuration file.

See the [configuration guide](https://github.com/ParadoxAlarmInterface/pai/wiki/Configuration)
and [development commits](https://github.com/ParadoxAlarmInterface/pai/commits/dev).
