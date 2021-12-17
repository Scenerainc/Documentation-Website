---
title: Overview
date: 2021-11-15 13:25:34
slug: general
---

Scenera is a real-time image analytics platform. Data is gathered from many cameras, and is always pre-processed by the camera itself or the Bridge. The Bridge is a local device, located close to the cameras, or indeed inside of the camera, that selects from the incoming stream based on its settings.

Resulting images and clips of movement, or specific detection (e.g. Humans, Vehicles) are sent to the DataPipeline as SceneMarks and SceneData. SceneMarks contain the metadata of a scene, expressed in a JSON structure. SceneData contain the images or video data.

The DataPipeline bundles the SceneMarks and the SceneData, and executes any further AI algorithms through a Node Sequence specified by the configuration of the user. Here the DataPipeline sends off the SceneMarks to any (external) AI Nodes. The AI nodes will send back the SceneMark to the DataPipeline with updated information, and the Pipeline will execute the next node in line.

When the processing has completed, the SceneMark is processed, and the App may retrieve the SceneMarks from the DataPipeline for display.

## SceneMarks & SceneData

These data structures are called SceneMarks.

Example:

```json
{
  "SceneMarkID": "SMK_00000013-60ed-9b3e-8002-000000001951_0001_182a2ae4",
  "Version": "1.0",
  "TimeStamp": "2021-07-19T16:25:21.647Z",
  "NodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
  "NotificationMessage": "",
  "SceneMarkStatus": "Active",
  "VersionControl": {
    "VersionList": [
      {
        "VersionNumber": 1.0,
        "DateTimeStamp": "2021-07-19T16:25:21.647Z",
        "NodeID": "FirstNode"
      }
    ]
  },
  "ThumbnailList": [
    {
      "VersionNumber": 1.0,
      "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_1b0813e7"
    }
  ],
  "AnalysisList": [
    {
    "VersionNumber": 1.0,
    "EventType": "Loitering",
    "CustomEventType": "Write whatever here.",
    "AnalysisID": "0001-0002-AI2",
    "AnalysisDescription": "General Detection of Humans",
    "ProcessingStatus": "Detected",
    "ErrorMessage": "",
    "TotalItemCount": 1,
    "DetectedObjects": [
      {
      "NICEItemType": "Human",
      "CustomItemType": "",
      "ItemID": "_123_",
      "ItemTypeCount": 1,
      "Probability": 0.73,
      "Attributes":
        [
        {
        "VersionNumber": 1.0,
        "Attribute": "Mood",
        "Value": "Anger",
        "ProbabilityOfAttribute": 0.8
        }
        ],
      "BoundingBox": {
          "XCoordinate": 10,
          "YCoordinate": 30,
          "Height": 10,
          "Width": 10
          },
      "RelatedSceneData": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_e4041246"
      }]
    }],
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
      "Resolution": {"Height": 100, "Width": 100},
      "SceneDataURI": ""
    },
    {
      "VersionNumber": 1.0,
      "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_e4041246",
      "TimeStamp": "2021-07-19T16:25:21.647Z",
      "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
      "SourceNodeDescription": "Scenera Bridge",
      "DataType": "RGBStill",
      "Status": "Upload in Progress",
      "Encryption": {},
      "MediaFormat": "JPEG",
      "Resolution": {"Height": 100, "Width": 100},
      "SceneDataURI": ""
    },
    {
      "VersionNumber": 1.0,
      "SceneDataID": "SDT_00000013-60ed-9b3e-8002-000000001951_0001_eb907423",
      "TimeStamp": "2021-07-19T16:25:21.647Z",
      "SourceNodeID": "00000013-60ed-9b3e-8002-000000001951_0001",
      "SourceNodeDescription": "Scenera Bridge",
      "DataType": "RGBVideo",
      "Duration": 30,
      "Status": "Upload in Progress",
      "Encryption": {},
      "MediaFormat": "H.264",
      "Resolution": {"Height": 100, "Width": 100},
      "SceneDataURI": ""
    }
  ]
}
```
