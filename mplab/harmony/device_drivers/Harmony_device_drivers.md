# How to develop custom device driver for MPLAB Harmony Framework

The note in this file are based on the complete document that can be found [here](http://ww1.microchip.com/downloads/en/DeviceDoc/MPLAB%20Harmony%20Driver%20Development%20Guide_v111.pdf).

## System Interface

Every driver has 2 interfaces, one to the system and one to the user (via a Client interface).
The functions that the system use to interface the driver are the following:
- `DRV_<module>_Initialize`
- `DRV_<module>_Tasks`
- `DRV_<module>_Reinitialize`
- `DRV_<module>_Deinitialize`
- `DRV_<module>_Status`


