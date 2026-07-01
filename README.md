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
```

---

## How to Use

### 1. Find your RC COM Port
1. Connect your DJI RC-N1 controller via USB to your PC and turn it on.
2. Open the Windows **Device Manager** (Geräte-Manager).
3. Expand **Ports (COM & LPT)** (Anschlüsse) and note down the COM port number (e.g., `COM5` or `COM6`).

### 2. Run the Script
Navigate to your project directory in PowerShell or Command Prompt and run the script by passing your COM port via the `-p` flag:

```bash
python main.py -p COM6
```
*(Replace `COM6` with your actual COM port).*

### 3. Verify the Controller
1. Press `Win + R`, type `joy.cpl` and press Enter.
2. You should see an **Xbox 360 Controller** listed. Click on **Properties** to test the stick movements and buttons live.
3. Keep the script running in the background and launch your simulator (e.g., Liftoff, VelociDrone, DJI Virtual Flight).

---

## Credits and License

* **Original Project:** Based on the reverse-engineered DJI DUML packet parser from `DjiMini2RCasJoystick-master`.
* **License:** This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
