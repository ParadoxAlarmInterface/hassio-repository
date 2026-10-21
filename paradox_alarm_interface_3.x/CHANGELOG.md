# Changelog

## 3.8.1

- Update the PAI image from 3.7.0 to 3.8.1.
- Add PRT3 connection settings, encrypted EVO serial and MG6250 username options.
- Expose current MQTT, Home Assistant naming, notification and IP-interface settings.
- Add `MQTT_DEFINITION_TOPIC`, retaining the ignored legacy spelling for saved configurations.
- Add English field labels, examples, units and warnings without tightening existing validation or changing existing defaults.
- Mask credential fields and document password/code lengths without restricting valid panel-specific formats.
- Limit architectures to amd64, aarch64 and armv7, matching the released image.
- Document upgrade steps and unsupported dictionary settings.

Full PAI changes: [release notes](https://github.com/ParadoxAlarmInterface/pai/releases).
