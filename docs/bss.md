---
title: BSS User Guide
date: 2018-09-15 07:42:34
slug: bss
---

| Version | Date  | Comments |
| :---: | :---: |  :---:  |
| 0.1  | 2024-03-22     | First Release    |
| 0.2  | 2024-05-01     | New Releases for Dashboard, Widgets and Password updates  |
| 0.3  | 2024-06-18     | Update for Scheduling Feature & Event Capturing with Examples |



# How to Log-In
![Login Page](https://github.com/Scenerainc/Documentation-Website/assets/160102817/c826fd24-f712-49c2-9093-9551040a8170)

1. Visit the Scenera's Business Support System, Maistrous Live website at [https://maistrous.scenera.live/login].
2. Enter your username in the "User ID (Email)l".
3. Enter password in the "Password".
4. After entering, click the "Log-In" (Blue) button to access your account.
5. To see details of Terms & Policy, please refer and links on "Terms of Use " and "Privacy Policy".
6. Upon logging in, you will be directed to the tab that you have set as the default.

***************************************************************************************************

# Main View
Upon logging in, "Main" tab is the very first tab on the left column. The "Main" view allows you to interact with and analyze data related to Events, Event Lists, and Processed Rates of the events. This view cannot be customized.

![Main Tab](https://github.com/Scenerainc/Documentation-Website/assets/160102817/05c8e2cb-9d85-4172-bc02-7f70687cfe27)

### Events View
The "Events" section provides users with high-level data points regarding event status, enabling them to quickly understand the number of events that have been viewed/unviewed and resolved/unresolved.
![Main Events](https://github.com/Scenerainc/Documentation-Website/assets/160102817/d60261b9-db8c-4139-b2d1-6cbbaf55f94b)

- **Total** represents total number of events.
- **Unviewed** represents total number of events that has not been viewed.
- **Viewed** represents total number of events that has been viewed.
- **Resolved** represents total number of events that has been viewed and resolved.

### Events List
The Event List provides users with a simplified, detailed view of all events, offering quick insights into the what, where, when, and how of each occurrence and its triggers.
![Main EventList](https://github.com/Scenerainc/Documentation-Website/assets/160102817/aeb52f77-00a4-415a-a7cd-e5771dbf9b57)

- **Category**: Indicates the severity level of the event, categorized as caution, urgent/emergency, or warning.
- **Status**: Shows the current status of the event, whether it has been viewed, unresolved, or resolved.
- **Center** **Name**: Specifies the name of the warehouse, center, or campus where the event occurred.
- **Building** **Name**: Provides the exact name or description of the building where the event took place.
- **Camera**: Identifies the individual camera location and position within each building that captured the event.
- **Event** **Name**: Describes the type of action or use case associated with the event, as set by the user group.
- **Detected** **Date**: Indicates the date and time when the event was initially detected by the system.
- **Identified** **Date**: Shows the date and time when the event was viewed or identified by the user.
- **Resolved** **Date**: Specifies the date and time when the event was marked as resolved by the user or system.

#### Events List Filter
The Event List Filter enables users to arrange the list of events based on preferred criteria
![Main EventListOrdering](https://github.com/Scenerainc/Documentation-Website/assets/160102817/10c35a54-a8ed-401d-a10d-d9c452e47ed0)


### Processed State
![Main ProcessedStatus](https://github.com/Scenerainc/Documentation-Website/assets/160102817/64a27122-ed5f-4cf9-8098-df5ef9f72bc5)

- **Processed** **Rate**: The processed rate displayed in the widget represents the percentage of events that have been identified and resolved.
This metric indicates the efficiency and effectiveness of your event resolution process.
- **Unprocessed**: Reflects the number of cases/events that have not yet been resolved. Monitoring this metric helps you track the backlog of unresolved events and prioritize accordingly.


#### Home Filter
The filter feature allows users to refine the main dashboard by various criteria including building, detection time, categories, status, and registered date. This functionality enables users to customize their dashboard view, focusing on specific parameters to better analyze and manage the displayed data.
![Main Filter](https://github.com/Scenerainc/Documentation-Website/assets/160102817/46dcbd5f-a9f1-4461-a9b2-850935484d55)

- **Building** **Filter**: Allows users to filter events based on the specific building or location where they occurred. Users can select from a list of available buildings or enter a building name to narrow down the events displayed.
- **Detection** **Time** **Filter**: Enables users to filter events based on the time they were detected or identified. Users can specify a date range or time period to view events detected within that timeframe.
- **Category** **Filter**: Provides users with the ability to filter events based on predefined categories or types. Users can select from a list of categories such as caution, urgent/emergency, or warning to focus on specific types of events.
- **Status** **Filter**: Allows users to filter events based on their current status, such as viewed, unviewed, unresolved, or resolved. Users can choose to view events with a particular status or combination of statuses to track their progress.
- **Register** **Date** **Filter**: Enables users to filter events based on the date they were registered or logged in the system. Users can specify a date range to view events registered within that timeframe.

***************************************************************************************************

# Dashboard View
The "Dashboard" view in MAIstro allows users to efficiently manage and view multiple dashboards related to various operational centers, such as warehouses, service centers, offices, and more.
![Dashboard Tab](https://github.com/Scenerainc/Documentation-Website/assets/160102817/a8c43bee-89f9-4b4f-8fae-b43f724a91d5)

1. Customize the layout and appearance of your dashboard(s).
2. Choose which widgets, charts, or metrics to display for different end-users/groups (e.g., Safety & Security, Maintenance, Janitorial, etc.)
3. Set up requirements, alerts and notifications for specific events or thresholds.
4. Manage data sources and integrations for real-time updates.

### Selecting Operation Centers
Use the "Operation Center" dropdown menu to choose specific regions or operational centers you want to view, such as "West Coast Warehouses" or "Northeast Retail Stores". (Example shows "Wachter_OP_PoC").
![Dashboard OpsCenter](https://github.com/Scenerainc/Documentation-Website/assets/160102817/379d31f7-0fb1-4f2e-8c51-bcd733704b4c)

### Set to Default & Details Arrow Key
![Dashboard SetToDefault](https://github.com/Scenerainc/Documentation-Website/assets/160102817/3ee06ea9-2c11-42a1-8233-6a821224a2e4)

1. Set a customized dashboard as your default by clicking "Set as Default".
2. Use the ">" button to explore further details of the selected dashboard.

## Detailed Dashboard View
The detailed view allows users to see the personalized dashboard for each warehouse, data center, or retail store.

1. Use "Go to Dashboard List" to return to the main dashboard list.
2. Select different dashboards from the "Dashboard" pulldown for easy navigation.
3. Choose specific buildings from the "Building" pulldown, useful for managing multiple buildings.
4. Select individual floors using the "Floor" pulldown if the building has multiple levels.

![Dashboard DetailsTab1](https://github.com/Scenerainc/Documentation-Website/assets/160102817/2d2de26a-799d-423b-b408-bd3f49a8b59b)

![Dashboard DetailsTab2](https://github.com/Scenerainc/Documentation-Website/assets/160102817/5e6380e0-fafb-448f-9c36-f826b2cfda63)

#### Customize the dashboard to your operational needs with various widgets.
#### Widgets can include:
   - "Floor Maps" showing device locations and important areas.
   - "Plant Status" to monitor plant conditions.
   - "IP Cameras" displaying event detection locations.
   - "Event List" showing detected events.
   - "Weather" providing general weather forecast.
   - "Weather Rooftop" for current outdoor weather.
   - "Energy Trend" tracking energy usage.
   - "Occupancy Trend" monitoring foot traffic.

### Adding / Editing Image Widget
   - Go to "Settings" -> Click on "Dashboard Settings" (top left) -> Select which dashboard you want to modify, then select "Modify Dashboard"
   - **Adjusting Images:**
      - When you add an image, it automatically fits the width of the widget. If the image is too long, it'll trim the extra parts to keep it neat.
   - **Setting Up the Widget:**
      - Once you've added your image and given it a title, remember to save it by clicking the "Save" button inside the widget.
      - After setting up the image widget, save the whole dashboard by clicking the "Save" button at the top-right corner.
      - You can only have one image widget at a time. If you add more than one, they'll all have the same settings.
   - **Making Changes:**
      - If you want to change the image or anything else about the widget, make your changes and then save them using the "Save" button inside the widget.
   <img width="1505" alt="Modify Dashboard_Image_Widget" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/8105886f-7cab-4bed-8a96-888c5c92ede4">
   <img width="1511" alt="Image_Widget_Selection" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/b85a5528-6ea3-4ec7-9f18-1cb6f920dba7">
   <img width="1510" alt="Drag_drop_save" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/72101991-b914-4040-9c2c-b82850907d3b">

### Rotational Dashboard Activation Guide

   - **Enable/Disable Rotation:** You have the option to turn the dashboard rotation feature on or off, and choose how frequently you want the dashboards to rotate (e.g., every 10 seconds or 30 seconds).
   - **Accessing Settings:** Navigate to Settings and locate the "IOC Settings" option at the top-left corner of the screen.
   - **Toggle Rotation:** Within the "IOC Settings" menu, find the "Dashboard Rotation Setting" section. Here, you'll see a toggle labeled "Rotation Use or Not." Switch the toggle to the desired position to activate (green) or deactivate (gray) the rotational feature.
   - **Adjust Rotation Interval:** If you've enabled rotation, specify the rotation interval by entering a numerical value indicating how quickly you want the dashboard to switch between screens, measured in seconds.
   - **Save Changes:** After configuring the rotation settings, remember to click the "Save" button to apply the changes and initiate the rotational behavior of your dashboard.

<img width="1498" alt="Rotational_Dashboard_On" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/a94a433b-13fd-473a-9371-e7a13c48bbc6">

***************************************************************************************************

# Devices View
- Organize Pulldown: Allows users to organize and order the list by specific headers such as camera, device, operation center, building, etc.
- Filter: Functionality to refine or narrow down the displayed devices based on specific criteria.
- New Device: Option to add a new camera, device or equipment to the list.

## Device Management View
<img width="1393" alt="Devices DeviceMgt" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/f3117e56-dbc6-4c9a-9afb-2eb2ca84f322">

1. Status: Current operational status of the device (e.g., “Active”, “Inactive”).
2. Device: Type or model of the device.
3. Building: Location or building where the device is installed.
4. Operation Team: Team or department responsible for managing the device.
5. Operation Center: Centralized operational management center associated with the device.
6. Customer: Name or identifier of the customer associated with the device.
7. Camera: Identifier or name of the camera (if applicable).
8. Register Date: Date when the device was registered or installed.

## Camera Management View
<img width="1393" alt="Devices CameraMgt" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/7abf3e8b-1fd3-4231-a9cd-d3db77eb2530">

1. Status: Current operational status of the camera (e.g., “Active”, “Inactive”).
2. Camera: Identifier or name of the camera with unique locations (e.g., company_camera.location_unique.identifier)
3. Device: Name of the device, typically type or model of the device.
4. Building: Unique location or building identifier where the camera is installed.
5. Operation Center: Centralized operational management center associated with the camera.
6. Operation Team: Team or department responsible for managing the camera.
7. Register Date: Date when the camera was registered or installed.
8. Config: Status indicating whether the camera configuration is complete (Complete, Incomplete). The 'Complete' state is reached when the parameters and ROI settings for all nodes that will be applied to the camera are complete.

### How To Add/Delete Camera
<img width="1490" alt="Devices EditCamera" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/a6874de2-45b8-4b33-9cd5-2c2e7ef9e099">
   
   #### To Delete A Camera
   - To Delete a Camera, click on 'Trash Can' Icon
   - Press 'Confirm'
  
   #### To Add A Camera
   - Click on the 'New Camera' Button
   - Fill out the Required Fields such as:
      - Assign the Camera to the Operations Center and Team
      - Select the building and floor for installation of registering camera
      - Use a unique camera name (e.g., *CenterName_Location_Area*)
      - Note: Please request assistance if a new time zone is needed. 
   <img width="1490" alt="Devices NewCameraRegistration" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/f9caaa2c-e75d-462f-8097-db8dfaaa8e8a">

### How To Modify a New/Existing Camera

   - Go to the Camera Management section.
   - Click on the "Modify" tab to update and modify camera details.
   - Change camera names, resolutions, RTSP addresses, FPS settings, and more.
   - For additional assistance, contact SCENERA's support team.
     
<img width="1511" alt="HowToCamera Modify" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/a6501fe7-62fe-4735-ac9d-d30050fce552">


### How To Configure a New/Existing Camera

   - Go to the Camera Management section.
   - Click on the "Config" tab to configure and update AI nodes for each camera.
   - Choose specific AI nodes, select an inference engine, customize detection areas, and add an ROI as needed. Follow the steps below.
   - For additional assistance, contact SCENERA's support team.

<img width="1511" alt="HowToCamera Config General" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/d9fe1b28-a45a-400c-aba8-56919d3c853a">

   1. Choose an "AI Node" from the dropdown menu. These nodes are customizable to suit your organization's requirements and may include options like Fall Detection, Zone Entry, Intrusion, or Line Crossing. Refer to the example screenshot below for clarification.

         <img width="1389" alt="HowToCamera Config AInodes" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/7dd2ff4b-a9b5-47ac-a1d6-cccd7aa3ae79">

   2. Select an inference engine, such as "TNM YoloV8 M416". Refer to the example below.

         <img width="1388" alt="HowToCamera Config Inference" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/83f1c9c7-0609-4d15-b022-08a69f9c8507">


   3. Customize the detection area for each AI node. To specify the exact area, use the "Get CCTV thumbnail" feature to generate a visual representation of the detection area.

   5. After generating the visual, add Regions of Interest (ROI) by clicking on "Add ROI". Use the yellow lines to mark the specific event area within the visual.

     
### Camera Configuration Parameters Definitions
   ![Screenshot 2024-04-04 at 4 03 52 PM](https://github.com/Scenerainc/Documentation-Website/assets/160102817/520fa374-6905-4624-9a8f-c096f3b7ec3a)

   - **Recognition Rate (%)**: This parameter is no longer in use and has been replaced by the Analysis Threshold.
   - **Event Start Time (Seconds Elapsed)**: This setting applies specifically to Loitering and Falldown events. It represents the duration before an event is recognized as valid.
     Example:
        - For Loitering events, if set to 10 seconds, a person must linger in the designated area for 10 seconds before the event is triggered.
        - For Falldown events, if set to 10 seconds, the system waits for 10 seconds after a person falls in the designated area before registering the event.
   - **Alarm Delay (Seconds)**: This setting determines the delay before sending a SceneMark when multiple events occur consecutively on the same camera.
     Example:
        - If set to 10 seconds for a specific camera, any repeated events within a 10-second window following a ZoneEntry event will be ignored, and no SceneMark will be generated.

#### How to Update & Edit the Scheduling Feature for Event Capturing
Our system allows you to set specific schedules for capturing events, which can vary between weekdays and weekends. This guide explains how this scheduling feature works, especially as it relates to transitions from weekdays to weekends and vice versa.
![BSS Configure Event Detection Time Wknd Wkdy](https://github.com/Scenerainc/Documentation-Website/assets/160102817/ac895e01-62cb-420d-afee-96662694ca0e)

   - **How the System Works**: Time Adjustment for Midnight: If the scheduled end time is earlier than the start time (e.g., from 7 PM to 6 AM), it means the event capturing period goes past midnight.
   - **Adjusting 'detectedtime'**: If the current time (detectedtime) is between midnight and the scheduled end time,    the system adds 2400 to detectedtime. This adjustment helps compare times across days. The end time (EndTime) is also increased by 2400 to align with the adjusted detectedtime.
   - **Event Capturing Decision**: The system checks if detectedtime falls within the adjusted time range (from the start time to the adjusted end time). If it does, events are captured during this time.

   - **Example Use Case Below**:
      - Suppose you set the following schedule for capturing events:
         - Weekdays: Capture events 7pm-6am  (1900-0600)
         - Weekends: Capture events: 2pm-11am (1400-1100)
      - Then, we can ask:
         - Could the events be captured Friday at 5am?  Yes. (Weekday schedule is in effect)
         - Could the events be captured Saturday at 5am?  Yes.  (Weekend schedule has taken effect.)
         - Could the events be captured Sunday at 7am?  Yes.  (Weekend schedule has taken effect.)
         - Could the events be captured Monday at 7am?  No.  (Weekday schedule has taken effect.)
           

## Device Status View
<img width="1159" alt="Devices DeviceStatus" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/b4147b18-9acf-42ba-9495-5a36007f899c">

1. No : Simple number
2. Device: Bridge device name
3. Report Time: The last time the bridge device reported status information
4. Firmware Version: Firmware version of the bridge device
5. Uptime: The amount of time the bridge device has been up since the last boot (in seconds)
6. CPU Usage/Temp: CPU usage/temperature of the bridge device (unit: % / °C)
7. GPU Usage/Temp: GPU usage / temperature of the bridge device (Unit: % / °C)
8. Memory Usage : Memory usage of the bridge device (Unit : %)
9. SWAP Memory Usage : SWAP memory usage of the bridge device (Unit : %)
10. Application Status: Status of the application on the bridge device - Normal: Normal, Error: Error, -: No report
11. Camera RTSP Status : Status of RTSPs connected to the bridge device - Normal : Normal, Error : If any of the RTSPs is abnormal, - : No report
   - If the RTSP status is Error, it is likely that there is a problem with the RTSP connection and it is disconnected
12. Camera FPS Status : Status indicating whether the FPS processing set for each camera is being processed normally - Normal : Normal, Error : FPS processing problem, - : Nothing to report
   - FPS settings are 'Camera FPS' and 'FPS Drop' items in the camera configuration screen. Camera FPS: Number of frames provided by RTSP, FPS Drop: Number of frames to drop when inferencing
   - Example: If Camera FPS is 30 and FPS Drop is 5, the bridge device will inferencing for that RTSP at 6 frames per second
   - The FPS status is reported as an error when the number of frames provided by the RTSP drops or the resource usage of the bridge device increases and FPS processing is not normal

### Self-Check Result View
<img width="1218" alt="Devices SelfCheckResult" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/1d7b60c9-033a-41ae-9da2-dc2928c64fac">

   Note:
      - Self-Check is an additional function to identify problematic components (bridge devices, data pipelines, etc.) in the entire system, discover the cause, and take action efficiently by preparing a video with 100% guaranteed event detection in advance and sending the video to the bridge device -> Algorithm Server -> Data Pipeline -> BSS to check whether an alarm occurs at the end.
      - Depending on the event (Intrusion, Loitering ..), it may not go through both AI Server (BD) and AI Server (Pipeline) steps, only one step, or both steps. An event with a Diagnosis Result of '-' means that it does not go through that step.
      - Diagnosis Result : Success - Diagnosis success, Fail - Diagnosis failure

1. No: Simple number
2. Device: Bridge device name
3. Camera: Camera name
4. Event Name: The name of the event that performed the self-check
5. Report Time: Self-Check started time
6. Inference Engine Diagnosis Result/Time: Inferencing result and time performed on the bridge device
7. AI Server(BD) Diagnosis Result/Time: Processing result and time for events sent from the bridge device to the algorithm server.
8. Pipeline Diagnosis Result/Time: Processing result and time for events sent from the bridge device to the data pipeline.
9. AI Server(Pipeline) Diagnosis Result/Time: Processing result and time for events sent from the data pipeline to the algorithm server
10. Alarm Diagnosis Result/Time: Alarm sending result and time for events sent from the data pipeline to the BSS

***************************************************************************************************

# Users View
In the 'Users' tab of the BSS, administrators and BSS users can manage user profiles, security clearances, and alarm configurations.

![Users Tab](https://github.com/Scenerainc/Documentation-Website/assets/160102817/804bb881-3b5c-44ee-a05d-288bfe5f71f8)

### How to Add/Delete New Users
<img width="1601" alt="Users UserMgt Add Delete" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/e0c65646-c76e-454d-a0d6-2622b270fe34">

   ### To Delete Users
   1. Click on the Trash Can Icon
   2. Press 'Confirm

   ### To Add Users

   1. Click on "New User" Button
   2. Fill Out Required Fields from the 'Register New User' Window
   <img width="1556" alt="Register NewUser" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/333de0fc-3019-4d21-a499-112ae65d7c45">
   
   <img width="396" alt="Authority Of Users" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/aa348c4a-0ea0-4192-8188-88dba442d565">
   
   *User Authority Categories:*
   - IOC Administrator: Manages system settings and user permissions at the highest level.
   - Operations Team Administrator: Oversees user access and tasks for the operations team.
   - Operations Center Administrator: Controls access and functions specific to the operations center.
   - Facility Staff: Handles facility-related tasks like maintenance and cleaning.
   - Security Manager: Manages security measures and user access.
   - Security Guard: Monitors and enforces security procedures.
   - Building Owner: Manages property ownership and finances.

### How To Reset Password

   - **Initiating Password Reset:** If you've forgotten your password and need to reset it, start by clicking on the "reset password" option.
   - **Enter Registered Email:** Next, type in the email address associated with your account, the one you used during registration.
   - **Check Your Email:** After submitting your email, check your inbox. You should receive an email with instructions on how to reset your password.
   - **Check Spam Folder:** If you haven't received the email after a few minutes, please also check your spam or junk folder in case the email was misclassified.
   - **Follow Instructions in Email:** Open the email and follow the directions provided to reset your password securely.
<img width="226" alt="Reset Password_Main" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/3fd046a9-b131-4b3a-8694-380485ace32d"><img width="224" alt="Reset Password_E-mail" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/f24fed21-8d9f-48fc-81ca-907e83951cc0">


