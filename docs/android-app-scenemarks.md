---
title: Send Scenemarks Through the App
date: 2022-03-28
slug: android-app-scenemarks
---

## Import Dependencies ##
1. To use JitPack with private repositories, get your personal access token to use the library in your project. 

  * For this example, we will use this as our access token: ``` jp_dbku18oktekp0aj72fgv9h9bm2 ```
2. Use this access token as the &lt;username\> in your project’s *build.gradle* file like:
```
INSERT CODE SNIPPET HERE
```

3. Add the Library dependency in your module’s *build.gradle* file:
  * This is the sample library :```implementation 'com.github.awajs:appsecuritysdk:<Tag>'```
    * Note: &lt;Tag\> will be the latest version name of the library
```
INSERT CODE SNIPPET HERE
```
  * Note: Build artifacts (jar, aar) are also private and can only be downloaded if you have access to the Git repo itself.

### 1. Link BSS Account to App ###
  * The first step is to link your BSS account with the Android Application. Call the library’s *BSSLoginActivity.class* like the following example:
```java
Intent intent = new Intent(MainActivity.this, BSSLoginActivity.class);
startActivityForResult(intent, MY_REQUEST_CODE);
```
  * After successful login, the *AppSecurityObject* and *AppControlObject* will be added to the library’s shared preference variables which you can now use further in the project
  * Once login is successful, redirect from the library’s activity to the developer’s activity to perform next steps. For example:
  ```
  CODE SNIPPET
  ```

  * Here, *HomeActivity.class* is the app developer’s activity to redirect the user after successful login from library’s activity
  * Here's an example of the developer’s *BSSLoginActivity*:
  ``` 
  CODE SNIPPET
  ```

### 2. GetSceneMode ###
  * After successful BSS login, the next step is to get the scene mode.
  * The *MainViewModel.class* ﬁle contains all the API calling functions which developers will need.
  * To call the *sceneMode* API, first create an instance of MainViewModel Class:
  ```java
  MainViewModel mainViewModel;
  // Get the ViewModel.
  mainViewModel = new ViewModelProvider(this).get(MainViewModel.class;
  ```
  * Then, call the scene mode API:
  ```java
  mainViewModel.getSceneMode(this);
  ```
  * Get the response string of the sceneMode by implementing an observer for each API function call.
  * To get the response from the library API call, call the observer:
  ```
  CODE SNIPPET
  ```
  * Here, the library's *getSceneModeLiveData()* function will return scenemode data. Check if Encryption is ON and if the preference has a saved key. 
  * If there is no saved key, then call the *getPrivacyObject()* function and its callback as shown below:
  ```
  CODE SNIPPET
  ```

### 2. Upload SceneMark ###
  * After successfully getting *scenemode*, upload the scenemark using the following steps:
  * Note: the *MainViewModel.class* ﬁle contains all the API calling functions you will use
  * To call API's for uploading *scenemarks*, you first must create ab instance of the *MainViewModel* Class as follows:
  ```java
  MainViewModel mainViewModel;
  // Get the ViewModel.
  mainViewModel = new ViewModelProvider(this).get(MainViewModel.class);
  ```
  * Then, call the API's in the following sequence:
  1. Clear the list of Objects to be used for a SceneMark:
    * Call the *clearDetectedObjects* api as follows:
    ```java
    mainViewModel.clearDetectedObjectList(this)
    ```
  2. Update the detected objects in a scene by calling the following function for every object detected in an image:
    * Call the *updateDetectedObjects* API as follows:
      * In the  &lt;encodedImage\> parameter, you must pass an image in Base64 encoded string format. This thumbnail image will be uploaded in the scenemark.
    ```java
    mainViewModel.updateDetectedObjectList(this,encodedImage,label_text,probability,xmin,xmax,ymin,ymax);
    ```
    * For Example:
    ```java
    mainViewModel.updateDetectedObjectList(this,encodedImage,"Human",1,30,40,50,40, 30,40);
    ```
### 3. Update the SceneDataID ###
  * If a new Video recording is started with this SceneMark, then the SceneDataID for the Video must be updated
  * Call the *createVideoScenedataID* API as follows where &lt;VideoDurationSec\> how long the video will be (in seconds):
  ```java
  mainViewModel.createVideoSceneDataID(this,VideoDurationSec,VideoWidth, VideoHeight);
  ```
  * For Example:
  ```java
  mainViewModel.createVideoSceneDataID(this,60,0,0);
  ```

### 4. Send the SceneMark ###
  * Call the *sendScenemark* API as follows to create a scenemark and upload thumbnail image
in scenemark:
```java
mainViewModel.sendSceneMark(activity);
```

### 5. Send Full-Image SceneData ###
  * Call the *sendFullImageScenedata* API. In the &lt;encodedImage\> parameter, you must pass an image in Base64 encoded string format. This is the full image to be uploaded in scenemark.
  ```java
  mainViewModel.SendFullImageSceneData(activity,encodedImage);
  ```

### 6. Create and Upload Video SceneData ###
  * Call the *sendVideoScenedata* API. In the &lt;encodedVideo\> parameter, you must pass video in Base64 encoded string format
    * If the video is small enough, you can just send the full video using:
    ```java
    iChunkNumber = 1
    iNumberOfChunksToUse = 1
    ```

  ```java
  mainViewModel.SendVideoSection(activity,encodedVideo,iChunkNumber,iNumberOfChunksToUse);
  ```

  * For Example:
  ```java
  mainViewModel.SendVideoSection(activity,encodedVideo,1,1);
  ```


### DONE! Your scenemark with scenedata has been successfully created and sent! ###