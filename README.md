# midea-lan python lib

[![Python build](https://github.com/wuwentao/midea-lan/actions/workflows/python-build.yml/badge.svg)](https://github.com/wuwentao/midea-lan/actions/workflows/python-build.yml)
[![Stable](https://img.shields.io/github/v/release/wuwentao/midea-lan)](https://github.com/wuwentao/midea-lan/releases/latest)
[![codecov](https://codecov.io/gh/wuwentao/midea-lan/graph/badge.svg?token=MSM6KLLTYK)](https://codecov.io/gh/wuwentao/midea-lan)

> [中文版 / Chinese README](./README_hans.md)

Control your Midea M-Smart appliances via local area network.

This library is part of https://github.com/georgezhao2010/midea_ac_lan code. It was separated to segregate responsibilities.

⭐If this component is helpful for you, please star it, it encourages me a lot.

## Getting started

### Finding your device

```python3
from midealan.discover import discover
# Without knowing the ip address
discover()
# If you know the ip address
discover(ip_address="203.0.113.11")
# The device type is in hexadecimal as in midealan/devices/TYPE
type_code = hex(list(discover().values())[0]['type'])[2:]
```

### Getting data from device

```python3
from midealan.discover import discover
from midealan.devices import device_selector

token = '...'
key = '...'

# Get the first device
d = list(discover().values())[0]
# Select the device
ac = device_selector(
  name="AC",
  device_id=d['device_id'],
  device_type=d['type'],
  ip_address=d['ip_address'],
  port=d['port'],
  token=token,
  key=key,
  device_protocol=d['protocol'],
  model=d['model'],
  subtype=0,
  customize="",
)

# Connect and authenticate
ac.connect()

# Getting the attributes
print(ac.attributes)
# Setting the temperature
ac.set_target_temperature(23.0, None)
# Setting the swing
ac.set_swing(False, False)
```

### command line tool

```python3
# for local install without uv/venv
python3 -m midealan.cli -h
# for uv development venv
uv run python -m midealan.cli -h
```

## Development

This project uses [uv](https://docs.astral.sh/uv/) for its development environment.
After [installing uv](https://docs.astral.sh/uv/getting-started/installation/):

```bash
git clone https://github.com/wuwentao/midea-lan.git
cd midea-lan
./scripts/setup.sh          # Linux / macOS / WSL2  (Windows: scripts\setup.ps1)
```

This creates a `.venv`, installs all dependencies, and sets up the prek hooks.
Run tools with `uv run`, e.g. `uv run python -m pytest ./tests/`. See the contributing
guide for the full workflow and per-OS uv install instructions.

## Contributing Guide

[CONTRIBUTING](.github/CONTRIBUTING.md)
[中文版CONTRIBUTING](.github/CONTRIBUTING.zh.md)
