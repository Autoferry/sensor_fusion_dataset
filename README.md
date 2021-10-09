# Maritime Sensor Fusion Dataset
This repo contains the sensor fusion dataset from the paper xxxx 

Detections from radar, lidar, EO and IR cameras are provided in an ownship-fixed NED frame as both json and mat files. Target ground truths are also included. We also aim to publish raw sensor/navigation data used to generate these files if and when any potential privacy concerns have been adressed. 
## Data structure
Each scenario folder contains three files, two json files with detections and ground truth and a single MATLAB file containing both. 
Each detection has the following structure
```javascript
    {
        "sensorID": 3, // Lidar:1, Radar:2, EO:3, IR:4
        
        "ownshipPosition": [ // North-east position of ownship relative to Piren NED frame.
            -16.605584546937536,
            -390.34757580136119
        ],
        "time": 1.6201148916230948E+9, // Time-stamp of measurements
        "measurement": [ // Measurements given in vessel fixed NED. Has dimensions 1xm for EO/IR (bearings) and 2xm for Lidar/Radar (north, east)
            1.0615958558089145,
            1.2464051632248236,
            0.40396339293077094
        ],  
    }
 ```
 Ground truth uses a similar structure with positions and velocities reported in the ownship fixed NED frame. 
 ```javascript
[        {
            "targetID": 1, 
            "position": [
                101.57502148953375,
                36.200472225608678,
                0
            ],
            "velocity": [
                0.0002763919016669642,
                -2.495464414766166,
                0
            ],
            "time": 1.62011489164E+9
        },
        {
            "targetID": 2,
            "position": [
                -137.63073752771453,
                -193.54472437864416,
                0
            ],
            "velocity": [
                -2.7864588537541586,
                -2.4957877293854738,
                0
            ],
            "time": 1.6201148916E+9
        }    ], 
```
## Scenarios
Multiple scenarios are available, each designed to challenge SITAW in certain ways.
### Environment 1
### Environment 2
#### Scenario x
