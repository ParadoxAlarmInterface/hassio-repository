<div align="left">
    <div style="display: flex;">
        <a href="https://gitter.im/paradox-alarm-interface/community">
            <img alt="Gitter" src="https://img.shields.io/gitter/room/paradox-alarm-interface/community?logo=gitter">
        </a>
        <a href="https://hub.docker.com/r/paradoxalarminterface/pai">
            <img alt="Docker Arch" src="https://img.shields.io/badge/docker_arch-386%7Camd64%7Carmv6%7Carmv7%7Carm64-green?logo=docker">
            <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/paradoxalarminterface/pai?logo=docker">
        </a>
        <img alt="GitHub" src="https://img.shields.io/github/license/ParadoxAlarmInterface/pai">
    </div>
</div>

# PAI - Paradox Alarm Interface (deprecated, 2.7.1, second instance)

Middleware that aims to connect to a Paradox Alarm panel, exposing the interface for monitoring and control via several technologies.
With this interface it is possible to integrate Paradox panels with HomeAssistant, OpenHAB, Homebridge or other domotics system that supports MQTT, as well as several IM methods.

It supports MG/SP/EVO panels connected through a serial port, which is present in all panels (TTL 5V), or through a USB 307 module. It also supports connections using the IP150 module, both directly (firmware version <4.0), and through the SITE ID (firmware versions >4.0).

Support for Magellan, Spectra and EVO panels is very stable. If you find a bug, please report it.

For **configuration**, further information and detailed usage refer to the [**Wiki**](https://github.com/ParadoxAlarmInterface/pai/wiki).

Also see changelog in [**Releases**](https://github.com/ParadoxAlarmInterface/pai/releases)
