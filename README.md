# Thorlabs PAX1000 Polarimeter Tool

This is a module to help program the [PAX1000 Polarimeter](https://www.thorlabs.com/newgrouppage9.cfm?objectgroup_id=1564) in Python.

# Requirements

1. Install the official [Software for PAX1000 Series Polarimeters](https://www.thorlabs.com/software_pages/viewsoftwarepage.cfm?code=PAX1000x).
2. Install pre-requisite Python modules:
```
# ctypes module
pip install ctypes

# pyvisa module
pip install pyvisa
```
# Usage

* Copy the file `./src/PAX1000LTM.py` to your local folder where you will write codes to call the module.
* In your python file, you can do:
```
from PAX1000LTM import *

# connect to the device
'''
resource identifier, you can find it by:
pyvisa.ResourceManager().list_resources()
'''
resource = b'USB0::0x1313::0x8031::M00766101::INSTR'

polarimeter = Polarimeter(resource, 9, 0.000000532) # measureMode:9, wavelength: 532nm
polarimeter.connectDevice()
# take measurements

'''Initialize the class instance'''
ltm = PolarimeterLTM(polarimeter.handler, None, 0, 30, 0.05)

# take one measurement
ltm.takeOneMeasurement()
```
Refer to files under `./samples` for the complete sample codes and usage.

# Notes
1. The module has been tested under Windows platform, and assumes the `Software for PAX1000 Series Polarimeters` is installed under the `C` driver by default. If you have different install path, you need to change the path in the file `./src/PAX1000LTM.py` at line 20:
```
# {YOUR PATH} is the path where the file TLPAX_64.dll is located. By default: C:\Program Files\IVI Foundation\VISA\Win64\Lib_x64\msc
os.chdir(r"{YOUR PATH}")
```

2. For the code to connect your polarimeter correctly, you need to know the resource id of your device.
You could find this resource id by after pluging the device:
```
pyvisa.ResourceManager().list_resources()
```

# CopyLeft, Nothing Ganranteed
