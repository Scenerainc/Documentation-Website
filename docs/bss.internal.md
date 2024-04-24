
# INTERNAL USE ONLY
# DRAFT



# LOGIN SYSTEM

  1. Each account is linked to a specific IOC.
  2. For instance, 'lmw_abm@tnmtech.com' can only access the ABM IOC, while a separate account like 'lmw_wachter@tnmtech.com' is required for the WACHTER IOC.
  3. Sharing the same account among multiple users will result in only the last person to log in remaining active, while earlier users will be automatically logged out.
  4. Presently, logging into multiple IOCs with a single account is not supported. Further discussion is needed if this feature is required.
  5. If a 'developer4netflix@scenera.net' account is created, please share its password.

    Uploading 화면 기록 2024-04-04 10.04.10.mov…



# BSS USER ACCOUNTS

  - All existing accounts will be deleted, leaving only two new ones: support4netflix@scenera.net and developer4netflix@scenera.net. Developers will share login credentials, while customer support and others will use the support4netflix@scenera.net account. Confirmation is needed regarding the possibility of multiple logins with a single account, which was previously restricted.
    ![image](https://github.com/Scenerainc/Documentation-Website/assets/160102817/ae1ddc41-e606-4928-a717-6aaea1b9fe16)

# DEVICES

- Camera Management: Hiding AI Nodes
    <img width="855" alt="Screenshot 2024-04-03 at 6 54 50 PM" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/a9fd42de-4604-4e74-9466-2ae48ee8133f">

- Delete Camera
  What happens to related documents when a single camera is registered
    - Added the camera's information to the 'nodeList' in the 'devices' document in the AccountService
    - Added the camera's SceneMode to the 'devicescenemode' document in Controller
    - Added 2 configs for the camera to the 'datapipelineconfig' document in the Controller
    - Added 2 PipelineConfigurations for that camera to the 'ConfigDocuments' document in PipelineConfigFacade 
<img width="599" alt="image" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/a91422fd-1933-4a62-827c-2dbfc0049c4b">


# DASHBOARD

- Users with 'SCENERA Administrator' permissions can play an event, but it is not counted as 'Viewed'.
    <img width="1208" alt="Screenshot 2024-04-03 at 6 55 57 PM" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/bf90156f-7420-4865-8835-08b6af219b98">

- Add units to the Y-axis of the Occupancy vs Energy widget
    <img width="1020" alt="Screenshot 2024-04-03 at 6 57 03 PM" src="https://github.com/Scenerainc/Documentation-Website/assets/160102817/ed5334bd-7825-48e6-9eb1-09f77273cc88">
