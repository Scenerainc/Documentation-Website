---
title: Controller
date: 2022-11-12 13:25:34
slug: controller
---

**This page is under construction**

Controller is backend service responsible for managing and configuration of datapipeline of devices.

Different APIs are available in controller for configuring different appilcation templates, managing scenemode and datapipeline configuration of devices.


## ConfigureTemplateMenifest

Configuration template menifest API is used to configure configuration templates of each app. App template is used internally to identify Scenemode and Datapipeconfig template based on device type and tags respectively.


An example of request payload is shown below.

Request:
```json
{
   "AppID":"00000001-5e84-224c-8003-0000000002102", mandatory
   "SceneModeTemplates":[ mandatory
      {
         "DeviceType":[ mandatory
            "tag1",
            "tag2"
         ],
         "SceneModeTemplateID":"00000001-5cdd-280b-8003" mandatory
      }
   ],
   "DataPipelineTemplates":[ mandatory
      {
         "SourceNodeTags":[ mandatory
            "devicetype1"
         ],
         "DataPipelineConfigTemplateID":"FaceDataPipelineTemplate" mandatory
      }
   ],
   "AppControlTemplates":[ mandatory

   ]
}
```

Response:
```json
{
    "Payload": {
        "AppID": "00000001-5e84-224c-8003-0000000002102",
        "Status": "Success"
    },
    "ReplyStatusCode": 200,
    "ReplyStatusMessage": "TemplateMenifest updated successfully."
}
```

## ConfigureTemplate

Configuration template API is used to configure Scenemode and Datapipeline template. App provides different base configuration in template which is used to configure Scenemode and Datapipeconfig.


An example of request payload is shown below.

Request:
```json
{
   "DataPipelineTemplateID":"FaceDataPipelineTemplate", mandatory
   "DataPipelineInstanceID":"", mandatory
   "SourceNodeID":"", mandatory
   "DestinationNodeID":[ mandatory

   ],
   "MinimumSceneData":[ mandatory
   ],
   "DataPipelineConfig":[ mandatory
     {
        "NodeConfig":null,
        "NodeSequencerConfig":[

        ]
     }
   ]
}
```

Response:
```json
 {
  "Payload": {
      "Status": "Success",
      "TemplateID": "FaceDataPipelineTemplate"
  },
  "ReplyStatusCode": 200,
  "ReplyStatusMessage": "Template is updated with template Id FaceDataPipelineTemplate"
}
```


## SetDataPipelineConfig

SetDataPipelineConfig API is used for datapipeline configuration of device. Controller identifies template based on DeviceTag value in request payload and configure datapipeline in datapipeline facade database.


An example of request payload is shown below.

Request:
```json
{
   "DeviceID":"0000000d-6022-9058-8002-000000001593_00111", mandatory
   "AppInstanceID":[ mandatory
      "00000001-6089-220f-8003-000000000342",
      "00000001-6089-220f-8003-000000000343"
   ],
   "AppID":"00000001-5e84-224c-000000000065", mandatory
   "DeviceTag": ["Default","Default"], mandatory
   "ConfigType": "Target", mandatory
   "NotificationList":[ optional
      {
         "DestinationNodeID":"00000001-6089-220f-8003-000000000342",
         "StartTime":"01:11",
         "EndTime":"23:55",
         "RepeatDays":[
            "Monday"
         ],
         "Service":"Apple",
         "Token":"00EA7453BF34F3AFA5F2688E9E1E8AD43748F07166DFBAB8F47A7CE75FFE0E83"
      },
      {
         "DestinationNodeID":"00000001-6089-220f-8003-000000000342",
         "StartTime":"01:12",
         "EndTime":"20:51",
         "RepeatDays":[
            "Tuesday"
         ],
         "Service":"Apple",
         "Token":"00EA7453BF34F3AFA5F2688E9E1E8AD43748F07166DFBAB8F47A7CE75FFE0E83"
      },
      {
         "DestinationNodeID":"00000001-6089-220f-8003-000000000342",
         "StartTime":"20:56",
         "EndTime":"23:55",
         "RepeatDays":[
            "Friday"
         ],
         "Service":"Google",
         "Token":"fiio36wUSMehVYuHspQaPu:APA91bFq7mCg5uoP1IC7j-sLNnNJekqGdXbd9KR_LaBrHzxcvCL_8OJoP-bvUZVdz2XJgWY-UEk_LW5lp-wVuK3Omeoyo0MCdEzA17pK-YmpGXomT09GaipZ088J8y_z2j_f3_6t3gYX"
      }
   ]
}
```

Response:
```json
{
    "Payload": {
        "Status": "Created"
    },
    "ReplyStatusCode": 201,
    "ReplyStatusMessage": "DataPipelineConfig submitted successfully.",
    "Tag": "Default"
}
```

## ConfigureDeviceSceneMode

ConfigureDeviceSceneMode API is used for scenemode configuration of device in controller system. Controller identifies template based on DeviceType and SourceType value in request payload.


An example of request payload is shown below.

Request:
```json
{
   "NodeID":"00000001-619f-2365-8003-00490000021900_0001", mandatory 
   "AppID":"00000002-5eab-2e10-8003-000000000000", mandatory
   "DeviceType":"EncryptCamera", mandatory
   "SourceType":"Device", mandatory
   "SceneEncryptionKeyID":"ehubduebefneinr-ceervrjn", mandatory
   "SceneModeConfig":{ mandatory
      "Inputs":[
         
      ],
      "Mode":{
         "SceneModeConfig":[
            {
               "CustomAnalysisStage":"Falldown",
               "AnalysisRegion":[
                  {
                     "XCoord":145,
                     "YCoord":160
                  },
                  {
                     "XCoord":245,
                     "YCoord":160
                  },
                  {
                     "XCoord":245,
                     "YCoord":260
                  },
                  {
                     "XCoord":145,
                     "YCoord":260
                  }
               ],
               "AnalysisResult":{
                  
               },
               "Resolution":"1920x1080",
               "Threshold":0.7,
               "Scheduling":[
                  
               ]
            }
         ]
      }
   }
}
```

Response:
```json
{
    "Payload": {
        "Status": "Success"
    },
    "ReplyStatusCode": 200,
    "ReplyStatusMessage": "Scenemode configured successfully."
}
```

## GetSceneMode

GetSceneMode API is consumed by bridge to get device configuration.


An example of request payload is shown below.

Request:
```json
{
	"Version": "1.0", mandatory 
	"MessageType": "request", mandatory 
	"SourceEndPointID": "00000001-619f-2365-8003-004900000200_0001", mandatory 
	"DestinationEndPointID": "00000000-5eab-2e11-8003-000100000000", mandatory 
	"DateTimeStamp": "2020-09-11T04:51:50.664Z", mandatory 
	"CommandID": 0, mandatory 
	"CommandType": "GetSceneMode", mandatory 
	"Payload": {
		"NodeID": "00000001-619f-2365-8003-004900000200_0001" mandatory 
	}
}
```

Response:
```json
{
   "Version":"1.0",
   "MessageType":"request",
   "SourceEndPointID":"00000001-619f-2365-8003-004900000200_0001",
   "DestinationEndPointID":"00000002-5eab-2e3d-8003-000100000001",
   "DateTimeStamp":"2022-02-13T07:59:51.656Z",
   "CommandID":0,
   "CommandType":"GetSceneMode",
   "Payload":"{\"SceneModeID\": \"00000001-5cdd-280b-8003-000200000003\", \"NodeID\": \"00000001-619f-2365-8003-004900000200_0001\", \"Version\": \"1.0\", \"Inputs\": [], \"Outputs\": [{\"Type\": \"Video\", \"PortID\": \"00000001-619f-2365-8003-004900000200_0001_0001\", \"DestinationEndPointList\": [{\"AppEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\"}, \"NetEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"Scheme\": [{\"Protocol\": \"WebAPI\", \"Authority\": \"ingress-dev.scenera.live\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\", \"Role\": \"Client\"}]}}]}, {\"Type\": \"Image\", \"PortID\": \"00000001-619f-2365-8003-004900000200_0001_0001\", \"DestinationEndPointList\": [{\"AppEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\"}, \"NetEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"Scheme\": [{\"Protocol\": \"WebAPI\", \"Authority\": \"ingress-dev.scenera.live\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\", \"Role\": \"Client\"}]}}]}], \"Mode\": {\"SceneMode\": \"Label\", \"SceneModeConfig\": [{\"CustomAnalysisStage\": \"Falldown\", \"AnalysisRegion\": [{\"XCoord\": 145, \"YCoord\": 160}, {\"XCoord\": 245, \"YCoord\": 160}, {\"XCoord\": 245, \"YCoord\": 260}, {\"XCoord\": 145, \"YCoord\": 260}], \"AnalysisResult\": {}, \"Resolution\": \"1920x1080\", \"Threshold\": 0.7, \"Scheduling\": []}], \"AnalysisResult\": {\"Result\": \"UnDetected\", \"AdditionalInfo\": [{\"DetectedRegion\": [{\"XCoord\": 145, \"YCoord\": 160}, {\"XCoord\": 245, \"YCoord\": 160}, {\"XCoord\": 245, \"YCoord\": 260}, {\"XCoord\": 145, \"YCoord\": 260}]}]}, \"Resolution\": \"1920x1080\", \"Threshold\": 0.7, \"Scheduling\": [{\"SchedulingType\": \"ScheduledWeekDay\", \"StartTime\": \"20:00\", \"EndTime\": \"08:00\"}, {\"SchedulingType\": \"ScheduledWeekEnd\", \"StartTime\": \"00:00\", \"EndTime\": \"23:59\"}, {\"SchedulingType\": \"ScheduledHoliday\", \"StartTime\": \"00:00\", \"EndTime\": \"23:59\"}], \"SceneMarkOutputList\": [{\"AppEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\"}, \"NetEndPoint\": {\"APIVersion\": \"1.0\", \"EndPointID\": \"00000001-5cdd-280b-8003-00020000ffff\", \"Scheme\": [{\"Protocol\": \"WebAPI\", \"Authority\": \"ingress-dev.scenera.live\", \"AccessToken\": \"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCIsImtpZCI6Ik1yNS1BVWliZkJpaTdOZDFqQmViYXhib1hXMCJ9.eyJhdWQiOiJhcGk6Ly85ZmExNGI5NC0wMmFkLTRhNDMtOTU1MC04MzA1NDM0OGRkZGMiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8xMzEwMzFkNy1iOThjLTQzNWQtOGM1YS1mYTc0MDk1N2Q2MmIvIiwiaWF0IjoxNjQ0NzM4ODkxLCJuYmYiOjE2NDQ3Mzg4OTEsImV4cCI6MTY0NDgyMTk5MSwiYWlvIjoiRTJaZ1lGRGRLZER6N2JwTU1GdnA2MFdIQThwdkF3QT0iLCJhcHBpZCI6ImEzY2I0Mzc2LThkYWUtNDc2NC1iMGNhLWRjNzc3ZmNiODE1MCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzEzMTAzMWQ3LWI5OGMtNDM1ZC04YzVhLWZhNzQwOTU3ZDYyYi8iLCJvaWQiOiIzZmU4OTc3Zi1hZjg0LTQ4MTktYjRjZi05OTRkMTk2ODc4MDEiLCJyaCI6IjAuQVZnQTF6RVFFNHk1WFVPTVd2cDBDVmZXSzVSTG9aLXRBa05LbFZDREJVTkkzZHhZQUFBLiIsInJvbGVzIjpbIkFwcFJvbGUiXSwic3ViIjoiM2ZlODk3N2YtYWY4NC00ODE5LWI0Y2YtOTk0ZDE5Njg3ODAxIiwidGlkIjoiMTMxMDMxZDctYjk4Yy00MzVkLThjNWEtZmE3NDA5NTdkNjJiIiwidXRpIjoiMUJEcXU5U1doVWFoTHEtRThBTTdBQSIsInZlciI6IjEuMCJ9.de6jZxv2HXyJD_MjsnRKjd5UPg--M94pf8S14VhdSyS9O5nF3xDcHzdOp4xUbZKRZSgzNd0Huq4tJt83xHfeZZ2OsG4yAJ4SF4XjzCHrCBsnlVK7HVb016hzCdga9SzaVLUzlB5B3mH5K2SvSX8golvu3h7bj1my-JlhgyL1ZOYe3YODtJdAD1d_ZOkDWK3O5Zi8LVGtSQOBl6y3fVOuE8JFQUwNs0jSj1irQRTk_4Bljo-yKPGe3ARXg4dGqbClvJKBS5lvrjWwxiE3xPdAmpYrFDnItY22q-1s65Y6aPKMg__MsHZsjxv17H6KPG-jGel7TYaX6BqVodfCmBwLGA\", \"Role\": \"Client\"}]}}]}}",
   "ReplyStatusCode":200,
   "ReplyStatusMessage":"OK"
}
```
