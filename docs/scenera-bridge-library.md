---
title: Scenera Bridge Library
date: 2022-03-28
slug: scenera-bridge-library
---

**This page is under construction**

## Set the Device Security Object
```
/SetDeviceSecurityObject[POST]
```
Where **Content-Type : application/json**

Example: ```http://192.168.0.117:5001/SetDeviceSecurityObject```

## Set the Device Private Key
```
/SetDevicePrivateKey[POST]
```
Where **Content-Type : application/json**

Example: ```http://192.168.0.117:5001/SetDevicePrivateKey ```

## Start SceneMode Retrieval Process
Start the Scenera Library Thread to get the SceneMode at a regular period:
```
/StartSceneraProcesses/<numberOfNodes>/<repeatperiod> [GET]
```
Note: The numberOfNodes is the value of how many Nodes will be used with the instance of the SceneraLibrary.

Example: ```http://192.168.0.117:5001/StartSceneraProcesses/1/60```

## Monitor to see when the first SceneMode was retrieved
Call this function to see when the first SceneMode was retrieved by the Thread receiving the SceneMode:
```
/IsFirstSceneModeReceived [GET]
```

Example: ```http://192.168.0.117:5001/IsFirstSceneModeReceived ```

## Monitor the status and progress of the retrieving of the SceneMode
Call this function to see the status and progress of the retrieving of the SceneMode:
```
/GetSceneModeReceivedProcessStatus [GET]
```

Example: ```http://192.168.0.117:5001/GetSceneModeReceivedProcessStatus```

Here are the processing Responses to monitor the process of getting the SceneMode:
```
{"Success": true, "StatusMessage": "Waiting for -> StartSceneraProcesses"}
{"Success": true, "StatusMessage": "Busy Getting DeviceSecurityObject"}
{"Success": true, "StatusMessage": "Busy Setting PrivateKeyAndDeviceCertificate"}
{"Success": true, "StatusMessage": "Busy Getting ManagementEndPoint"}
{"Success": true, "StatusMessage": "Busy Getting ManagementObject"}
{"Success": true, "StatusMessage": "Busy Getting DeviceControlObject"}
{"Success": true, "StatusMessage": "Busy Getting SceneMode"}
{"Success": true, "StatusMessage": "Completed Receiving The First SceneMode"}
```

Here are the potential error messages:

```
{"Success": false, "StatusMessage": "Error: Getting DeviceSecurityObject" }
{"Success": false, "StatusMessage": "Error Setting PrivateKeyAndDeviceCertificate"}
{"Success": false, "StatusMessage": "Error: Getting ManagementEndPoint from NiceLA"}
{"Success": false, "StatusMessage": "Error: Getting ManagementObject from NiceLA"}
{"Success": false, "StatusMessage": "Error: Getting DeviceControlObjectInfo"}
{"Success": false, "StatusMessage": "Error: Getting SceneMarkInfo"}
```

## Return/Get the SceneMode
Returns the SceneMode retrieved:
```
/GetSceneMode/<NodesID> [GET]
```
Note: The NodeID is starting at 1 to the numberOfNodes defined in the StartSceneraProcesses

Example: ```http://192.168.0.120:5001/GetSceneMode/1```

## Get Video URL 
Get the VideoURL to use from the retrieved the SceneMode:
```
/GetVideoURL/<NodesID> [GET]
```

Example: ```http://192.168.0.100:5001/GetVideoURL/1``` 			

## Upload SceneMark and SceneData of Images
### Execute the following steps:
1. Clear the list of Objectd to be used for a SceneMark:
```
/ClearDetectedObjects/<NodesID> [GET]
```
Example: ```http://192.168.0.117:5001/ClearDetectedObjects/1 ```

2. Update the detected objects in a scene by calling the following function for every object detected in an image:
```
/UpdateDetectedObjects/<label>/<Probability>/<xmin>/<xmax>/<ymin>/<ymax>/<Width>/<Height>/<NodesID>[POST]
```
Note: The &lt;Width\> and &lt;Height\> are of the full image
Where **Content-Type : image/jpeg**

Example: ```Example: http://192.168.0.117:5001/UpdateDetectedObjects/Human/0.9/10/20/30/40/412/320/1 ```

3. If a new Video recording is started with this SceneMark then the following function should be called to update the SceneDataID for the Video:
```
/CreateVideoSceneDataID/<recordingduration>/<Width>/<Height>/<NodesID> [GET]
```
Note: The &lt;Width\> and &lt;Height\> are the video resolution

Example: ```http://192.168.0.117:5001/CreateVideoSceneDataID/60/19801/10801/1 ```

4. Send the Scenemark
```
/SendSceneMark/<NodeID>/<PortID> [GET]
```

Example: ```http://192.168.0.117:5001/SendSceneMark/1/1 ```

5. Send the Detected Objects' SceneData
```
/SendDetectedObjectsSceneData/<Width>/<Height>/<NodeID> [GET]
```
Note: The &lt;Width\> and &lt;Height\> are of the full image

Example: ```http://192.168.0.117:5001/SendDetectedObjectsSceneData/320/412/1 ```

6. Send Full Images SceneData
```
/SendFullImageSceneData/<Width>/<Height>/<NodeID> [POST]
```
Note: The &lt;Width\> and &lt;Height\> are of the full image
Where **Content-Type : image/jpeg**

Example: ``` http://192.168.0.117:5001/SendFullImageSceneData/320/412/1 ```

## Create and Upload Video SceneData Sections
```
/SendVideoSection/<chunk>/<numberchunks>/<NodeID> [POST]
```
Where **Content-Type : video/mp4**

Example: ```http://192.168.0.117:5001/SendVideoSection/1/1/1 ```

## Stop the SceneMode Retrieval Process
Stop the Scenera Library Thread
```
/StopSceneraProcesses [GET]
```

Example: ```http://192.168.0.117:5001/StopSceneraProcesses ```



