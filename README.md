<!-- README.me is generated automatically from .single-source-of-truth.org
    File edits may be overwritten! -->


# About

```text
- Name: lickport_array_interface
- Version: 2.0.1
- Description: Python interface to the Janelia Dudman lab mouse lickport array.
- License: BSD 3-Clause License
- URL: https://github.com/janelia-python/lickport_array_interface_python
- Author: Peter Polidoro
- Email: peter@polidoro.io
- Copyright: 2022 Howard Hughes Medical Institute
- Dependencies:
  - modular_client
```


# More Information

This library is an interface to the [Lickport Array Module](https://github.com/janelia-kicad/lickport_array_module).


# Example Usage

```python
from lickport_array_interface import LickportArrayInterface, LickportArrayMetadata
dev = LickportArrayInterface() # Try to automatically detect port
dev = LickportArrayInterface(port='/dev/ttyACM0') # Linux specific port
dev = LickportArrayInterface(port='/dev/tty.usbmodem262471') # Mac OS X specific port
dev = LickportArrayInterface(port='COM3') # Windows specific port

data_path_str = '~/lickport_array_data/data_file'

metadata = LickportArrayMetadata()
metadata.experiment_name = 'mouse_library'
metadata.task_name = 'hex_foraging_V2'
metadata.subject_id = 'ML11_NAc'

dev.controller.activate_lickports([0,1])
dev.start_acquiring_data()
dev.start_saving_data(data_path_str,metadata)
dev.stop_saving_data()
dev.stop_acquiring_data()

dev.controller.dispense_lickport_for_duration(0,200)
dev.controller.dispense_lickports_for_duration([0,1],200)
dev.controller.dispense_all_lickports_for_duration(200)
dev.controller.get_activated_lickports()
dev.controller.activate_only_lickport(0)
dev.controller.activate_only_lickports([0,1])
dev.controller.activate_lickport(0)
dev.controller.activate_lickports([0,1])
dev.controller.deactivate_lickport(0)
dev.controller.deactivate_lickports([0,1])
dev.controller.activate_all_lickports()
dev.controller.deactivate_all_lickports()
```


## Data

    I Experiment name  : mouse_library
    I Task name  : hex_foraging_V2
    I Subject ID : ML11_NAc
    I Start date : 2022/05/23 16:43:38
    time,millis,lickport_0,lickport_1,lickport_2,lickport_3,lickport_4,lickport_5,lickport_6,lickport_7,lickport_8,lickport_9,lickport_10,lickport_11
    1653338620,956503527,A,LA,,,,,,,,,,
    1653338622,956505441,LA,A,,,,,,,,,,
    1653338624,956507372,A,A,,,,,,,,,,L
    1653338626,956509622,A,A,,,,,,L,,,,
    1653338628,956511133,A,A,,L,,,,,,,,
    1653338629,956512828,A,A,,,L,,,,,,,


### time

time in seconds since the epoch

The epoch is the point where the time starts, and is platform dependent. For Unix, the epoch is January 1, 1970, 00:00:00 (UTC)

The term seconds since the epoch refers to the total number of elapsed seconds since the epoch, typically excluding leap seconds. Leap seconds are excluded from this total on all POSIX-compliant platforms.


### millis

The number of milliseconds passed since the LickportArrayController board was powered. This number will overflow (go back to zero), after approximately 50 days.


### lickport\_n

| Symbol       | Meaning                                         |
|------------ |----------------------------------------------- |
| "L"          | lickport\_n lick detected                       |
| "A"          | lickport\_n activated                           |
| "LA" or "AL" | lickport\_n lick detected and activated         |
| ""           | lickport\_n neither lick detected nor activated |


# Installation

<https://github.com/janelia-python/python_setup>


## Linux and Mac OS X

```sh
python3 -m venv ~/venvs/lickport_array_interface
source ~/venvs/lickport_array_interface/bin/activate
pip install lickport_array_interface
```


## Windows

```sh
python3 -m venv C:\venvs\lickport_array_interface
C:\venvs\lickport_array_interface\Scripts\activate
pip install lickport_array_interface
```


## Guix

Setup guix-janelia channel:

<https://github.com/guix-janelia/guix-janelia>

```sh
guix install python-lickport-array-interface
```
