---
title: Android App Setup
date: 2022-03-28
slug: android-app-setup
---

# THIS PAGE IS UNDER CONSTRUCTION #
## Implement the Scenera Library into a new Android Project ##

1. To use JitPack with private repositories get your personal access token to use the library in your project.
  * For this example, we will use this as our access token: ``` jp_dbku18oktekp0aj72fgv9h9bm2 ```
2. Use this access token as the &lt;username\> in your project’s *build.gradle* file like:
```
allprojects {    
   repositories {    
       google()   
       jcenter()   
       maven {    
           url "https://jitpack.io"   
           credentials { username ="jp_dbku18oktekp0aj72fgv9h9bm2"}    
       }   
   }   
}  
```

3. Add the Library dependency in your module’s *build.gradle* file:
  * This is the sample library :```implementation 'com.github.awajs:appsecuritysdk:<Tag>'```
    * Note: &lt;Tag\> will be the latest version name of the library
```
dependencies {    
   implementation fileTree(dir: 'libs', include: ['*.jar'] ) 
   implementation 'com.github.awajs:appsecuritysdk:v6.2'   
   implementation 'androidx.appcompat:appcompat:1.2.0'   
   implementation 'androidx.constraintlayout:constraintlayout:2.0.4'   
} 
```
  * Note: Build artifacts (jar, aar) are also private and can only be downloaded if you have access to the Git repo itself.


### 1. Link BSS Account to App ###
  * The first step is to link your BSS account with the Android Application. Call the library’s *BSSLoginActivity.class* like the following example:
```
Intent intent = new Intent(MainActivity.this, BSSLoginActivity.class);
startActivityForResult(intent, MY_REQUEST_CODE);
```
  * After successful login, the *AppSecurityObject* and *AppControlObject* will be added to the library’s shared preference variables which you can now use further in the project
  * Once login is successful, redirect from the library’s activity to the developer’s activity to perform next steps. For example:
  ```
@Override   
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {   
   super.onActivityResult(requestCode, resultCode, data);   
   if(requestCode == MY_REQUEST_CODE) {   
       if(resultCode == RESULT_OK) {   
           Intent intent = new Intent(this, HomeActivity.class);   
           startActivity(intent);   
       }   
   }   
}  
  ```

  * Here, *HomeActivity.class* is the app developer’s activity to redirect the user after successful login from library’s activity
  * Here's an example of the developer’s *BSSLoginActivity*:
  ``` 
public class MainActivity extends BaseActivity {    
 
    private final static int MY_REQUEST_CODE =  1;    
    @Override   
    protected void onCreate(Bundle savedInstanceState) {   
        super.onCreate(savedInstanceState);   
        setContentView(R.layout.activity_main_screen);   
   
        Intent intent = new Intent(MainActivity.this, BSSLoginActivity.class);   
        startActivityForResult(intent, MY_REQUEST_CODE); 
    }   
      
    @Override   
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {   
        super.onActivityResult(requestCode, resultCode, data);   
        if(requestCode == MY_REQUEST_CODE){   
            if(resultCode == RESULT_OK) {   
                Intent intent = new Intent(this, HomeActivity.class);   
                startActivity(intent);   
            }   
        }   
    }   
}
  ```

### 2. GetNodeList ###
  * After successful BSS login, the next step is to get the node list.
  * The *MainViewModel.class* ﬁle contains all the API calling functions which developers will need.
  * To call the *nodeList* API, first create an instance of MainViewModel Class:
  ```
  MainViewModel mainViewModel;
  // Get the ViewModel.
  mainViewModel = new ViewModelProvider(this).get(MainViewModel.class;
  ```
  * Then, call the node listing API:
  ```
  mainViewModel.getNodeList(this);
  ```
  * Get the response string of the node list by implementing an observer for each API function call.
  * To update UI for node list and get the response from library API call, call the observer:
  ```
mainViewModel.getDeviceList().observe(activity, new Observer<ArrayList<NodeList>>(){   
    @Override   
    public void onChanged(ArrayList<NodeList> nodeLists) {   
 
        if (nodeLists.size() > 0) {   
            nodeList.addAll(nodeLists);   
            Log.i("nodeListSize=> ", nodeList.size() + "");   
            Log.i("nodeListArray=> ", nodeList.toString() + ""); 
        }   
    }
});  
  ```
  * In this example, the *getDeviceList()* function from the library will return *nodeLists* which can be listed in their own UI. 

### 3. GetNICEItemTypes ###
  * After getting *NodeLists*, call the API to list all *NiceItemTypes*
  * Call the *NiceItemTypes* API as follows:
  ```
  mainViewModel.getNiceItemTypesList(this);
  ```
  * To update the UI for *niceitemtypes* list, and get the response from the library API call, call the observer like this:
  ```
mainViewModel.getNiceItemTypes().observe(HomeActivity.this, new Observer<ArrayList<String>>() 
{   
    @ Override   
    public void onChanged(ArrayList<String> niceItemsList) {   
        if (nodeLists.size() > 0) {   
            niceItems = niceItemsList;   
            Log.i("niceItems=> ", nodeList.toString() + ""); 
        }
    }   
}); 
  ```
  * Here, the *getNiceItemTypes()* function will return a list of *niceItemTypes* that can be use to list niceItems in the UI.  

### 4. GetSceneMarkManifest ###
  * After getting  *NiceItemTypes* call the API to list the first 10 *SceneMarkManifest* objects
  * These are the Parameter definitions for the *GetSceneMarkManifest* Service:
```  
  "NodeIDs": {  
    "type": "array",  
    "description": "All the devices available in bss account"  
  }  
  "StartTime": {  
    "type": "string",  
    "description": "date which user selected or date somewhere is past from current date"  
  }  
  "EndTime": {  
    "type": "string",  
    "description": "date string of tomorrow's date"  
  }  
  "PageLength": {  
    "type": "integer",  
    "description": "specifies limit to list total scenemarks"  
  }  
  ReturnNICEItemTypes": {  
    "type": "boolean",  
    "description": "set it to true for listing all the available niceItems" 
  }  
  "ReturnSceneMarkDates": {  
    "type": "boolean",  
    "description": "set it to true for listing all the available dates on which scenemarks  available"  
  }  
  ReturnPage": {  
    "type": "boolean",  
    "description": "set it to true for listing all the available scenemarks for specified  pagelength. also can use ReturnPage to get the next page. set it to false to get full list"  
  }  
  "ListNICEItemTypes": {  
    "type": "array",  
    "description": "NICE defines diferent DeviceModes which target specific types of data  associated with the DeviceMode."  
    "NICEItemTypesPresent": {  
      "type": "string",  
      "enum": [  
        "Motion",  
        "Face",  
        "Human",  
        "Vehicle",  
        "Label",  
        "Text/Logo>QRCode",  
        "Animal"  
    ]  
  }  
  "ContinuationToken": { 
    "type": "string",  
    "description": "token to get next scenemarks for next page"  
  }
```
 
  * call the *SceneMarksManifest* API:
  ``` 
private void getSceneMarksManifest(){   
    mainViewModel.getSceneMarksManifest(activity, nodeIdArrayList, "2010-08-25T03:17:53.1179276Z", "2022-03-31T03:17:53.1179276Z", 10, true, true, true, selectedNiceItemList, null);   
} 
  ```
**When calling ContinuationToken shell for the first time, pass a null value.**
**Not sure what this means?**
  * To get the response of SceneMarksManifest from the library API call, call the observer:
  ```
mainViewModel.getSceneMarkManifestLiveData().observe(getViewLifecycleOwner(), new Observer<GetSceneMarkManifestResponse>() {   
    @Override   
    public void onChanged(GetSceneMarkManifestResponse getSceneMarkManifestResponse) 
    {   
        ArrayList<SceneMarkList> sceneMarkLists = getSceneMarkManifestResponse.getSceneMarkList();   
        Log.d("sceneMarkList: ", sceneMarkLists.size() + "");   
        continuationToken = getSceneMarkManifestResponse.getContinuationToken();   
        Log.d("continuationToken: ", continuationToken);   
    }
}
  ```
  * Here, the  *getSceneMarkManifestLiveData()* function will return a list of *sceneMarksManifest*s
  * The *ContinuationToken* must be saved in your code and passed to every subsequent page request call for *sceneMarksManifest*s.
  * For example, to load the next 10 *sceneMarksManifest*s after the user scrolls past 10 scenemarks, the API request call will look like this:
  ```
private void getSceneMarksManifest(){   
    mainViewModel.getSceneMarksManifest(activity, nodeIdArrayList, "2010-08-25T03:17:53.1179276Z", "2022-03-31T03:17:53.1179276Z", 10, true, true, true, selectedNiceItemList, continuationToken);
}   
  ```
  * Here, the *ContinuationToken* saved in the first request call should be passed. It will return in the response of the *GetSceneMarkManifest* API call.

  Sample response of GetSceneMarksManifest api call:
  ```
  {  
  "Version": "1.0",   
  "StartDateTime": "2010-08-25T03:53.117Z",   
  "EndDateTime": "2021-01-15T03:53.117Z",   
  "PageLength": 1,   
  "NICEItemTypesPresent": {  
    "Human" : 7  
  },  
  "ListDates": [  
    "2021-01-15"  
  ],  
  "SceneMarkList": [  
    {  
    "SceneMarkID": "SMK_00000001-5cdd-280b-8002-00010000f3e0_0001_00064c9a",    
    "NodeID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
    "SceneMarkURI": "https://stagingenvnodesequencer.scenera.live/1.0/00000001-5e84-224c-8003- 
    000000000065/GetSceneMark/SMK_00000001-5cdd-280b-8002-00010000f3e0_0001_00064c9a",   
    "TimeStamp" : "2021-01-15T03:51:19.863Z",   
    "SceneDataThumbnail": {  
      "SceneModeDetectionType": "Human" ,  
      "SceneDataThumbnailURI": "https://stagingenvsd1.blob.core.windows.net:443/00000001-5cdd-280b-8002-00010000f3e0-0001/003efe05.jpeg?sv=2019-07-07&st=2021-01-19T06%3A52%3A38Z&se=2021-01-19T07%3A33%3A10Z&sr=b&sp=r&sig=i9bIBiHVRm68XVj32LXbhHzvLiSS5ImJ7fFrDanRvHA%3D",    
      "EncryptionOn": true,   
      "SceneEncryptionKeyID": "0000000000001"  
    }  
  }  
  ],  
  "ContinuationToken": "[{\"token\":\"+RID:~3ts2AIVXTRVV7AAAAAAAAQ==#RT:1#TRC:1#RTD:pInRkQDE/WRQPdWYJzqRBTMxMzIuMTIuMjZVMTQ7NjI7MjovOTc0WwA=#ISV:2#IEO:65551#QCF:1#FPC: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\",\"range\":{\"min\":\"05C1BDD37D7BE0\",\"max\":\"05C1CB337B2DC0\"}}]" } 
  ```

### 5. GetSceneMark ###
  * After getting the *GetSceneMarksManifest* list, make a &lt;GET> call for SceneMarks and SceneData.
  * Retreive the *SceneMarkURI* from the *GetSceneMarksManifest* API call response.
  * Call the *SceneMarks* API as follows: 
  ```
  mainVM.getLiveSceneMarks(activity, sceneMarkURI)
  ```
  * To get the response of *SceneMarks* from the API call, call the observer:
  ```
mainVM.getAlertLiveData().observe(getViewLifecycleOwner(), new Observer<SceneMarkResponseCMF>() {   
    @Override   
    public void onChanged(SceneMarkResponseCMFsceneMarkResponseCMF){   
        Log.d("Observer SceneMarksLive...", sceneMarkResponseCMF + "");   
    }   
});
  ```
  * Here, the *getAlertLiveData()* function from the library will return *SceneData* information.
  * Sample *SceneData* Response:
  ```
  {
  "Version": "1.0",   
  "TimeStamp" : "2021-01-15T03:51:19.863Z",   
  "SceneMarkID": "SMK_00000001-5cdd-280b-8002-00010000f3e0_0001_00064c9a",  
  "DestinationID": "00000001-5cdd-280b-8003-00020000ffff",   
  "SceneMarkStatus": "Active",   
  "NodeID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
  "PortID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
  "VersionControl": {  
    "DataPipelineInstanceID": "00000001-5cdd-280b-8003-000200000003",   
    "VersionList" : []  
  },  
  "ThumbnailList": [
    {  
    "VersionNumber": 1.0,   
    "SceneDataID": "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe05"  
    }
  ],  
  "AnalysisList": [
    {
    "VersionNumber": 1.0,   
    "SceneMode" : "Human" ,  
    "CustomAnalysisID" : "",   
    "AnalysisDescription": "Yolo v3 configured to detect Human",   
    "ProcessingStatus": "Detect",  
    "EXIFData": null  
    }
  ],  
  "DetectedObjects":  [
    {  
    "VersionNumber": 0.0,   
    "NICEItemType": "Human" ,  
    "CustomItemType": "",   
    "ItemID": null ,  
    "Probability" : 0.0,   
    "Analysis" : null ,  
    "Attributes": null ,  
    "BoundingBox":  
      {
      "XCoordinate": 414,   
      "YCoordinate": 166,   
      "Height": 186,
      "Width": 40  
      },  
    "ThumbnailSceneDataID": "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe05",  
    "RelatedSceneData": 
      [
      "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe04","SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe06"
      ]  
    }
  ],  
  "ParentSceneMarks": null,  
  "ChildSceneMarks": null,  
  "SceneDataList": [
    {  
    "SceneDataID": "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe05",  
    "TimeStamp": "2021-01-15T03:51:19.863Z",   
    "SourceNodeID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
    "SourceNodeDescription": "Scenera Bridge - NVidia Jetson Nano",   
    "Duration": null ,  
    "DataType": "RGBStill" ,  
    "Status": "Available at Provided URI",   
    "MediaFormat": "JPEG",   
    "SceneDataURI": "https://stagingenvsd1.blob.core.windows.net/00000001-5cdd-280b-8002-00010000f3e0-0001/003efe05.jpeg?sv=2019-07-07&st=2021-01-19T07%3A02%3A12Z&se=2021-01-19T07%3A42%3A44Z&sr=b&sp=r&sig=1zz8%2F3q0x3o4HOOc3qAXe6iIgV3MWi2nvFDWcuFi8lY%3D",
    "EmbeddedSceneData": null ,  
    "Encryption":
      {  
      "EncryptionOn": true,
      "SceneEncryptionKeyID": "0000000000001",   
      "PrivacyServerEndPoint": 
        {  
        "AppEndPoint": null ,  
        "NetEndPoint":  
          {  
          "APIVersion": "1.0",   
          "EndPointID": "00000000-5cdd-280b-8003-000000000000",   
          "NodeID": null , 
          "PortID": null ,  
          "Scheme": [
            {
            "Protocol": "WebAPI",   
            "Authority": "niceas.scenera.live",   
            "AccessToken": "eyJ0eXAiOiJK....U7qunXZg",   
            "Role": "Client",   
            "ValidationKey": null  
            }  
          ]  
          }  
        }  
      }  
    },  
    {  
    "SceneDataID": "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe04",  
    "TimeStamp" : "2021-01-15T03:51:19.863Z",   
    "SourceNodeID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
    "SourceNodeDescription": "Scenera Bridge - NVidia Jetson Nano",   
    "Duration": null,  
    "DataType": "RGBStill" ,  
    "Status": "Available at Provided URI",   
    "MediaFormat": "JPEG",   
    "SceneDataURI": "https://stagingenvsd1.blob.core.windows.net/00000001-5cdd-280b-8002-00010000f3e0-0001/003efe04.jpeg?sv=2019-07-07&st=2021-01-19T07%3A02%3A12Z&se=2021-01-19T07%3A42%3A44Z&sr=b&sp=r&sig=Jb8AWHQOOEXO67AixyN0CpEkRJZdtkVR2KqeteoyJH4%3D",
    "EmbeddedSceneData": null ,  
    "Encryption":  
      {  
      "EncryptionOn": true,
      "SceneEncryptionKeyID": "0000000000001",   
      "PrivacyServerEndPoint":
        {
        "AppEndPoint": null ,  
        "NetEndPoint":
          {  
          "APIVersion": "1.0",   
          "EndPointID": "00000000-5cdd-280b-8003-000000000000",   
          "NodeID": null,  
          "PortID": null,
          "Scheme": [
            {  
            "Protocol": "WebAPI",
            "Authority": "niceas.scenera.live",   
            "AccessToken": "eyJ0eXAiOiJK....U7qunXZg",   
            "Role": "Client",
            "ValidationKey": null
            }  
            ]
          }  
        }  
      }  
    }, 
    {  
    "SceneDataID": "SDT_00000001-5cdd-280b-8002-00010000f3e0_0001_003efe06",  
    "TimeStamp": "2021-01-15T03:51:19.863Z",   
    "SourceNodeID": "00000001-5cdd-280b-8002-00010000f3e0_0001" ,  
    "SourceNodeDescription": "Scenera Bridge - NVidia Jetson Nano",   
    "Duration": "10",   
    "DataType": "RGBVideo",   
    "Status": "Available at Provided URI",   
    "MediaFormat": "H.264",   
    "SceneDataURI": "https://stagingenvsd1.blob.core.windows.net/00000001-5cdd-280b-8002-00010000f3e0-0001/003efe06.mp4?sv=2019-07-07&st=2021-01-19T07%3A02%3A12Z&se=2021-01-19T07%3A42%3A44Z&sr=b&sp=r&sig=zfN1n64o%2FfHLeROOS3GYFL2vuItv4P88jtybomIzOoM%3D",  
    "EmbeddedSceneData": null ,  
    "Encryption":  
      {
      "EncryptionOn": true,   
      "SceneEncryptionKeyID": "0000000000001",   
      "PrivacyServerEndPoint":
        {  
        "AppEndPoint": null ,  
        "NetEndPoint": 
          {         
          "APIVersion": "1.0",   
          "EndPointID": "00000000-5cdd-280b-8003-000000000000",   
          "NodeID": null ,  
          "PortID": null ,  
          "Scheme": [  
            {  
            "Protocol": "WebAPI",   
            "Authority": "niceas.scenera.live",   
            "AccessToken": "eyJ0eXAiOiJK....U7qunXZg",
            "Role": "Client",   
            "ValidationKey": null  
            }  
            ]  
          }  
        }  
      }  
    }  
  ],  
  "SceneModeConfig": null  
} 


### 6. GetPrivacyObject ###
  * After getting *SceneData* information, display the SceneData and SceneData Image from the sample response above.
  * To display the *SceneData Video* and *SceneData Image* in the developer UI, first retrieve the &lt;SceneEncryptionKeyID\> from the SceneData Response:
  Example: ```"SceneEncryptionKeyID": "0000000000001"``` 
  * Save the &lt;SceneEncryptionKeyID\> locally inside the app to decrypt and display images and video
  * Use the the &lt;SceneEncryptionKeyID\> to get the encryption key from the service.
  * Call for *GetPrivacyObject* API as follows:
  ```
  mainViewModel.getPrivacyObject(this,"2021-01-19T09:34:50.353Z","0000000000001");
  ```
  * In response, the library will save *iv* and *key* in preference variables which can be used to decrypt video and images using AES CTR algorithm.
  * Sample response of *GetPrivacyObject* API call:
  ```
  {
  "Version": "1.0",   
  "MessageType": "response",   
  "SourceEndPointID": "00000001-5e84-224c-8003-000000000065",   
  "DestinationEndPointID": "00000000-5eab-2e10-8003-000000000000",   
  "DateTimeStamp": "2021-0-19T7:29:15:000000",   
  "ReplyID": 11,   
  "ReplyStatusCode": 200,   
  "ReplyStatusMessage": "OK",   
  "Payload":  
    {  
    "PrivacyObjectID": "00000001-5e84-224c-8003-000000000065_000000000152",  
    "StartDateTime": "2021-0-19T7:29:15:000000",   
    "EndDateTime": "2022-0-19T7:29:15:000000",   
    "Authentication": false,   
    "EndPointID": "00000001-5e84-224c-8003-000000000065",   
    "Version": "1.0",   
    "MaskedItems": 
      [ 
      "Face"  
      ],  
    "SceneEncryptionKey":  
      {
      "alg": "AES-CTR",   
      "k": "UkFORE9NU0VTU0lPTktFWQ==",   
      "iv": "UmFuZG9tSW5pdFZlY3Rvcg==",   
      "kid": "0000000000001"  
      }  
    }  
  }  

  * *pHelper.getSceneEncryptionID()* returns THE stored encrypted key from library
  * *pHelper.getIvBytes()* returns stored iv from library
  * Use library’s key and iv to decrypt videos and images after making the GetPrivacyObject API call.

### 7. GetAppControlObject ###
  * Call *getAppControlObject* anytime to refresh the token.
  * Call the *GetAppControlObject* API as follows:
```
mainViewModel.getAppControlObject(this,Helper.getAppSecurityObject(),"2021-01-19T09:34:50.353Z");
```  
  * In response, the library will update the *appControlObject* in library’s preference
  * To get the updated *appControlObject* from the library, use the following functions:
    * *pHelper.getAppControlObject()* : returns AppControlObject from library  
    * *pHelper.getAppSecurityObject()* : returns AppSecurityObject from Library

### 8. Decrypt Image from URL ###
  * If **"DataType": "RGBStill"**, **"MediaFormat": "JPEG"** and **"EncryptionOn": true** inside *SceneData*, then Images are Encrypted.
  * Use the *DownloadImage* class from the library which will return a decrypted image bitmap that you can use in your UI.
  * This is an example of how to get the decrypted image from library :
```
DownloadImage task = new DownloadImage();   
Bitmap bitmap = null;    
try {
    bitmap = task.execute(strUrl).get();   
} catch (InterruptedException | ExecutionException e) {   
    e.printStackTrace();
}
```
  * In this example, we had to pass the Encrypted Image Url from the *SceneData* Object inside the *task.execute()* function

### 9. Decrypt Video from URL ###
  * If **"DataType": "RGBVideo"**, **"MediaFormat": "H.264"** and **"EncryptionOn": true**inside *SceneData*, then the Video is Encrypted.
  * Use the *DownloadVideo* class from the library to download, save locally, and decrypt video from the uri.
  * The following example shows how to get the decrypted video from the library :
  ```
DownloadVideo downloadVideo = new DownloadVideo();   
try {    
    downloadVideo.playvideo(strUrl);   
} catch (Execution e) {   
    e.printStackTrace();   
}  
  ```
  
  * In the above example, we passed the Encrypted Video Url from the *SceneData* Object inside the *playVideo()* function  
  * We then used the same URL to play the video in the VideoView.

### 10. Encrypt Image or Video: ###
  * The *EncryptData* class from the library will return encrypted data in a byte array. Use the encoded byte array in Base64 String. **Not sure what this means**
  * The following example shows how to get the encrypted data from the library:
  ```
if(fIsImageEncrypted){
    byte[] binImage = androi.util.Base64.decode(base64Image, android.util.Base64.DEFAULT);
    EncryptData encryptData = new EncryptData(context);
    byte[] binEncryptedData = null;
    try {
        binEncryptedData = encryptData.execute(binImage).get();
    } catch (InterruptedException | ExecutionException e) {
        e.printStackTrace();
    }
    base64Image = android.util.Base64.encodeToString(binEncryptedData, android.util.Base64.DEFAULT);
}
  ```
  * In the example, we passed Image/Video data in base64 deoded byte array inside the *execute()* function of the *EncryptData* class. Because it is an *AsyncTask*, we used the *.get()* function to get the encrypted Data in byte Array format in response.
  * You must follow step 6 (*GetPrivacyObject*) before you can get encrypted data.
