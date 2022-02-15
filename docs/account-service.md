---
title: Account Service
date: 2022-11-12 13:25:34
slug: account-service
---

**This page is under construction**

Account Service in backend service to manage user, device and app configuration.

Different APIs are available in AccountService for user, device and application data manipulation.


## CreateAccount

CreateAccount API creates unique user account in AccountServce.

An example of request payload is shown below.

Request:
```json
{

}
```

Response:
```json
{
  "Status": "Success",
  "NICEAccountID": "00000002-613f-2574-8003-000000000036"
}
```


## GetAccountStatus

GetAccountStatus API provides all user account details including linked device and application information.

An example of request payload is shown below.

Request:
```json
{{
        "AccountID": "00000002-60e7-22e1-8003-000000000029" mandatory
}
```

Response:
```json
{
   "AccountID":"00000002-60e7-22e1-8003-000000000029",
   "Status":"Active",
   "Apps":[
      {
         "AppId":"00000001-5e84-224c-000000000065",
         "AppInstanceId":"00000001-610f-24c5-8003-000000000062",
         "AppStatus":[
            "Active"
         ]
      },
      {
         "AppId":"00000001-5e84-224c-000000000027",
         "AppInstanceId":"00000001-5e84-224c-000000000077",
         "AppStatus":[
            "Active"
         ]
      }
   ],
   "Devices":[
      {
         "DeviceID":"00000001-5cdd-280b-8002-00010000sd04",
         "DeviceStatus":{
            "Status":"Active",
            "ActiveApps":[
               "00000001-5e84-224c-000000000065",
               "00000001-5e84-224c-000000000027"
            ],
            "NodeList":[
               {
                  "NodeID":"00000001-5cdd-280b-8002-00010000sd04_0003",
                  "Tag":"Default",
                  "Status":"Connected",
                  "TimeZone":"Asia/Seoul",
                  "SceneModeConfig":{
                     "Inputs":[
                        {
                           "Type":"Video",
                           "VideoEndPoint":{
                              "VideoURI":"http://158.58.130.148/jpg/video.jpg"
                           }
                        }
                     ],
                     "Mode":{
                        "SceneMode":"Label",
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
                                 "Result":"UnDetected",
                                 "AdditionalInfo":[
                                    {
                                       "DetectedRegion":[
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
                                       ]
                                    }
                                 ]
                              },
                              "Resolution":"1920x1080",
                              "Threshold":0.7,
                              "Scheduling":[
                                 {
                                    "SchedulingType":"ScheduledWeekDay",
                                    "StartTime":"20:00",
                                    "EndTime":"08:00"
                                 },
                                 {
                                    "SchedulingType":"ScheduledWeekEnd",
                                    "StartTime":"00:00",
                                    "EndTime":"23:59"
                                 },
                                 {
                                    "SchedulingType":"ScheduledHoliday",
                                    "StartTime":"00:00",
                                    "EndTime":"23:59"
                                 }
                              ]
                           }
                        ]
                     }
                  },
                  "TargetAppList":[
                     "00000001-5e84-224c-000000000065",
                     "00000001-5e84-224c-000000000027"
                  ]
               }
            ]
         }
      }
   ]
}
```


## LinkApp

LinkApp API links application with user account and provide encrypted app security object in response.

An example of request payload is shown below.

Request:
```json
{
   "AccountID": "00000002-60e7-22e1-8003-000000000029", mandatory
   "AppID": "00000001-5e84-224c-000000000065", mandatory
   "public_key":"{\"Algorithm\":\"ECDH-ES+A256KW\",\"EncryptionKey\":{\"crv\":\"P-256\",\"kty\":\"EC\",\"x\":\"Eixke3GEMWZC-XZZKvjL-3uandk-mCaK0jGG8lsjSPs=\",\"y\":\"AO0u7ZzYLu46UeiOh0DBNeAZJshutMDoKA00Omnc13Uy\"},\"SigningKeyID\":\"00000002-5cdd-280b-8003-000000000000\"}"  mandatory
}
```

Response:
```json
eyJhbGciOiJSUzUxMiIsImtpZCI6IjAwMDAwMDAyLTVjZGQtMjgwYi04MDAzLTAwMDAwMDAwMDAwMCIsIng1YyI6WyJNSUlEdkRDQ0FpU2dBd0lCQWdJR0FYS0NoWGdBTUEwR0NTcUdTSWIzRFFFQkRRVUFNQ0F4SGpBY0JnTlZCQU1NRlUxaGMzUmxja3RsZVM1elkyVnVaWEpoTG1OdmJUQWdGdzB5TURBMk1EVXdNekk0TURSYUdBOHlNVEl3TVRJek1UQTRNREF3TUZvd0hERWFNQmdHQTFVRUF4TVJRVk5TYjI5MExuTmpaVzVsY3k1amIyMHdnZ0dpTUEwR0NTcUdTSWIzRFFFQkFRVUFBNElCandBd2dnR0tBb0lCZ1FDaTJkZ2hQN3krYlA2dHZrSm1tUllicVc1MFcwSk5hOUo1K0QySW1mRksrN2lwTXorRzQ0MzFieWxzUHlmdEl3amhEdkMxTWVobDNuV3dUbUtJeEJHT1ludUliRWt1cVYyLytKbWpDeW1qZCt6Z2E2SVFtKzBIZTJ0N05JcjhwVDNnMnJ3amYxZGJScllNQ1V0RENQT1dWY2VCREVuQ3FpMHUxUkpCS0p0aDZlc09UR0RVckF4MzNxVjNhbXhUNVgxWlpmSjZKZ3A2KzBsWTkrVzl1bU0rako5a2E2bEtRczJVL
```


## LinkDevice

LinkDevice API creates device AccountService database and link with user account. It supports to link multiple devices with multiple account in same request payload. If device is available in database, it will with account and perform datapipeline configuration to send scenemarks to user account.

An example of request payload is shown below.

Request:
```json
[
    {
        "AccountID": "00000002-60e7-22e1-8003-000000000029", mandatory
        "Devices" : ["00000001-5cdd-280b-8002-00010000sd04"] mandatory
    }
]
```

Response:
```json
{
  "Status": "Success",
  "Message": "Device Added Successfully."
}
```


## UnlinkDevice

UnlinkDevice API unlink device with user account. If device unlink with device owner account, device will be deleted from device database.

An example of request payload is shown below.

Request:
```json
[
    {
        "AccountID": "00000002-60e7-22e1-8003-000000000029", mandatory
        "Devices" : ["00000001-5cdd-280b-8002-00010000sd04"] mandatory
    }
]
```

Response:
```json
{
  "Status": "Success",
  "Message": "Device unlinked Successfully."
}
```


## ConfigureDevices

ConfigureDevices API is used to configure device node. It can do multiple nodes management(Add/Update/Delete) task parrellaly in single request.

An example of request payload is shown below.

Request:
```json
{
   "AccountID":"00000002-60e7-22e1-8003-000000000029",
   "Devices":[
      {
         "DeviceID":"00000001-5cdd-280b-8002-00010000sd04",
         "DeviceStatus":{
            "Status":"Active",
            "ActiveApps":[
               "00000001-5eab-2e3d-8003-000100000001"
            ],
            "NodeList":[
               {
                  "NodeID":"00000001-5cdd-280b-8002-00010000sd04_0001",
                  "ConfigureStatus":"Added",
                  "DeviceType" : "RGBCamera",
                  "Tag": ["SIDDHARTH","Default"],
                  "Status":"Connected",
                  "TimeZone":"Asia/Sul",
                  "SceneModeConfig":{
                     "Inputs":[
                        {
                           "Type":"Video",
                           "VideoEndPoint":{
                              "VideoURI":"http://158.58.130.148/jpg/video.jpg"
                           }
                        }
                     ],
                     "Mode":{
                        "SceneMode":"Label",
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
                                 "Result":"UnDetected",
                                 "AdditionalInfo":[
                                    {
                                       "DetectedRegion":[
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
                                       ]
                                    }
                                 ]
                              },
                              "Resolution":"1920x1080",
                              "Threshold":0.7,
                              "Scheduling":[
                                 {
                                    "SchedulingType":"ScheduledWeekDay",
                                    "StartTime":"20:00",
                                    "EndTime":"08:00"
                                 },
                                 {
                                    "SchedulingType":"ScheduledWeekEnd",
                                    "StartTime":"00:00",
                                    "EndTime":"23:59"
                                 },
                                 {
                                    "SchedulingType":"ScheduledHoliday",
                                    "StartTime":"00:00",
                                    "EndTime":"23:59"
                                 }
                              ]
                           }
                        ]
                     }
                  }
               }
            ]
         }
      }
   ]
}
```

Response:
```json
{
  "Status": "Success",
  "Message": "Devices Configured successfully."
}
```


## UnlinkApp

UnlinkApp API unlinks application with user account.

An example of request payload is shown below.

Request:
```json
{
"AccountID": "00000002-60e7-22e1-8003-000000000029",
"AppID": "00000002-60e7-22e1-8003-000000000000",
"AppInstanceID": "00000001-60e7-2310-8003-000000000016"
}
```

Response:
```json
{
  "Status": "Success",
  "Message": "App unlinked Successfully."
}
```

## GetNotifications

GetNotifications API provides scenemark notification details to app. 

An example of request payload is shown below.

Request:
```json
{
    "Version": "1.0",  mandatory
    "MessageType": "request", mandatory
    "SourceEndPointID": "00000001-609b-2978-8003-000000000005", mandatory
    "DestinationEndPointID": "00000000-5eab-2e10-8003-000000000000", mandatory
    "DateTimeStamp": "2020-08-09T06:39:31:000000", mandatory
    "CommandID": 0, mandatory
    "CommandType": "/1.0/00000000-5eab-2e10-8003-000000000000/management/GetNotification", mandatory
    "Payload": {
        "AppInstanceID": "00000001-609b-2978-8003-000000000005", mandatory
        "SourceNodeID": "00000001-5cdd-280b-8002-00010000sd02_0002", mandatory
        "NotificationService":"iOS" mandatory
    }
}
```

Response:
```json
{
    "Version": "1.0",
    "MessageType": "response",
    "SourceEndPointID": "00000001-609b-2978-8003-000000000005",
    "DestinationEndPointID": "00000000-5eab-2e10-8003-000000000000",
    "DateTimeStamp": "2021-9-13T14:10:42:000000",
    "ReplyID": 0,
    "ReplyStatusCode": 200,
    "ReplyStatusMessage": "OK",
    "Payload": {
        "AppInstanceID": "00000001-609b-2978-8003-000000000005",
        "NotificationService": "iOS",
        "SourceNodeID": "00000001-5cdd-280b-8002-00010000sd02_0002",
        "Schedule": [],
        "Enabled": false
    }
}
```

## ConfigureNotifications

ConfigureNotifications API enable/disable notifications of application.

An example of request payload is shown below.

Request:
```json
{
   "Version":"1.0", mandatory
   "MessageType":"request", mandatory
   "SourceEndPointID":"00000001-609b-2978-8003-000000000005", mandatory
   "DestinationEndPointID":"00000002-5eab-2e11-8003-000000000000", mandatory
   "DateTimeStamp":"2020-08-09T06:39:31:000000", mandatory
   "CommandID":0,
   "CommandType":"/1.0/00000002-5eab-2e11-8003-000000000000/management/ConfigureNotifications", mandatory
   "Payload":{
      "AppInstanceID":"00000001-609b-2978-8003-000000000005", mandatory
      "SourceNodeID" : "00000001-5cdd-280b-8002-00010000sd02_0003", mandatory
      "NotificationService":"Android", mandatory
      "Enabled" : true, mandatory
      "Token": "dummy-token4" mandatory
   }
}
```

Response:
```json
{
    "Version": "1.0",
    "MessageType": "response",
    "SourceEndPointID": "00000001-609b-2978-8003-000000000005",
    "DestinationEndPointID": "00000002-5eab-2e11-8003-000000000000",
    "DateTimeStamp": "2021-9-13T14:12:10:000000",
    "ReplyID": 0,
    "ReplyStatusCode": 200,
    "ReplyStatusMessage": "OK",
    "Payload": {
        "AppInstanceID": "00000001-609b-2978-8003-000000000005",
        "Status": "Success"
    }
}
```


## SetNotifications

By defaut application gets all notifications. SetNotifications API is used to schedule scenemark notification in application. 

An example of request payload is shown below.

Request:
```json
{
   "Version":"1.0", mandatory
   "MessageType":"request", mandatory
   "SourceEndPointID":"00000001-609b-2978-8003-000000000005", mandatory
   "DestinationEndPointID":"00000002-5eab-2e11-8003-000000000000", mandatory
   "DateTimeStamp":"2020-08-09T06:39:31:000000", mandatory
   "CommandID":0, mandatory
   "CommandType":"/1.0/00000002-5eab-2e11-8003-000000000000/management/SetNotifications", mandatory
   "Payload":{
      "AppInstanceID":"00000001-609b-2978-8003-000000000005", mandatory
      "NotificationService":"Andriod", mandatory
      "NotificationEndPoint":"", mandatory
      "SourceNodeID":"00000001-5cdd-280b-8002-00010000sd02_0002", mandatory
      "Schedule":[ Optional
         {
            "StartTime":"03:00",
            "EndTime":"23:56",
            "ScheduledDays":[
               "Monday",
               "Tuesday"
            ]
         },
          {
            "StartTime":"04:00",
            "EndTime":"23:56",
            "ScheduledDays":[
               "Thursday",
               "Wednesday"
            ]
         }
      ]
   }
}
```

Response:
```json
{
    "Version": "1.0",
    "MessageType": "response",
    "SourceEndPointID": "00000001-609b-2978-8003-000000000005",
    "DestinationEndPointID": "00000002-5eab-2e11-8003-000000000000",
    "DateTimeStamp": "2021-9-13T14:11:21:000000",
    "ReplyID": 0,
    "ReplyStatusCode": 200,
    "ReplyStatusMessage": "OK",
    "Payload": {
        "AppInstanceID": "00000001-609b-2978-8003-000000000005",
        "SourceNodeID": "00000001-5cdd-280b-8002-00010000sd02_0002",
        "Status": "Success"
    }
}
```

## GetAccountNode

GetAccountNode API returns details of all device nodes which are linked with user account.

An example of request payload is shown below.

Request:
```json
{
    "AccountID": "00000002-60e7-22e1-8003-000000000029", mandatory
    "AppID" : "00000001-5e84-224c-000000000027", optional
    "AppInstanceID" : "00000001-5e84-224c-000000000077" mandatory
}
```

Response:
```json
{
    "Version": "1.0",
    "AccountID": "00000002-60e7-22e1-8003-000000000029",
    "NodeList": []
}
```


## GetAppControlObject

GetAppControlObject API provides latest app security object with all tokens and endpoint details.

An example of request payload is shown below.

Request:
```json
{
    "Version": "1.0", mandatory
    "MessageType": "request", mandatory
    "SourceEndPointID": "00000001-5e84-224c-000000000065", mandatory
    "DestinationEndPointID": "00000000-5eab-2e10-8003-000000000000", mandatory
    "DateTimeStamp": "2020-08-09T06:39:31:000000", mandatory
    "CommandID": 0,
    "CommandType": "/1.0/00000000-5eab-2e10-8003-000000000000/management/GetAppControlObject", mandatory
    "Payload": {
        "AppID": "00000001-5e84-224c-0000-00000108" mandatory
    }
}
```

Response:
```json
{
   "Version":"1.0",
   "MessageType":"response",
   "SourceEndPointID":"",
   "DestinationEndPointID":"00000002-5eab-2e10-8003-000000000000",
   "DateTimeStamp":"2021-9-20T15:2:38:000000",
   "ReplyID":0,
   "ReplyStatusCode":200,
   "ReplyStatusMessage":"OK",
   "Payload":{
      "Version":"1.0",
      "AppID":"00000002-5eab-2e10-8003-000000000000",
      "AppInstanceID":"00000001-5e84-224c-0000-00000108",
      "ControlEndPoints":[
         {
            "AppEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e10-8003-000000000000",
               "X.509Certificate":"",
               "AccessToken":""
            },
            "NetEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e10-8003-000000000000",
               "Scheme":[
                  {
                     "Protocol":"WebAPI",
                     "Authority":"niceas-dev.scenera.live",
                     "Role":"Client",
                     "AccessToken":""
                  }
               ]
            }
         }
      ],
      "DataEndPoints":[
         {
            "AppEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e3d-8003-000100000001",
               "X.509Certificate":"",
               "AccessToken":""
            },
            "NetEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e3d-8003-000100000001",
               "Scheme":[
                  {
                     "Protocol":"WebAPI",
                     "Authority":"ns-dev.scenera.live",
                     "Role":"Client",
                     "AccessToken":""
                  }
               ]
            }
         }
      ],
      "NotificationEndPoints":[
         {
            "AppEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e10-8003-000000000000",
               "X.509Certificate":"",
               "AccessToken":""
            },
            "NetEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e10-8003-000000000000",
               "Scheme":[
                  {
                     "Protocol":"WebAPI",
                     "Authority":"scenerasec1.southafricanorth.cloudapp.azure.com",
                     "Role":"Client",
                     "AccessToken":""
                  }
               ]
            }
         }
      ]
   }
}
```


## GetControlObject

GetControlObject provides data security object which contains all endpoint and token details to device.

An example of request payload is shown below.

Request:
```json
{
    "Version": "1.0", mandatory
    "MessageType": "request", mandatory
    "SourceEndPointID": "00000005-6116-005b-8002-00000000002b", mandatory
    "DestinationEndPointID": "00000000-5eab-2e10-8003-000000000000", mandatory
    "DateTimeStamp": "2020-08-09T06:39:31:000000", mandatory
    "CommandID": 0, mandatory
    "CommandType": "/1.0/00000000-5eab-2e10-8003-000000000000/management/GetControlObject", mandatory
    "Payload": {
        "DeviceID": "00000005-6116-005b-8002-00000000002b" mandatory
    }
}
```

Response:
```json

   "Version":"1.0",
   "MessageType":"response",
   "SourceEndPointID":"00000005-6116-005b-8002-00000000002b",
   "DestinationEndPointID":"00000000-5eab-2e10-8003-000000000000",
   "DateTimeStamp":"2021-9-20T15:30:46:000000",
   "ReplyID":0,
   "ReplyStatusCode":200,
   "ReplyStatusMessage":"OK",
   "Payload":{
      "DeviceID":"00000005-6116-005b-8002-00000000002b",
      "Version":"1.0",
      "ControlEndPoints":[
         {
            "AppEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e10-8003-000000000000",
               "X.509Certificate":[
                  "MIIDvDCCAiSgAwIBAgIGAXKChXgAMA0GCSqGSIb3DQEBDQUAMCAxHjAcBgNVBAMMFU1hc3RlcktleS5zY2VuZXJhLmNvbTAgFw0yMDA2MDUwMzI4MDRaGA8yMTIwMTIzMTA4MDAwMFowHDEaMBgGA1UEAxMRQVNSb290LnNjZW5lcy5jb20wggGiMA0GCSqGSIb3DQEBAQUAA4IBjwAwggGKAoIBgQCi2dghP7y+bP6tvkJmmRYbqW50W0JNa9J5+D2ImfFK+7ipMz+G4431bylsPyftIwjhDvC1Mehl3nWwTmKIxBGOYnuIbEkuqV2/+JmjCymjd+zga6IQm+0He2t7NIr8pT3g2rwjf1dbRrYMCUtDCPOWVceBDEnCqi0u1RJBKJth6esOTGDUrAx33qV3amxT5X1ZZfJ6Jgp6+0lY9+W9umM+jJ9ka6lKQs2U/H9zr6fSfVvc+NQewpt3L5yQkunJyXel6jZVraUMBaFSwkhPuEBMSDkIR3PrziM8R03F3HHCvA/Kq5JX6HljoVOMa+3ggwiW4OcAmrl1qmtNd3tgBKdul7Q73IYb1oQ8w6dcmfQ5K/liQU6HREFGVtPtmxm5ecUfw1l/ZP4yGBq7VXiBg5IdgtdIbWk+nJ+In4/1klG9TgPjub/ppFOPB4v4ql6h+gfFZJ9ajZe8rnyYKCYzHXDpCkC4nBZkpWt+0kcz/t5JVnzT4Je0zoT9EXJYDzt8OC0CAwEAATANBgkqhkiG9w0BAQ0FAAOCAYEAm4/xl6y210c+FKRBCTLxCGDmjnG5H9+CT2Vt6+ouBJnbN6PtpgI/5fS1dUJcrRJFfJsZ3ZqyrTmQcm1INdudZ9y9FjDQRfNHc3jvzaFk6LFm+qJPbIoR4K/0twaIQQPKl48WbdLAh3Kxvz49vRMpl5RMVE0Z6JF3YhtyBber0Zvn1/JPN70h18r2JK5SHiMpJ0pDOQnEZmCFgV6dG5W6ErF5cWNlhydTD5u6RcX+baAt/II8aOEoAodhbFKT+i4QCFGnsnDif4UrQwNYuWuwa+pwA/dITRnzmp4TzSxhnii7AGn0XuuXRoLfm0uCP5Am4DmI3Ebef/MutqPDbtI6SNfFYdp0+MRRgo4GSmRUQts/i4gRtgeAaL1zlgBysapcIxtt4qHU/YjOyNhJCHH5s7HUAWF7dgmXSwjkhxmDSj7BI872u6bYwEwTv5OqyasxOrDR/kb7UJvOLUb1+u2xFkaeNsQJA5I2Kjv3JiD/AUcOByyAYd0cOpscRX/g3WMa"
               ],
               "AccessToken":".eyJWZXJzaW9uIjoiMS4wIiwiRW5mb3JjZUVuY3J5cHRpb24iOnRydWUsImlzcyI6IjAwMDAwMDAyLTVlYWItMmUxMC04MDAzLTAwMDAwMDAwMDAwMCIsInN1YiI6IjAwMDAwMDA1LTYxMTYtMDA1Yi04MDAyLTAwMDAwMDAwMDAyYiIsImF1ZCI6IjAwMDAwMDAyLTVlYWItMmUzZC04MDAzLTAwMDEwMDAwMDAwMSIsImlhdCI6MTYzMjEzMjA2MSwibmJmIjoxNjMyMTMyMDYxLCJleHAiOjE2MzIyMTg0NjEsImp0aSI6Imp0aSIsIlBlcm1pc3Npb25zIjpbIk1hbmFnZW1lbnQiXX0.bYnUhjMqQNwcxhgznsT33iHuoU1LSZKh1SJycxC5oAOoExLQ2Qp2GFMGIRx1qQVR5iXBxOE4xIrnEVfGeA5Rcet9ux7w_ap1qvO8K25pKqg_8lYysw-WdxKlEhsKCC_C6r6Gwt4eScZyDidBaMufvwtQskYuaPHmt9demsIH2nmEaCZtrqTL1Y7-oR9KKny4JFYXge_L6h47W8F83W-s2icZR74exhwU1t_zaJm28XFtnY_ajOhxqsWveZtxt3zRGE667xXi8Lg4BOpfzBnFSda6SyZ5RSkqRbeWXg1VoAHD-VIrfm3z3waKKbe3ym0z274KedGZxlhvsNTOkd2OZeE-fmGaiNr9-AdSax-PJ9SaWIi8vMF8NaivYTiCgRQ0HOm5AqHHccM6jiCh1IiDwUhaSCxmFYGOQEhUtjn8LXNC8dYEWmfCrbKFg2HAMNv1UDWs0OhJpbBd0TWl8za_wrYieNvULn0EdxHg5yr6taxW2N8B_H1L6lXWgi-83EaE"
            },
            "NetEndPoint":{
               "APIVersion":"1.0",
               "EndPointID":"00000002-5eab-2e3d-8003-000100000001",
               "Scheme":[
                  {
                     "Protocol":"WebAPI",
                     "Authority":"scenera-pipelinecontroller-dev.scenera.live",
                     "Role":"Client",
                     "AccessToken":".eyJWZXJzaW9uIjoiMS4wIiwiRW5mb3JjZUVuY3J5cHRpb24iOnRydWUsImlzcyI6IjAwMDAwMDAyLTVlYWItMmUxMC04MDAzLTAwMDAwMDAwMDAwMCIsInN1YiI6IjAwMDAwMDA1LTYxMTYtMDA1Yi04MDAyLTAwMDAwMDAwMDAyYiIsImF1ZCI6IjAwMDAwMDAyLTVlYWItMmUzZC04MDAzLTAwMDEwMDAwMDAwMSIsImlhdCI6MTYzMjEzMjA2MSwibmJmIjoxNjMyMTMyMDYxLCJleHAiOjE2MzIyMTg0NjEsImp0aSI6Imp0aSIsIlBlcm1pc3Npb25zIjpbIk1hbmFnZW1lbnQiXX0.bYnUhjMqQNwcxhgznsT33iHuoU1LSZKh1SJycxC5oAOoExLQ2Qp2GFMGIRx1qQVR5iXBxOE4xIrnEVfGeA5Rcet9ux7w_ap1qvO8K25pKqg_8lYysw-WdxKlEhsKCC_C6r6Gwt4eScZyDidBaMufvwtQskYuaPHmt9demsIH2nmEaCZtrqTL1Y7-oR9KKny4JFYXge_L6h47W8F83W-s2icZR74exhwU1t_zaJm28XFtnY_ajOhxqsWveZtxt3zRGE667xXi8Lg4BOpfzBnFSda6SyZ5RSkqRbeWXg1VoAHD-VIrfm3z3waKKbe3ym0z274KedGZxlhvsNTOkd2OZeE-fmGaiNr9-AdSax-PJ9SaWIi8vMF8NaivYTiCgRQ0HOm5AqHHccM6jiCh1IiDwUhaSCxmFYGOQEhUtjn8LXNC8dYEWmfCrbKFg2HAMNv1UDWs0OhJpbBd0TWl8za_wrYieNvULn0EdxHg5yr6taxW2N8B_H1L6lXWgi-83EaE"
                  }
               ]
            }
         }
      ],
      "RevokedJSONTokenIDs":[

      ],
      "AllowedTLSRootCertificates":[

      ]
   }
}
```

