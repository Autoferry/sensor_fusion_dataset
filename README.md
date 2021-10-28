# Maritime Sensor Fusion Benchmark Dataset
This page contains the Autoferry sensor fusion benchmark dataset for multi-target tracking. Get the datasets [here](https://github.com/Autoferry/sensor_fusion_dataset) or by following the *View on GitHub* link above.

Detections from radar, lidar, EO and IR cameras are provided in an ownship-fixed NED frame as both json and mat files. Target ground truths are also included. We also aim to publish raw sensor/navigation data used to generate these files if and when any potential privacy concerns have been adressed. 
## Data structure
Each scenario folder contains three files, two json files with detections and ground truth and a single MATLAB file containing both. Each file will contain a series of detections or measurements where a detections index in the detection list will have a corresponding ground truth index in the ground truth list, e.g. the fifth detection object will correspond to the fifth ground truth object.

Each detection has the following structure
```javascript
    {
        "sensorID": 3, // Lidar:1, Radar:2, IR:3, EO:4
        
        "ownshipPosition": [ // North-east position of ownship relative to Piren NED frame.
            -16.605584546937536,
            -390.34757580136119
        ],
        "time": 1.6201148916230948E+9, // Time-stamp of measurements
        "measurement": [ // Measurements given in vessel fixed NED. Has dimensions 1xM for EO/IR (bearings) and 2xM for Lidar/Radar (north, east)
            1.0615958558089145,
            1.2464051632248236,
            0.40396339293077094
        ],  
    }
 ```
 Ground truth uses a similar structure with positions and velocities reported in the Piren NED frame. 
 ```javascript
[        {
            "targetID": 1, // Havfruen
            "position": [ // Reported in Piren NED frame.
                101.57502148953375,
                36.200472225608678,
                0
            ],
            "time": 1.62011489164E+9
        },
        {
            "targetID": 2, // Gunnerus/Jet boat (environment 1/2)
            "position": [
                -137.63073752771453,
                -193.54472437864416,
                0
            ],
            "time": 1.6201148916E+9
        }    ], 
```
Measurements can be converted to the Piren NED frame by adding the ownship position to each individual measurement for the radar/lidar. Similarly ground truth can be converted to the ownship NED frame by subtracting the ownship translation of the corresponding detection. 
The Piren NED frame has origin in the LLA coordinates
 ```javascript
PirenLLA = [63.4389029083, 10.39908278, 39.923]
```
## Scenarios
Multiple scenarios are available, each designed to challenge tracking systems in certain ways.
### Target vessels
A total of three reference targets were employed during the collection of this dataset. Two targets were only used in a single environment each while one was used in both.
#### Havfruen
Havfruen is a medium-sized leisure craft owned by the \textit{Mannhullet} student association at NTNU. Havfruen was used in both environments
![Havfruen](/figs/havfruen.jpg)
#### Gunnerus
R/V Gunnerus is an ocean-going research vessel owned by NTNU and was used as a reference target in environment 1.
![Havfruen](/figs/gunnerus.jpg)
#### Jetboat
The final reference target used in environment 2 is a water jetboat designed for professional use.
![Havfruen](/figs/jet.jpg)
### Environment 1
Data recording in this environment took place on the 4th of May 2021 from 09:44 to 13:41 in partially cloudy weather.
#### Scenario 2
In this scenario Havfruen starts to the east while Gunnerus starts to the west. The targets perform a crossing maneuver in front of milliAmpere where Havfruen travels behind Gunnerus relative to milliAmpere. Challenges in this dataset include track merging, merged measurements, track continuation as well as target obscuration.
![Scenario 2 Map](/figs/scenario2_map.jpg)
#### Scenario 3
In scenario 3 Havfruen start to the north of Gunnerus. Gunnerus holds a relatively steady course south-west while Havfruen maneuvers around Gunnerus, passing to the south. Parts of this maneuver takes place in the sensor shadow of Gunnerus, challenging the ability of the tracking system to both predict and keep alive obscured targets.
![Scenario 3 Map](/figs/scenario3_map.jpg)
#### Scenario 4
Both targets start west of milliAmpere traveling towards it side by side. Close to milliAmpere Gunnerus performs a maneuver to the north while Havfruen continues on its original course. Challenges in this scenario include target maneuvers and merged radar measurements.
![Scenario 4 Map](/figs/scenario4_map.jpg)
#### Scenario 5
This scenario includes a high-speed overtake from Havfruen in the sensor shadow of Gunnerus. Both targets start north of milliAmpere to the east with Havfruen behind Gunnerus. Obscuration and track management are the main challenges in this dataset.
![Scenario 5 Map](/figs/scenario5_map.jpg)
#### Scenario 6
Havfruen starts behind Gunnerus with both targets situated westward of milliAmpere. Gunnerus and Havfruen both travel towards milliAmpere with Havfruen directly behind Gunnerus in its sensor shadow. Closer to milliAmpere Gunnerus maneuvers northwards revealing Havfruen. Challenges include obscuration and track establishment.
![Scenario 6 Map](/figs/scenario6_map.jpg)

### Environment 2
Data recording in this environment took place on the following day, the 5th of May 2021 from 10:52 to 11:57 in partially cloudy weather.
#### Scenario 13
This scenario represents a common scenario in the channel with targets approaching milliAmpere from each side. milliAmpere is docked to the south which initially obscures both targets due to the surrounding buildings. Rapid track establishment is a key part of this scenario.
![Scenario 13 Map](/figs/scenario13_map.jpg)
#### Scenario 16
In this scenario, we repeat the situation from scenario 13 but with milliAmpere stationary in the middle of the channel. This removes most of the obscurations from scenario 13 maximizing the detection range of the sensing system. Both targets travel directly towards milliAmpere and eventually maneuver around it.
![Scenario 16 Map](/figs/scenario16_map.jpg)
#### Scenario 17
Both targets approach milliAmpere from the east traveling side by side. This introduces the potential for merged measurements in the radar which could be mitigated by introducing additional sensors.
![Scenario 17 Map](/figs/scenario17_map.jpg)
#### Scenario 22
This scenario includes a channel crossing from milliAmpere starting north. Both targets start east and travel westward side by side. Near milliAmpere one target breaks off to the north continuing under the bridge. Track merging and track continuation are relevant challenges in this scenario as well as accurate tracking of target maneuvers.
![Scenario 22 Map](/figs/scenario22_map.jpg)
