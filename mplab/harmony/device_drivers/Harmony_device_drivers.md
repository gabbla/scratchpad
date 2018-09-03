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

### Module initialization

A possible implementation of a module initialization is the following: 
```C
SYS_MODULE_OBJ DRV_Sample_Initialize(
		const SYS_MODULE_INDEX index,
		const SYS_MODULE_INIT *init){
	SAMPLE_MODULE_DATA *pObj = (SAMPLE_MODULE_DATA)&gObj[index];
	SAMPLE_MODULE_INIT_DATA *pInit = (SAMPLE_MODULE_INIT_DATA)init;
	
	// Initialize module object
	pObj->state = SAMPLE_STATE_INITIALIZE; // State for the client
	pObj->status = SYS_STATUS_BUSY; // State for the system
	pObj->dataNewIsValid = false;
	pObj->dataProcessedIsValid = false; 

	if(pInit != null){
		pObj->dataNew = pInit->dataSome;
		pObj->dataNewIsValid = true;
	}
	
	return (SYS_MODULE_OBJ)pObj;
}
```

### Module Status

The module `DRV_<module>_Status` function **must** return a value of `SYS_STATUS`, however, it is possible to extend the information by implementing a _detailed_ get status function.
