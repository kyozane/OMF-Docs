---
uid: dataExample
---

# Data Example

	
In this example, instance data is created for the `static` types \'Plant\' and \'Tank\', and the `dynamic` type, \'TankPressure\', for Containers 
\'Tank1_PressureMeasurements\' and \'Tank2_PressureMeasurements\'. The link data messages are used to relate the instance data as well as combine static and dynamic Types.

### Headers

	omfversion = 1.2
	messagetype = data
	action = create
	messageformat = json

### Body


	[{
		"typeid": "Plant",
		"values": [{
			"PlantId": "WTP1",
			"PlantName": "Water Treatment Plant One",
			"Address": "123 Meridian Ave",
			"Contact": "Bob Ross"
		}]
	}, {
		"typeid": "Tank",
		"values": [{
			"TankName": "Tank1",
			"Serial": "5236-3523-KKF4",
			"Model": "FN-2187"
		}, {
			"TankName": "Tank2",
			"Serial": "2364-4243-FS12",
			"Model": "TK-421"			
		}]	
	}, {
		"typeid": "__Link",
		"values": [{
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "Tank",
				"index": "Tank1"
			}
		}, {
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "Tank",
				"index": "Tank2"
			}
		}, {
			"source": {
				"typeid": "Tank",
				"index": "Tank1"
			},
			"target": {
				"containerid": "Tank1_PressureMeasurements"
			}
		}, {
			"source": {
				"typeid": "Tank",
				"index": "Tank2"
			},
			"target": {
				"containerid": "Tank2_PressureMeasurements"
			}
		}]
	}, {
		"containerid": "Tank1_PressureMeasurements",
		"values": [{
			"Time": "2019-09-11T22:23:23.430Z",
			"Pressure": 12.0
		}, {
			"Time": "2019-09-11T22:24:23.430Z",
			"Pressure": 11.5
		}]
	}, {
		"containerid": "Tank2_PressureMeasurements",
		"values": [{
			"Time": "2019-09-11T22:23:23.430Z",
			"Pressure": 14.0
		}, {
			"Time": "2019-09-11T22:24:23.430Z",
			"Pressure": 15.1
		}]
	}]

### Inheritance Data Message Example

In this example, the Data message contains values for the inherited properties TankName, Serial and Model as well as the properties TankHeight and TankWidth.
 

	{
		"typeid":"RectangularTank",		
		"values": [{ 
			"TankName": "RectangularTank1",
			"Serial":"3829-3827-C0EK",
			"Model":"EL-5839",
			"TankHeight": 120,
			"TankWidth": 90
		}]
	}

### Reference Data Message Example

In this example, the Data message contains values Latitude and Longitude which were included using `reftypeid` on the Location property. 

	{
		"typeid":"TankV2",		
		"values": [{ 
			"TankName": "Tank3",
			"Serial": "1928-4827-2987",
			"Model": "KE-2834",						
			"Location": {
				"Latitude": 36.3134,
				"Longitude": -82.3535
			}
		}]
	}


	
### Enum Data Message Example

In this example, the Data message contains values for the ValvePosition and DeviceStatus. These properties were defined as `enum` types using `reftypeid`. 

	{
		"containerid":"TankMeasurementsV1_Tank3",		
		"values": [{ 			
			"Time": "2019-09-11T22:23:23.430Z",
			"DeviceStatus": 2,
			"ValvePosition": 1,
			"Pressure": 16.0,
			"Temperature": 90.1
		}]
	}




	
### Type-less Static Data Message

In this example, the Data message extends the 'Tank' type to include a 'Maintenance Schedule' for this instance. The 'Tank' Type itself is not extended.

	[{ 
	   "typeid": "Tank",
       "properties": { 
            "Maintenance Schedule": {
				"type": "array",
                "items": {
					"type": "string",
                    "format": "date-time"
                }
			}
        }, 
        "values": [{ 
              "TankName": "Tank1", 
              "Serial": "5236-3523-KKF4", 
              "Model": "FN-2187",
			  "Maintenance Schedule": [ "2019-09-01T00:00:00Z", "2019-09-01T08:00:00Z", "2019-09-01T16:00:00Z" ]
        }] 
	}] 


In this example, the Data message defines properties for a Tank, and sends the instance data. No Type definitions are defined or created. 

	[{ 	   
       "properties": { 
			"Name": {
				"type":"string",
				"isindex":true
			},
			"Description": {
				"type":"string"
			},
			"Model": {
				"type":"string"
			},			
            "HourlyMaintenanceSchedule": {
				"type": "integer",
                "format": "int16"
			}
        }, 
        "values": [{ 
              "Name": "Tank4", 
              "Description": "Tank4 in Building C12", 
              "Model": "EK-2393",
			  "HourlyMaintenanceSchedule": 8
        }] 
	}] 
