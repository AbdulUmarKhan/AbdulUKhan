# CHANGELOG

## Note

Kindly advise that **please do not re-sign / assign new digital signature to** the following files as assigning new digital signature on these files could lead to fatal errors:
   * **CptControl.exe**
   * **CptHost.exe**
   * **CptInstall.exe**
   * **CptService.exe**
   * **CptShare.dll**
   * **zzhost.dll**
   * **zzplugin.dll**
   * **aomhost64.exe**

## 2019-09-04 @ [v4.4.55968.0904](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.4.55968.0904)

## Note

### :red_circle: SDK file structure has changed

**In order to further optimize the size of our SDK package, starting from this version, Zoom Windows SDK removes the installation package of `Microsoft VC90 runtime`. Please visit Microsoft's website to download and install the `Microsoft VC90 runtime` on your machine. Please also kindly consider adding the `Microsoft VC90 runtime` installation packages in your installation package when you publish your applications developed using Zoom Windows SDK.**

## Added
*  Add a new interface to hide switch-camera-button on `ShareCameraWindow`
* `IMeetingConfiguration.HideSwitchCameraButton(bool bHide)`
*  Add a new interface to switch share to next camera when sharing the camera
* `IMeetingShareController.SwitchToShareNextCamera();`
*  Add a new interface to determine whether the user can switch to next camera when sharing the camera
* `IMeetingShareController.CanSwitchToShareNextCamera(bool& bCan);`
*  Add new interfaces in `IMeetingUIController` to allow swapping the position of the video view and the sharing view:
* `virtual SDKError SwapToShowShareViewOrVideo(bool bToDisplayShare) = 0;`
* `virtual SDKError IsDisplayingShareViewOrVideo(bool& bIsShare) = 0;`
* `virtual SDKError CanSwapToShowShareViewOrVideo(bool& bCan) = 0;`
*  Add a new interface to redirect the warning messages (e.g:"Resource Insufficient") and to trigger the callback `IMeetingServiceEvent.onMeetingStatisticsWarningNotification()`
* `IMeetingUIElemConfiguration.RedirectMeetingWarningMsg(RedirectWarningMsgOption redirectOption)`
*  Add a new interface `IMeetingAudioCtrlEvent.onHostRequestStartAudio()` and a new class `IRequestStartAudioHandler` to notify attendee when the host is requesting to enable microphone.
*  Add new callbacks for default devices(mic/speaker/camera) when they are selected or have changes:
* `IVideoSettingContextEvent.onDefaultCamDeviceChanged(const wchar_t* deviceId, const wchar_t* deviceName)`
* `IAudioSettingContextEvent.onDefaultMicDeviceChanged(const wchar_t* deviceId, const wchar_t* deviceName)`
* `IAudioSettingContextEvent.onDefaultSpeakerDeviceChanged(const wchar_t* deviceId, const wchar_t* deviceName)`
*  Add a parameter to the interface `IsAnnoataionDisable()` with a default value.
* `IAnnotationController.IsAnnoataionDisable(SDKViewType viewtype = SDK_FIRST_VIEW)`

## Changed & Fixed
*  Fixed an issue that the schedule meeting dialog is not shown
*  Fixed an issue that the video is turned off by default when starting a meeting with ZAK
*  Fixed an issue that replacing the Zoom icon in the main meeting window is not success
*  Fixed an issue that sharing with pairing code does not show the UI controls
*  Fixed an issue that the meeting ends right after starting a meeting
*  Optimized the `IMeetingAudioCtrlEvent.onUserActiveAudioChange()` callback so it will be triggered less frequent
*  Optimized the SDK initialization process by reducing the call to `newfitpanel:initallcontrol()`
*  Optimized the performance of `MuteAudio()` interface
*  Changed to hide the "Pause/Stop" buttons when the auto-recording feature is turned on


## 2019-07-15 @ [v4.4.55130.0712](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.4.55130.0712)

**Note**

Some default behavior in Zoom meeting has changed:
1. The sharing toolbar will be shown by default. If you want to hide the sharing toolbar, please call `IMeetingUIElemConfiguration.SetSharingToolbarVisibility(false)` explicitly in your app.
2. Once the local recording content is converting, the converting progress dialog will be shown by default. If you don't want to show this progress dialog, please call `IMeetingUIElemConfiguration.EnableLocalRecordingConvertProgressBarDialog(false)` explicitly in your app.

**Added**

* Introduced new Zoom meeting UI
* Added new interfaces for setting items
  * `IGeneralSettingContext.EnableDisplayReminderWindowWhenExit(bool bEnable)`
  * `IGeneralSettingContext.IsDisplayReminderWindowWhenExitEnabled()`
  * `IGeneralSettingContext.EnableShowMyMeetingElapseTime(bool bEnable)`
  * `IGeneralSettingContext.IsShowMyMeetingElapseTimeEnabled()`
  * `IGeneralSettingContext.IsCurrentOSSupportAccelerateGPUWhenShare()`
  * `IGeneralSettingContext.EnableAccelerateGPUWhenShare(bool& bEnable)`
  * `IGeneralSettingContext.IsAccelerateGPUWhenShareEnabled()`
  * `IGeneralSettingContext.EnableRemoteControlAllApplications(bool bEnable)`
  * `IGeneralSettingContext.IsRemoteControlAllApplicationsEnabled()`
  * `IAudioSettingContext.EnableEchoCancellation(bool bEnable)`
  * `IAudioSettingContext.IsEchoCancellationEnabled()`
  * `IRecordingSettingContextEvent.onCloudRecordingStorageInfo(INT64 storage_total_size, INT64 storage_used_size, bool allow_exceed_storage)`
  * `IRecordingSettingContext.SetRecordingSettingEvent(IRecordingSettingContextEvent* pEvent)`
  * `IRecordingSettingContext.CanGetCloudRecordingStorageInfo()`
  * `IRecordingSettingContext.GetCloudRecordingStorageInfo()`
  * `IRecordingSettingContext.GetRecordingManagementURL()`
  * `IRecordingSettingContext.CanGetRecordingManagementURL(bool& bEnable)`
  * `IRecordingSettingContext.EnableSelectRecordFileLocationAfterMeeting(bool bEnable)`
  * `IRecordingSettingContext.IsSelectRecordFileLocationAfterMeetingEnabled()`
  * `IRecordingSettingContext.EnableMultiAudioStreamRecord(bool bEnable)`
  * `IRecordingSettingContext.IsMultiAudioStreamRecordEnabled()`
  * `IRecordingSettingContext.EnableAddTimestampWatermark(bool bEnable)`
  * `IRecordingSettingContext.IsAddTimestampWatermarkEnabled()`
  * `IRecordingSettingContext.EnableOptimizeFor3rdPartyVideoEditor(bool bEnable)`
  * `IRecordingSettingContext.IsOptimizeFor3rdPartyVideoEditorEnabled()`
  * `IRecordingSettingContext.EnableShowVideoThumbnailWhenShare(bool bEnable)`
  * `IRecordingSettingContext.IsShowVideoThumbnailWhenShareEnabled()`
  * `IRecordingSettingContext.EnablePlaceVideoNextToShareInRecord(bool bEnable)`
  * `IRecordingSettingContext.IsPlaceVideoNextToShareInRecordEnabled()`
  * `IAccessibilitySettingContext.EnableAlwaysShowMeetingControls(bool bEnable)`
  * `IAccessibilitySettingContext.IsAlwaysShowMeetingControlsEnable(bool& bEnable)`
  * `ISettingService.GetAccessibilitySettings()`
* Added a new interface to hide the “Upgrade to Pro” text from the free meeting reminder message
  * `IMeetingUIElemConfiguration.HideUpgradeFreeMeetingButton(bool bHide)`
* Add a new parameter to the SDK initialization method to customize the log size, the range is from 1MB to 50MB per log file, and by default is 5MB. The maximum number of the log file is 5.
  * `tagInitParam.uiLogFileSize`
* Added a new interface to redirect bad network warning message
  * `IMeetingUIElemConfiguration.RedirectMeetingWarningMsg(RedirectWarningMsgOption redirectOption)`
* Added a new interface to show/hide the tabs in the setting dialog
  * `ISettingUIStrategy.ConfSettingDialogShownTabPage(SettingDlgShowTabPageOption showOption)`
* Added a new interface to show/hide video button
  * `IMeetingUIElemConfiguration.EnableVideoButtonOnMeetingUI(bool bEnable)`
* Redefined the return values of ZOOM_SDK_NAMESPACE::AuthResult. Added 2 new values:
  * `AUTHRET_OVERTIME`
  * `AUTHRET_NETWORKISSUE`
* Added a new interface to switch between the active video view and the sharing content view
  * `IMeetingUIController.SwitchVideoASView()`
* Added new examples in sdk_demo_v2

**Changed & Fixed**

* Modified to allow editing or deleting recurring meetings via SDK
* Hide the “End Other Meeting” dialog when the `redirectEndOtherMeeting(true)` is called
* Fixed an issue that when sharing specific window the desktop is shared
* Fixed an issue that when disabling the chat feature the message alert still pops up
* Fixed an issue that sometimes the Windows Electron SDK failed to load zzhost.dll
* Fixed an issue that the user’s info showed up as a string of random characters
* Fixed an issue that the meeting is ended at an unexpected time while only 1 user is in the meeting
* Fixed an issue that 3 black borders appear after calling `SetBottomFloatToolbarWndVisibility`

**Deprecated**

* IMeetingShareController.LockShare()
* IMeetingShareController.UnLockShare()
* IScheduleForUser.GetEmail()




## 2019-03-25 @ [v4.3.1.47204.0325](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.3.1.47204.0325)

**Added**

* A new refactorized demo project that provides clear instructions on how to implement major features
* Introduce new Zoom meeting UI
* Add new interfaces to control share viewer’s annotate privilege
* Add 1080p video support
* Add new interfaces to customize the sub-tab pages in H323 invite page and customize all tab pages in the invite dialog
* Add new interfaces to show/hide ‘chat’,’record’ buttons
* Add new EndMeeting reasons for IMeetingServiceEvent.onMeetingStatusChanged
* Add support audio/video option on start meeting with API User
* Add customize labels/logos/texts in the in-meeting UI

**Changed & Fixed**

* Fix an issue that the user is unable to show chat window when assigning the window to its parent window
* Fix an issue that the user is unable to get window handle when calling showParticipantListWnd
* FIx an issue that the Windows SDK crashes with "Out of Memory" error
* Remove remaining 10 minutes tooltips and support callback
* Fix an issue that the participant’s video is blur and shaken

**Deprecated**

* IFreeMeetingEndingReminderHandler
* IMeetingConfigurationFreeMeetingEvent.onFreeMeetingEndingReminderNotification
* SetUICustomizedString

## 2019-01-23 @ [v4.3.0.30730.0118](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.3.0.30730.0118)

**Added**
*	Support for closed caption
*	Support for multi-share setting
*	Support for controlling the device camera
*	New feature to customize the title of meeting UI
*	New feature to handle meeting reminder. The user can hide the reminder tooltip button and customize the reminder message
*	New logging feature that stores logs with the maximum size of 5MB.
*	New options to turn on/off the video and audio for API user.
*	A new method to join/start meeting directly via url, such as zoommtg://zoom.us/join?action=....

**Changed & Fixed**
*	An issue that the screen sharing set to 1 FPS when another API is called
*	An issue that cannot move floating video window to screen edge
*	An issue that cannot use chat under donet framework
*	An issue that IMeetingConfiguration::EnableAutoEndOtherMeetingWhenStartMeeting doesn’t work

**Coming in the future releases**
*	A new refactorized demo project that provides clear instructions on how to implement major features will come in the next release

## 2018-10-29 @ [v4.1.30384.1029](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.30384.1029)

* Support advanced share at API level
1. Share a selected area of desktop
2. Share only the computer audio
3. Share the camera

* Add more meeting configurations

* Bug fixes


## 2018-09-11 @ [v4.1.31872.0905](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.31872.0905)

* Support to direct share with ultrasonic

* Support to integrate with Outlook plugin

* Support Zoom meeting invite dialog by default

* Bug fixes

## 2018-08-20 @ [v4.1.30420.0817](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.30420.0817)

* Custom Meeting UI (support basic meeting function, except for Webinar and Breakout Session)

Meeting Service

meeting_webinar_interface.h
```
support common feature of webinar meeting in sdk layer
```

meeting_annotation_interface.h
```
add new interface to get customized annotation controller
```

meeting_chat_interface.h
```
1.add new callback  event for chat status changed.
onChatStautsChangedNotification
2.add new interface to send chat for webinar meeting.
SendChat4WebinarMeeting
3.add new interface to get current privilege status of chat session.
 GetChatStatus
```

meeting_configuration_interface.h
```
support redirect click evnet of custom live stream menu.
ClickCustomLiveStreamMenuEvent
```

meeting_recording_interface.h
```
1.add callback event for customized ui local recroding source changed
onCustomizedLocalRecordingSourceNotification
2.add new interface to request customized local recording source notification.
RequestCustomizedLocalRecordingSource
```

Setting Service
```
1.add more audio settings interface
IAudioSettingContext
2.add more video settings interface
IVideoSettingContext
3.support test audio mic and speaker
4.support video device preview
```

Customized UI support
```
./h/customized_ui
1.support customized video ui
2.support customized share ui
3.support local recording for customized ui
4.support customized annotation ui
5.support customized remote control
6.now don't support Q&A
7.now don't support Polling
```

## 2018-07-26 @ [v4.1.28966.0727](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.28966.0727)

The start meeting logic for API users has changed. Please read below before upgrading to this version.

### Added
Auth Service
```
add new callback event for zoom access token expired
ZOOM_SDK_NAMESPACE.IAuthServiceEvent.onZoomIdentityExpired
once received this event, you need to re-login again
```

Meeting Service

meeting_service_interface.h
```
1.support start or join meeting with meeting's vanity ID
2.add new start meeting method for without login user to replace old api user start meeting method
StartParam.StartParam4WithoutLogin
3.add new interface to get meeting password
ZOOM_SDK_NAMESPACE.IMeetingInfo.GetMeetingPassword
4.add new callback event for meeting parameter notification
ZOOM_SDK_NAMESPACE.IMeetingServiceEvent.onMeetingParameterNotification
```

meeting_configuration_interface.h
```
1. add callback event for webinar register notification
ZOOM_SDK_NAMESPACE.IMeetingConfigurationEvent.onWebinarNeedRegisterNotification
2.add callback event for end other meeting notification
ZOOM_SDK_NAMESPACE.IMeetingConfigurationEvent.onEndOtherMeetingToJoinMeetingNotification
3.add callback event for end other meeting notification
ZOOM_SDK_NAMESPACE.IMeetingConfigurationEvent.onFreeMeetingEndingReminderNotification
4. add new interfaces of meeting configuration
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.EnableInputMeetingScreenNameDlg
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.RedirectWebinarNeedRegister
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.RedirectEndOtherMeeting
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.EnableShareIOSDevice
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.EnableShareWhiteBoard
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.AlwaysShowIconOnTaskBar
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.RedirectFreeMeetingEndingReminderDlg
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.SetShowAudioUseComputerSoundChkbox
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.SetShowVideoOptimizeChkbox
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.SetShowCallInTab
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.SetShowCallMeTab
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.ForceDisableMultiShare
ZOOM_SDK_NAMESPACE.IMeetingConfiguration.SetAlwaysShowMeetingIDOnTitle
```

meeting_live_stream_interface.h
```
support live stream in sdk layer
```

meeting_participants_ctrl_interface.h
```
1. add new interfaces of meeting participants control
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.LowerHand
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.RaiseHand
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.MakeHost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.CanbeCohost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.AssignCoHost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.RevokeCoHost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.ExpelUser
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.CanReclaimHost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.ReclaimHost
ZOOM_SDK_NAMESPACE.IMeetingParticipantsController.ReclaimHostByHostKey
2.add callback event for cohost change notification
ZOOM_SDK_NAMESPACE.IMeetingParticipantsCtrlEvent.onCoHostChangeNotification
```

meeting_recording_interface.h
```
1. add new interfaces of meeting recording control
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.CanStartRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.CanAllowDisAllowLocalRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.StartCloudRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.StopCloudRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.IsSupportLocalRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.AllowLocalRecording
ZOOM_SDK_NAMESPACE.IMeetingRecordingController.DisAllowLocalRecording
2.add callback event for cloud recording status notification
ZOOM_SDK_NAMESPACE.IMeetingRecordingCtrlEvent.onCloudRecordingStatus
```

meeting_remote_ctrl_interface.h
```
add new interfaces of meeting recording control
ZOOM_SDK_NAMESPACE.IMeetingRemoteController.CanRequestControl
ZOOM_SDK_NAMESPACE.IMeetingRemoteController.IsHaveRemoteControlRight
ZOOM_SDK_NAMESPACE.IMeetingRemoteController.IsInRemoteControllingStatus
ZOOM_SDK_NAMESPACE.IMeetingRemoteController.EnterRemoteControllingStatus
ZOOM_SDK_NAMESPACE.IMeetingRemoteController.LeaveRemoteControllingStatus
```

meeting_sharing_interface.h
```
add new interfaces of meeting share control
ZOOM_SDK_NAMESPACE.IMeetingShareController.StartWhiteBoardShare
```

meeting_video_interface.h
```
1.add new interfaces of meeting video control
ZOOM_SDK_NAMESPACE.IMeetingVideoController.CanAskAttendeeToStartVideo
ZOOM_SDK_NAMESPACE.IMeetingVideoController.AskAttendeeToStartVideo
ZOOM_SDK_NAMESPACE.IMeetingVideoController.CanStopAttendeeVideo
ZOOM_SDK_NAMESPACE.IMeetingVideoController.StopAttendeeVideo
2.add callback event for host request to start video notification
ZOOM_SDK_NAMESPACE.IMeetingVideoCtrlEvent.onHostRequestStartVideo
```


## 2018-05-22 @ [v4.1.25013.0522](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.25013.0522)
### Added
1.c++ sdk
a> Configuration of Meeting Service Interface

support to config DSCP for audio video session

support to redirect click event of participant list button

support to disable copy and paste feature when remote control

support to disable UI elements of split screen mode

support to auto hide join audio dialog when it shown

support to enable hide the full phone number for pure call in user
b> H323 helper interface

support to get h323 device for current meeting

change the CallOutH323 interface

c> Sharing of Meeting Service Interface

support to block window form screen share without change windows's style

d>Meeting Service Interface

support to get meeting connect type

e> Setting Service Interface

support to enable or disable auto enter full screen video mode when view share

support to enable or disable always show name on video

support to enable or disable turn off video when join meeting

support to enable or disable original input of mic

support to enable or disable stereo audio

add new interface for statistic setting

f>L10n

add new language support(Italian Portuguese Russian)

2.c# sdk

add new c++ interface wrap

## 2017-12-25 @ [v4.1.18127.1225](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.18127.1225)
### Added

1.c++ sdk
    a> setting service

add SettingTabPage option in ShowSettingDlgParam

add EnableHDVideo and IsHDVideoEnabled interface in IVideoSettingContext

b> meeting service

add IsMeetingLocked interface in IMeetingService

rename GetMeetingConnQuality to GetSharingConnQuality in IMeetingService

support to get sending and receiving connection quality of audio/video/share session

b> meeting audio controller

fix onUserActiveAudioChange does not worked bugs in IMeetingAudioCtrlEvent

c>meeting configuration

add RedirectClickEndMeetingBTNEvent interface in IMeetingConfiguration

add EnableClaimHostFeature interface in IMeetingConfiguration

d> meeting share controller

add ShowSharingAppSelectWnd interface in IMeetingShareController

add share computer sound interface

IsSupportEnableShareComputerSound

EnableShareComputerSound

add optimize for full screen video clip interface:

IsSupportEnableOptimizeForFullScreenVideoClip

EnableOptimizeForFullScreenVideoClip

e>meeting ui controller

add onEndMeetingBtnClicked callback event in IMeetingUIControllerEvent

2.c# sdk

a>wrap new c++ interface and callback event

b>fix callback event does not worked issue


## 2017-11-01 @ [v4.1.12147.1101](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.1.12147.1101)

### Added

1.add two new callback events in IMeetingServiceEvent

a>onMeetingStatisticsWarningNotification :  Meeting statistics warning notification callback

b>onMeetingSecureKeyNotification : Meeting secure key notification, need to web backend and special account type support.

2.fix crash bug of sdk cleanup

3.minor bug fix

## 2017-10-10 @ [v4.1.9658.1010](https://github.com/zoom/zoom-sdk-windows/releases/tag/v.4.1.9658.1010)

### Added

01.Interface refactoring

for details, please visit: https://developer.zoom.us/docs/windows/windows-sdk-refactor-details/

02.New interface of change inmeeting display user name and notification of inmeeting display user name changed

03.New interface of hide/show sharing frame window

04.Notification of active speaker

05.Support L10N customized

06.Notification of current sharing type

07.New interface of get current meeting id

08.New interface of hide video thumnails

09.New interface of pre-populate register email and user name when join webinar

10.Support select sharing app window customized

11.Notification of meeting ui action

12.New interface of change the main window to no video mode.

13.Notification of proxy detect complete

14.New interface of get call-in number list

15.Add more interface to get user information

16.Add more interface of meeting settings

17.New interface of split screen mode

18.New interface of schedule/edit meeting dialog, same as zoom windows client.

19.Support Airhost dialog customized

20.bug fix

## 2017-06-08 @ [v4.0.35674.0608](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.0.35674.0608)

### Added

1. Lock share status notify

2. Support switch video wall to next page feature

3. Support join leave VoIP feature

4. Support get meeting type feature

5. Support get user role feature

6. Breakout room feature enhancement

7. Webinar feature enhancement

8. Waiting room feature enhancement

9. More settings support:
    1> Support disable input meeting password dialog
    2> Allow or disallow "can unmute by self if mute by host" flag
    3> Support hide enter and exit full screen button

10. Bug fix

## 2017-04-12 @ [v4.0.29637.0413](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.0.29637.0413)

### Added

1. Webinar promote and depromote meeting status change notify

2. Join and leave Breakout room meeting status change notify

3. Show or hide invite button in meeting ui and callback invite button click message support

4. Add new interface for H323 password

5. Bug Fix

## 2017-03-10 @ [4.0.26042.0307](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.0.26042.0307)

### Added

1. Add host change callback

2. Add spotlight video change callback

3. Add self record privilige change callback

4. Add Low Or Raise Hand Status change callback

5. Bug Fix

## 2017-03-02 @ [v4.0.22918.0213](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.0.22918.0213)

### Added

1. Enhancement of proxy
   zoom_sdk.h
    - New interface:
		SDK_API SDKError CreateNetworkConnectionHelper(INetworkConnectio Helper** ppNetworkHelper);
        network_connection_handler_interface.h
    - New callback event:
        virtual void onProxySettingNotification(IProxySettingHandler* handler) = 0;

2. Enhancement of SSL cert Verification
   zoom_sdk.h
    - New interface:
    	SDK_API SDKError CreateNetworkConnectionHelper(INetworkConnectionHelper** ppNetworkHelper);
    	network_connection_handler_interface.h
    - New callback event:
    	virtual void onSSLCertVerifyNotification(ISSLCertVerificationHandler* handler    ) = 0;

3. Video/Audio session connection quality API
    meeting_service_interface.h
    - New interface:
       virtual ConnectionQuality GetAudioConnQuality() = 0;
       virtual ConnectionQuality GetVideoConnQuality() = 0;

4. Bugs fix

## 2017-02-10 @ [v4.0.21754.0118](https://github.com/zoom/zoom-sdk-windows/releases/tag/v4.0.21754.0118)

### Added

1. Support waiting room

2. Support embedded browser feature

3. Refine the sdk demo project, add VS2015 support

5. Bug Fix

## 2017-01-20 @ [v3.6.12148.1115](https://github.com/zoom/zoom-sdk-windows/releases/tag/v3.6.12148.1115)

### Added

1. Support to join Webinar meeting with as Panelist Support to pin/spotlight video

2. Support to pause/resume screen sharing Support H.323/SIP callout directly

3. Support invite by Phone andCall Medirectly

4. Add watermark - Powered by Zoom

5. Support to start/join meeting without audio

6. Support to start/join meeting without video

7. Support Multi-share

8. New interface in ISettingService

9. New interface in IMeetingConfiguration

10. Refine IMeetingService interface

## 2016-11-15

### Added

1. Add new interface for get windows handle

2. Fix branding issue in setting dialog, whiteboard and airhost window

3. Fix participant id don't take effect when start/join meeting

## 2016-10-05

### Added

1. fix leave meeting wnd cut off issue

## 2016-06-05

### Added

1. Support login zoom user
