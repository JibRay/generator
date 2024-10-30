# generator

## Description

This project builds a backup generator monitor. It senses temperature,
humidity and battery voltage. It uses a Raspberry Pi Pico W board. These
values are displayed on a web page. The tempurature and humidity are sensed
by a SHT30 device.

## Setup
### Python Virtual Environment
1. Create the python virtual environment with:
     `python3 -m venv .venv`
2. Activate the virtual environment with:
     `source .venv/bin/activate`
3. Confirm the virtual environment is active with:
     `which python3`
 The path should be to the .venv directory.
4. Deactivate the virtual environment with:
     `deactivate`
 Note the virtual environment will deactivate when the terminal is closed.

Also add .venv to the .gitignore file.

### Install Required Packages
[See](https://projects.raspberrypi.org/en/projects/get-started-pico-w/1)

1. Download micro-python run-time (RPI_PICO_W*.uf2).
2. Use BOOTSEL button to mount board at /media/<user-name>.
3. copy run-time file to board. Board will un-mount automatically.
4. Install thonny.
5. Install rshell and test REPL with the following code:
     `import machine`
     `led = machine.Pin("LED", machime.Pin.OUT)`
     `led.on()`
     `led.off()`
 Use ctrl-x to exit rshell.
5. Install ampy (pip3 install adafruit-ampy).
6. Find the name of the Pico serial port. Board I am using is at
 /dev/ttyACM0.

I prefer to use nvim for editing and rshell/ampy to run. The thonny IDE does
all this.

Ampy key commands:
     `ampy --port <port-path> put <python-file-path>`
     `ampy --port <port-path> run -n <python-file-name>`
The '-n' causes ampy to disconnect after starting the program. This is
required otherwise ampy times-out waiting for program to end. Use the
following screen command to get program output:

     `screen /dev/ttyACM0 115200`

The shell scripts load-run.sh and load.sh help automate the process.

SHT30 connections (Raspberry Pi Pico W I2C ID 0):
| SHT30 | Pico W | Signal     |
| ----- | ------------------- |
| RED   | pin 36 | +3.3 volts |
| BLK   | pin 38 | ground     |
| YEL   | pin 7  | I2C clock  |
| WHT   | pin 6  | I2C data   |

SHT30 device may have I2c address 0x44 or 0x45. To check this using rshell repl:
     `from machine import I2C`
     `i2c = I2C(id=0)`
     `i2c.scan()`

See README.md in micropython-sht30 for instructions how to test SHT30.
