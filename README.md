# DJI Mini 2 RC to Windows Joystick Interface

This repository contains a Windows compatibility port of the original DJI RC-N1 serial-to-joystick interface. It reads the serial data stream from a DJI Mini 2 Remote Controller (RC-N1) connected via USB and emulates a virtual Xbox 360 controller on Windows using `vgamepad`.

This is a fork/port adapted specifically for Windows environments, replacing Linux-only dependencies (`uinput`).

---

## Features
* **Windows Support:** Works natively on Windows 10 and 11.
* **Xbox 360 Emulation:** Automatically maps the DJI RC sticks and buttons to a virtual Xbox 360 controller recognized by most games and flight simulators.
* **High Refresh Rate:** Runs a background thread at ~50Hz for smooth stick inputs in simulators.

---

## Requirements

Before running the script, you need to install the virtual gamepad driver and the required Python packages.

### 1. Install ViGEmBus Driver
The `vgamepad` library relies on the ViGEmBus driver to emulate the Xbox controller. 
* Download and install the latest release from the official repository: [ViGEmBus Releases](https://github.com/ViGEm/ViGEmBus/releases).

### 2. Install Python Dependencies
Install the required libraries using `pip`:
```bash
pip install pyserial vgamepad
