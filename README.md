# Control-LED-with-Raspberry-Pi-using-Blynk-App

![capture1](https://github.com/user-attachments/assets/516889d9-d740-49d8-b02c-ce401c603491)

Control an LED connected to a Raspberry Pi 4B using the Blynk 2.0 IoT mobile app and web dashboard. This project demonstrates real-time IoT control of GPIO pins with Python.

---

## Table of Contents

1. [About](#about)
2. [Introduction](#introduction)
3. [Hardware Requirements](#hardware-requirements)
4. [Software Requirements](#software-requirements)
5. [Raspberry Pi OS Setup](#raspberry-pi-os-setup)
6. [Circuit Diagram](#circuit-diagram)
7. [Blynk App Setup](#blynk-app-setup)
8. [Python Code Setup](#python-code-setup)
9. [Running the Project](#running-the-project)
10. [GitHub Repository](#github-repository)

---

## About

This project allows you to turn an LED ON/OFF on a Raspberry Pi 4B remotely using the Blynk mobile app. The system uses Python and the Blynk Python library to interact with the GPIO pins of the Raspberry Pi.

---

## Introduction

IoT (Internet of Things) enables controlling devices remotely. This project demonstrates a basic IoT application where a single LED can be controlled via a mobile device over Wi-Fi. Perfect for beginners learning IoT, Python programming, and Raspberry Pi hardware interaction.

---

## Hardware Requirements

* Raspberry Pi 4B
* 7” HDMI Display (800x480)
* LED (any color)
* 220Ω Resistor
* Jumper Wires (Male-to-Female)
* Breadboard
* Micro SD Card (16GB+)

---

## Software Requirements

* Raspberry Pi Pure Debian 64-bit OS
* Python 3
* Blynk Python Library
* Text Editor (Thonny / nano / VS Code)

---

## Raspberry Pi OS Setup

1. Download Debian OS (64-bit) for Raspberry Pi from [Raspberry Pi Downloads](https://www.raspberrypi.com/software/).
2. Flash the OS to your SD card using **Balena Etcher** or **Raspberry Pi Imager**.
3. Insert SD card into Raspberry Pi 4B and boot.
4. Complete initial setup (Wi-Fi, username/password, updates).

---

## Circuit Diagram
<img width="236" height="199" alt="image" src="https://github.com/user-attachments/assets/ff240cda-860f-45ce-8f72-5474c859a791" />
```

* LED **anode (+)** → GPIO18 via 220Ω resistor
* LED **cathode (-)** → GND

![Circuit Diagram]

## Blynk App Setup

1. Download **Blynk 2.0** app on your smartphone.

2. Sign up and create a new project:

   * Name: **control LED RaspberryPi**
   * Device: **Raspberry Pi**
   * Connection: **Wi-Fi**

3. Add **Button Widget**:

   * Pin: **V0**
   * Mode: **Switch**
   * Name: **LED**
<img width="335" height="749" alt="image" src="https://github.com/user-attachments/assets/adc1676a-fa47-4451-9427-735c796bbeb8" />
<img width="288" height="637" alt="image" src="https://github.com/user-attachments/assets/57383aa5-117f-4591-932d-89a836a8727e" />



4. Copy **Auth Token** generated for the project and replace in your Python code:

```python
BLYNK_AUTH_TOKEN = 'Your_Auth_Token_Here'
```

---

## Python Code Setup

1. Clone the Blynk Python library:

```bash
git clone https://github.com/vshymanskyy/blynk-library-python.git
cd blynk-library-python
```

2. Create Python file `led_control_blynk.py`:

```python
import BlynkLib
import RPi.GPIO as GPIO

BLYNK_AUTH_TOKEN = 'Your_Auth_Token_Here'

led = 18

GPIO.setmode(GPIO.BCM)
GPIO.setup(led, GPIO.OUT)

blynk = BlynkLib.Blynk(BLYNK_AUTH_TOKEN)

@blynk.on("V0")
def v0_write_handler(value):
    if int(value[0]) != 0:
        GPIO.output(led, GPIO.HIGH)
        print('LED ON')
    else:
        GPIO.output(led, GPIO.LOW)
        print('LED OFF')

@blynk.on("connected")
def blynk_connected():
    print("Raspberry Pi Connected to Blynk")

while True:
    blynk.run()
```

---

## Running the Project

1. Open terminal on Raspberry Pi.
2. Navigate to the project directory.
3. Run Python code:

```bash
sudo python3 led_control_blynk.py
```

4. Open Blynk app on your smartphone.
5. Press **LED button** to turn LED ON/OFF.
6. Check terminal for LED status logs.

---

## Author
Misbah Rafique

* Repository: [https://github.com/Misbah81](https://github.com/Misbah81)

---

