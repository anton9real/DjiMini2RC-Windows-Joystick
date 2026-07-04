# DJI Mini 2 RC to Windows Joystick Interface

This repository contains a Windows compatibility port of the original DJI RC-N1 serial-to-joystick interface. It reads the serial data stream from a DJI Mini 2 Remote Controller (RC-N1) connected via USB and emulates a virtual Xbox 360 controller on Windows using `vgamepad`.

This is a fork/port adapted specifically for Windows environments, replacing Linux-only dependencies (`uinput`).

---

## Features
* **Windows Support:** Works natively on Windows 10 and 11.
* **Xbox 360 Emulation:** Automatically maps the DJI RC sticks and buttons to a virtual Xbox 360 controller recognized by most games and flight simulators.
* **High Refresh Rate:** Runs a background thread at ~50Hz for smooth stick inputs in simulators.
* **Button Support:** Maps the RC-N1 physical buttons (C1, C2, Record, Photo) to Xbox A/B/X/Y buttons.
* **Trigger Support:** Maps the RC-N1 gimbal wheel/switch to Xbox left and right triggers.
* **Debug Mode:** Built-in `--debug` flag to inspect raw serial packets for troubleshooting button mappings.

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
1. Connect your DJI RC-N1 controller via USB to your PC and turn it on. IMPORTANT! Bottom Port
2. Open the Windows **Device Manager** (Geräte-Manager).
3. Expand **Ports (COM & LPT)** and note down the COM port number (e.g., `COM5` or `COM6`).

### 2. Run the Script
Navigate to your project directory in PowerShell or Command Prompt and run the script by passing your COM port via the `-p` flag:

```bash
python main.py -p COM6
```
*(Replace `COM6` with your actual COM port).*

### 3. Debug Mode (Optional)
If buttons or triggers are not working as expected, run with the `--debug` flag to see raw packet data:

```bash
python main.py -p COM6 --debug
```

This will print the hex payload of every packet received from the controller, making it easy to identify which bytes change when you press each button. Example output:

```
[DEBUG] 58-byte payload: 40 06 27 00 10 60 ...
[DEBUG]   Key bytes: [27]=0x00 [28]=0x10 [29]=0x60 [30]=0x00
[DEBUG]   Active inputs: b1->A
```

---

## Controller Mapping

| RC-N1 Input       | Xbox 360 Equivalent |
|:-------------------|:---------------------|
| Left Stick (H/V)  | Left Joystick X/Y   |
| Right Stick (H/V) | Right Joystick X/Y   |
| Button 1 (C1/Fn)  | A Button             |
| Button 2 (Record) | B Button             |
| Button 3 (Photo)  | X Button             |
| Button 4 (C2)     | Y Button             |
| Gimbal Wheel Up   | Right Trigger        |
| Gimbal Wheel Down | Left Trigger         |

---

## Troubleshooting

* **Buttons not registering:** Run with `--debug` and press each button. Look at the `Key bytes` output to see which byte/bit changes. If the mapping doesn't match your firmware version, the bit positions in `main.py` may need adjusting.
* **Alt+Tab or phantom input:** This was caused by a bug in the trigger parsing that has been fixed. If it still occurs, run with `--debug` to check if any trigger input is being sent while the controller is idle.
* **Script can't open COM port:** Make sure no other application (DJI Fly, DJI Assistant) is using the port. Close them and try again.
* **Controller not detected:** Ensure you are using the **bottom USB-C port** on the RC-N1, not the top one.

## Credits and License

* **Original Project:** Based on the reverse-engineered DJI DUML packet parser from `DjiMini2RCasJoystick-master`.
* **License:** This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.