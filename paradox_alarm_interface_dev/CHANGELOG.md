# Changelog

## Configuration refresh

- Align options and schema with the stable 3.8.1 add-ons, including PRT3,
  encrypted EVO serial, MQTT, notification and IP-interface settings.
- Add masked credentials and English field labels, examples, units and warnings.
- Preserve existing defaults and accepted legacy settings; add the explicit
  `MQTT_BASE_TOPIC: paradox` default, matching PAI's existing default.
- Match published image architectures: amd64, aarch64 and armv7.
- Update setup guidance and document unsupported dictionary settings.
- Retain the rolling `dev` image tag and experimental status.

The development image follows the `dev` branch. It is not stable and should not
be used in production.

See [development commits](https://github.com/ParadoxAlarmInterface/pai/commits/dev)
for code changes.
