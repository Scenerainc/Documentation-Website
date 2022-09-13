---
title: Overview
date: 2021-23-12 13:25:34
slug: general
---

**This page is under construction**

* TODO: add schemalink
* TODO: add types of all fields
* TODO: add whether any fields are required
* TODO: add diagram that explains the layout

Scenera is a real-time IoT analytics platform. It allows devlopers to process, analyze, encrypt, and store data from cameras or other IoT sensors, and receive the results on a mobile or web application. With all it's complexity and pieces, we've built this guide to help explain the system from end to end.

Data is gathered from many cameras, and is always pre-processed by the camera itself or the Bridge. **The Bridge** is a local device, located close to the cameras, that selects from the incoming video-stream based on its settings.

Resulting images and clips of movement, or specific modes of detection (e.g. Humans, Vehicles) are sent to the **DataPipeline**, as SceneMarks and SceneData. SceneMarks contain the metadata of a scene, expressed in a JSON structure. SceneData contain the images or video data.

The DataPipeline bundles the **SceneMark**s and the **SceneData**, and executes any further AI algorithms through a Node Sequence specified by the configuration of the user. Here the DataPipeline sends off the SceneMarks to any (external) AI Nodes. The **AI nodes** will send back the SceneMark to the DataPipeline with updated information, and the Pipeline will execute the next node in line.

When the processing has completed, the SceneMark is processed, and the **App** may retrieve the SceneMarks from the DataPipeline for display.

Let's define some key terms:

## Key Terms
### SceneMarks (SMKs)
- The SceneMark is Scenera's fundamental data structure, used to transmit metadata from the sensors. Scenemarks are JSON files that are passed around the entire platform, and carry all important information about what the system is seeing. How many people are in a frame? What time was a vehicle detected? Did an intruder enter my house while I was gone? All of this information and more is contained within a SceneMark. Please note that no actual PII, video footage, or images are stored in SceneMarks, just URLs and metadata. We will go much further in-depth about this data structure below.

### SceneData
- This is the raw data. Images, video clips, temperature readings, volume levels, audio recordings, all of these are examples of SceneData. These are stored separately from SceneMarks because they are inherently full of PII. Scenera's philosophy of "Zero-Image Surveillance" seeks to draw conclusions from the SceneMark, not the SceneData. 

### The Bridge
- This is a processor that connects the data source (i.e camera, thermometer, or other sensor) to our platform. It must convert raw data into SceneMarks and SceneData, then securely send those SMKs and SceneData to our DataPipeline[link]. The bridge also can conduct AI analysis, though not necessarily. It is written in Python. Learn more about the Bridge here.[link]

### Bridge Nodes
- When processing data streams, each IoT Device that connects to a bridge is called a Node. For example, if one bridge is processing 8 cameras then that Bridge has 8 **Nodes**, each with a unique identifier. The more powerful a Bridge processor is, the more nodes it can handle. Do not confuse bridge nodes with AI nodes (we're sorry about this).

### SceneModes
- This is a data structure that the Business Support System (BSS) [link] uses to communicate configurations to the Bridge. It is a JSON file that contains information on how the brige is to handle the processing and formatting of data.

### Data Pipeline
The Data Pipeline is the backend of our platform. It manages all the logic of storing and routing SceneMarks and SceneData to the various other components. This includes the management of SMK and SceneData databases, the handling of notifications for the mobile app, and translating requests for data to the user-facing applications. Additionally, the Data Pipeline handles AI processing via AI Nodes. Don't confuse these with Bridge Nodes (which are devices). When the mobile application displays a video recording or alerts a user about an intruder, it is receiving all that information from the Data Pipeline. It is written in C# and deployed in k8s via Azure.

### AI Nodes

### BSS
The Business Support System, or BSS, is the web portal used to configure the platform. It is a website with a uniform backend managed by Scenera, and a fully customizable front end that can be tailored for inidividual applications and use cases. Users login to the BSS to manage their **Bridge** processors, manage their cameras and RTSP feeds, and add/remove additional devices or sensors. It is built in React with a Nodejs backend, and deployed via Azure Web Apps.

### Developer Portal
Similar to the BSS, but for developers who are working on the platform's capabiliites, rather than individual configuration. Users can log into the Developer Portal to add or remove new AI algorithms, select which pipelines are available to app users, or define new sensor types. This is a website built with a Python Backend and Django frontend.

### Account Service
The Account Service is a an API backend that manages user accounts and devices in the NICE ecosystem. All devices, users, and bridges as well as the connections between them, are maanged by the Account Service. This is implemented via serveless REST API in Azure Functions. 

### License Authority
The License Authority, or NICE LA, is the authentication server for the NICE ecosystem. As the Account Service adds and configures users and devices, the NICE LA verifies that the certificates and tokens are valid. This server is built in Tomcat & hosted as an Azure Virtual Machine.

### Key Service
The Key Service handles all JWT encryption, decryption, and token generation. It works closely with the NICE AS to guarantee that all devices are authorized to access our platform, as well to protect the platform from unwanted access. The Key Service is a serverless REST backed built in Azure Functions.  

We will discuss these terms in more detail below.


## The SceneMark

The SceneMark is the gold standard data structure for scenes. After the SceneMarks and SceneData are sent to the API, these are merged such that the SceneMark refers to the corresponding SceneData pieces. This updating happens in real time, such that some SceneData pieces may still be uploading, as can be the case with longer videos. During that time the SceneMark is already available for further processing should you wish to, by configuring the minimum amount of SceneData it needs to wait for.

An example SceneMark is shown below. Some aspects of the SceneMark are missing from this example, as they are currently not in use. The full schema can be found at :SCHEMALINK:

```json
{
    "SceneMarkID": "SMK_00000013-60ed-9b3e-8002-000000001951_0001_182a2ae4", mandatory
    "Version": "1.0", mandatory
    "TimeStamp": "2022-07-19T16:25:21.647Z", mandatory
    "NodeID": "00000013-60ed-9b3e-8002-000000001951_0001", mandatory
    "NotificationMessage": "", optional
    "SceneMarkStatus": "Active", optional
    "VersionControl": { mandatory
        "VersionList": [
            {
                "VersionNumber": 1.0, mandatory
                "DateTimeStamp": "2022-07-19T16:25:21.647Z", mandatory (TODO: make it so that the pipeline puts it in for you)
                "NodeID": "Bridge" mandatory
            }
        ]
    },
    "ThumbnailList": [ optional
        {
            "VersionNumber": 1.0, mandatory
            "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_1b0813e7" mandatory
        }
    ],
    "AnalysisList": [ mandatory
        {
            "VersionNumber": 1.0, mandatory
            "EventType": "ItemPresence", mandatory
            "CustomEventType": "", optional
            "AnalysisID": "0001-0002-AI2", optional
            "AnalysisDescription": "YOLOv4", optional
            "ProcessingStatus": "Detected", mandatory
            "ErrorMessage": "", optional
            "TotalItemCount": 1, optional
            "DetectedObjects": [ optional
                {
                    "NICEItemType": "Human", mandatory
                    "CustomItemType": "", optional
                    "ItemID": "", optional
                    "ItemTypeCount": 1, optional
                    "Probability": 0.73, optional
                    "Attributes": [ optional
                        {
                            "VersionNumber": 1.0, mandatory
                            "Attribute": "Mood", mandatory
                            "Value": "Happy", mandatory
                            "ProbabilityOfAttribute": 0.8 optional
                        }
                    ],
                    "BoundingBox": { optional
                        "XCoordinate": 10, mandatory
                        "YCoordinate": 30, mandatory
                        "Height": 10, mandatory
                        "Width": 10 mandatory
                    },
                    "RelatedSceneData": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_e4041246" mandatory
                }
            ]
        }
    ],
    "SceneDataList": [ optional
        {
            "VersionNumber": 1.0, mandatory
            "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_1b0813e7", mandatory
            "TimeStamp": "2022-07-19T16:25:21.647Z", optional
            "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001", mandatory
            "SourceNodeDescription": "Scenera Bridge", optinoal
            "DataType": "Thumbnail", mandatory
            "Status": "Upload in Progress", mandatory (does the datapipeline set this?)
            "Encryption": {}, optional
            "MediaFormat": "JPEG", optional
            "Resolution": { optional
                "Height": 100, mandatory
                "Width": 100 mandatory
            },
            "SceneDataURI": "https://example.scenedata.uri/thumbnail.jpeg" mandatory
        },
        {
            "VersionNumber": 1.0,
            "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_e4041246",
            "TimeStamp": "2022-07-19T16:25:21.647Z",
            "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
            "SourceNodeDescription": "Scenera Bridge",
            "DataType": "RGBStill",
            "Status": "Upload in Progress",
            "Encryption": {},
            "MediaFormat": "JPEG",
            "Resolution": {
                "Height": 320,
                "Width": 416
            },
            "SceneDataURI": "https://example.scenedata.uri/still.jpeg"
        },
        {
            "VersionNumber": 1.0,
            "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_eb907423",
            "TimeStamp": "2022-07-19T16:25:21.647Z",
            "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
            "SourceNodeDescription": "Scenera Bridge",
            "DataType": "RGBVideo",
            "Duration": 30,
            "Status": "Upload in Progress",
            "Encryption": {},
            "MediaFormat": "H.264",
            "Resolution": {
                "Height": 100,
                "Width": 100
            },
            "SceneDataURI": "https://example.scenedata.uri/video.mp4"
        }
    ]
}
```
Let's go through these items one by one.

### Top Level Elements

```json
"SceneMarkID": "SMK_00000013-60ed-9b3e-8002-000000001951_0001_182a2ae4"
```

This is the unique ID the SceneMark is identified with. It's comprised of
- SMK +
- the Device ID (00000013-60ed-9b3e-8002-000000001951) +
- the Node ID (0001) +
- a unique scenemark ID (182a2ae4)

separated by underscores.

```json
"Version": "1.0"
```

Defines the version of the SceneMark schema. Future versions may contain different fields for different purposes (e.g. sounds).

```json
"TimeStamp": "2022-07-19T16:25:21.647Z"
```

Moment when the SceneMark was created.

```json
"NodeID": "00000013-60ed-9b3e-8002-000000001951_0001"
```

The **NodeID** contains both the Device ID and the Node ID

- Device ID (00000013-60ed-9b3e-8002-000000001951)
- Node ID (0001)

```json
"NotificationMessage": ""
```

Specifies a custom message to be displayed in the push notification to the phone. The title of this message is hardcode to "A new SceneMark has arrived", however the body of the message is variable, defaulted to "Press to view in the app", and altered by setting the **NotificationMessage**.

```json
"SceneMarkStatus": "Active"
```

The **SceneMarkStatus** is set to "Active" when the SceneMark is still in the pipeline. It is then set to "Processed" as it has moved through the entire pipeline of processing. The status may be set to "Removed" when the SceneMark is no longer valid or otherwise active.

Possible values:
- Active
- Processed
- Removed

N.B. This setting is currently not properly implemented and the SceneMarkStatus is always set to "Active".

### VersionControl

The purpose of the Version Control is to keep track of what nodes the SceneMark has visited --and consequently what each node has contributed to the processing. The VersionControl item contains a VersionList (it is nested because the VersionControl itself also takes a DataPipelineID, set automatically by the pipeline) the entries of which log when and by what the SceneMark was updated.

```json
"VersionControl": {
    "VersionList": [
        {
            "VersionNumber": 1.0,
            "DateTimeStamp": "2022-07-19T16:25:21.647Z",
            "NodeID": "Bridge"
        }
    ]
}
```
The **VersionNumber** above refers to the point in the node sequence that the current node takes on. The bridge is always 1.0, and any subsequent nodes will infer their own VersionNumber from the highest number in this list, incremented by 1.0. This VersionNumber is distinct from the Version of the SceneMark (see above).

The **DateTimeStamp** refers to exactly when the particular node applied its processing

The **NodeID** contains the unique identifier of the node that made the contribution, here written as "Bridge" for readability, to it will rather take the form of a guid.

### ThumbnailList

```json
"ThumbnailList": [
    {
        "VersionNumber": 1.0,
        "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_1b0813e7"
    }
]
```

The **ThumbnailList** is there to change the thumbnail that is displayed in the app, should any node in the chain decide so. It contains the **VersionNumber** of the node that made the change, and the **SceneDataID** of the image that should feature as a thumbnail. The reason the app does not simply infer the latest thumbnail from the SceneDataList is that the above should allow you to set non-thumbnail images as thumbnail as well, without necessarily classifying them so.

### AnalysisList

The purpose of the AnalysisList is to contain within itself items that summarise all (AI) processing done within a single node. Each node updates the SceneMark with one unique entry, which may contain multiple **DetectedObjects** (explained below).

```json
"AnalysisList": [
    {
        "VersionNumber": 1.0,
        "EventType": "ItemPresence",
        "CustomEventType": "",
        "AnalysisID": "0001-0002-AI2",
        "AnalysisDescription": "YOLOv4",
        "ProcessingStatus": "Detected",
        "ErrorMessage": "",
        "TotalItemCount": 1,
        "DetectedObjects": [ ... ]
    }
]
```
The **VersionNumber** here refers to the number of the node that has done the analysis.

The **EventType** is the supercategory assigned to a node that covers the aggregate event that is the node's 'job' and may take the following forms:

- ItemPresence
- Loitering
- Intrusion
- Falldown
- Violence
- Fire
- Abandonment
- SpeedGate
- Xray
- Facility
- Custom

This list is not set-in-stone and likely to expand (and to some degree contract) in future. **ItemPresence** is a catch-all category that will allow you to list simply some unrelated items. For now, you can append anything to this list, by setting it to **Custom** and then using the **CustomEventType** field to define your own custom category.

The **AnalysisID** refers to the unique identifier associated with the algorithm that is implemented by the node. It will be provided to the node through the developer portal but may also be left blank.

The **AnalysisDescription** describes the algorithm used in a human readable format.

**ProcessingStatus** can take the following values:

- Motion
- Detected
- Recognized
- Characterized
- Undetected
- Failed
- Error
- CustomAnalysis

**Motion** refers to any movement in the stream. **Detected** means some object or other has been detected. **Recognized** is similar to the former but recognized the object as some specific thing or person. **Characterized** refers to a particular aspect of the recognized object, such as a colour or a facial expression. **Undetected** means the algorithm failed to find anything in the image. **Failed** means the algorithm failed to run for some algorithm-specific reason and **Error** means the script crashed. **CustomAnalysis** can be picked whenever above does not cover your needs.

**Error Message** should contain any message that accompanies the above **Error** status. Whatever error occurred running the node can be inserted as a string.

### DetectedObjects

**DetectedObjects** are encapsulated in the AnalysisList item. DetectedObjects are list items that track any sort of separated detections. You may for example log the detection of five humans by using the **NICEItemType** "Human", and setting the **ItemTypeCount** to 5. But you may also separate all five into separate detected objects which may then have their respective confidence and bounding box, item identities and so on. DetectedObjects entries have within themselves an **Attributes** list that shall be treated separately below.

```json
"DetectedObjects": [
    {
        "NICEItemType": "Human",
        "CustomItemType": "",
        "ItemID": "",
        "ItemTypeCount": 1,
        "Probability": 0.73,
        "Attributes": [ ... ],
        "BoundingBox": {
            "XCoordinate": 10,
            "YCoordinate": 30,
            "Height": 10,
            "Width": 10
        },
        "RelatedSceneData": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_e4041246"
    }
]
```

**NICEItemType** is an object category that can take any of the following values

- Motion
- Face
- Human
- Animal
- Vehicle
- Label
- TextLogoQRCode
- Custom
- Scene

**Motion** can be used to log any ordinary movement in a scene. **Face** is for faces. **Human** may log any human, or alien, or whatever humanoid you like to log whole. **Animal** likewise but for dogs, cats. **Vehicle** is for any car, truck, bicycle, plane, or skateboard. **Label** is short for Object Label and may be used to refer to any object you would like to distinguish, such as "chair", "window", and so on. **TextLogoQRCode** can be used for any phrase, QR code, logo, like it says basically. **Custom** can be used to define any category of your own (see below), and lastly **Scene** covers the entire scene in some abstract sense, allowing you to have a generic top level you may use to assign attributes to, such as color, weather, location, and so on.

**CustomItemType** may be used to explain the type of **Label**, and otherwise to specify the **Custom** itemtype.

The **ItemID** is a string that allow you to recognize the item as being a particular (unique) instance, such as a name, e.g. "Elizabeth".

**ItemTypeCount** is an integer that counts the number of that ItemType you've decided to log into a single detected object item.

**Probability** is the confidence level of what you've found. This is hard to do for aggregates (ItemTypeCount >= 2).

**Attributes** can be used to cover any and all aspects of the detected object and are explained below.

The **BoundingBox** is an object that takes the *upper-left* **XCoordinate**, *upper-left* **YCoordinate**, **Height** & **Width** of a bounding box that surrounds some object or objects.

Then finally the **RelatedSceneData** specifies which scenedata the object was detected on, or in.

### Attributes

Attributes are encapsulated within the DetectedObject item. They may be used to list any detail about the object. For example. faces may be given a mood, or objects a color.

```json
"Attributes": [
    {
        "VersionNumber": 1.0,
        "Attribute": "Mood",
        "Value": "Happy",
        "ProbabilityOfAttribute": 0.8
    }
]
```

The **VersionNumber** in the attributes list refers to the node that made this contribution. The reason is that nodes should be able to find attributes of items that had been previously detected by other nodes.

**Attribute** takes the name of the attribute you want to define the value of, so "color" or, in the above case "mood".

**Value** is the value it takes, "blue", "happy", "round", and so on.

And **ProbabilityOfAttribute** sets the confidence for this particular attribute. (Not required, defaulted to 1.0)

### SceneDataList

The SceneDataList contains all the SceneData that is linked to this Scene. SceneData associated with a SceneMark is typically added by the Bridge or the camera itself. Nodes may add SceneData items too, should they wish to.

```json
"SceneDataList": [
    {
        "VersionNumber": 1.0,
        "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_1b0813e7",
        "TimeStamp": "2021-07-19T16:25:21.647Z",
        "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
        "SourceNodeDescription": "Scenera Bridge",
        "DataType": "Thumbnail",
        "Status": "Upload in Progress",
        "Encryption": {},
        "MediaFormat": "JPEG",
        "Resolution": {
            "Height": 320,
            "Width": 416

        },
        "SceneDataURI": "https://example.scenedata.uri/thumbnail.jpeg"
    },
    ...
```

Each item of the SceneData list contains the following entries:

**VersionNumber** is that of the node that added the piece of SceneData. Required.

The **SceneDataID** is structured similar to the SceneMark's, but prefixed by SDT.

**TimeStamp** refers to the moment the SceneData was captured.

The **SourceNodeID** is the NodeID of the device + node that captured the SceneData

**SourceNodeDescription** decribes in a human readable way what the **SourceNodeID** refers to.

A **DataType** may take the following values:

- Thumbnail
- RGBStill
- IRStill
- DepthStill
- RGBStereoStill
- ThermalStill
- RGBVideo
- IRVideo
- DepthVideo
- RGBStereoVideo
- ThermalVideo
- Audio
- Temperature
- Humidity
- PIR
- CarbonMonoxide
- AudioTranscript
- IRDetection
- Pressure
- Proximity
- LiquidLevel
- Acceleration
- Rotation
- Other

There is a distinct **DataType** reserved for the thumbnail, because otherwise defining the minimum amount of scenedata to be collected before the SceneMark is sent off to the nodes will get the images confused with the thumbnails.

**Status** keeps track of whether a piece of SceneData is still uploading, and takes one of two values:

- Available at Provided URI
- Upload in Progress

**Encryption** is not yet implemented, and may be ignored for the time being.

**MediaFormat** specifies the codec used for the piece of data (image, video or otherwise) and may take any of the following values:

- UNSPECIFIED
- JPEG
- PNG
- H264
- H265
- RAW
- JSON

The **Resolution** is used to specify the size of image or video data. It takes a **Height** and a **Width**

And the **SceneDataURI** contains a readily accessible link containing the SceneData. Should a node add SceneData, it then must upload the SceneData somewhere for access.

## The Bridge 
- As we described before, the Bridge is a processor that turns raw information into SceneMarks and SceneData, conducts initial AI analysis on that data, then sends it into our backend.
- The Bridge can be implemented as a docker container or run natively in Python, and can run on physical hardware (usually the Intel NUC or Nvidia Jetson), in cloud VM (typically provisioned via Azure), in the MEC (through one of our 5G partners), or even on the sensor itself (currently in development to be run on Android-powered cameras with onboard processing, as well as some other architectures). 
- Each bridge device can process multiple camera streams or sensor inputs (called "nodes") simultaneously, and is limited only by its processing power. For example, a massive VM may be able to process 1000 camera streams, while a tiny RaspberryPi may only be able to handle 1 or 2 cameras. Obviously, if the bridge is running demanding AI algorithms as well, it will be able to handle fewer camera streams. The processing requirements grow linearly with the # of cameras or devices.
- The bridge can use the results of its AI capabilities to filter unwanted SceneMarks and SceneData from entering the system. A large percentage of camera footage is useless (nightime shots of empty hallways, random vehicles harmlessly driving by, employees riding the elevator to work). Recording this footage is expensive in bandwidth and storage, and also a liability from a privacy perspective. People shouldn't have recordings of them sitting somewhere without purpose. The bridge can use AI to determine what footage is not worth keeping, and discard it at that time, preventing unnecessary costs and protecting people's privacy.
- The Bridge can be configured in many different ways. For example, the number of nodes processed, the AI algorithms in use, the objects to be filtered or ignored, and the length of the video recordings in the SceneData are all values that the user can set. These settings are managed by the user through the Business Support System (BSS).[link]. 
    - The BSS passes these configurations to the Bridge via a data structure called a SceneMode.[link]
