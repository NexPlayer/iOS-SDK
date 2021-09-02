# NexPlayer™ SDK for iOS Release Notes

### Version 5.40.1.5156
- [Improve] Improve setTargetBandwidth API with QUICK_MIX option for faster track changes
- [Improve] Improve multiple player instance stability

### Version 5.40.1.5155
- [Add] Added new functionality to get content information
- [Add] Added EMSG events for HLS/fMP4
- [Fix] Fixed an issue with SET_PRESENTATION_DELAY property

### Version 5.40.1.5154
- [Add] Added new functionality to get content information

### Version 5.40.1.5152
- [Fix] Fixed an issue with the pssh key for Widevine

### Version 5.40.1.5150
- [Update] Support Widevine Key Renewal
- [Fix] Fixed an issue for specific type of DRM contents
- [Update] Introduce a parameter to disable WV logs

### Version 5.40.1.5144
- [Optimization] Optimization for multiview playback

### Version 5.40.1.5143
- [Fixed] Fixed a crash when device loses the connection
- [Optimization] Optimise SPD feature to work with no-audio streams

### Version 5.40.1.5142
- [Update] Updated SW Widevine library(15.2.4)

### Version 5.40.1.5137
- [Update] Updated SW Widevine library(14.4.1)

### Version 5.40.1.5136
- [Update] Updated SW Widevine library(14.4.0).
- [Update] Updated SPD work.
- [Update] Updated low latency work including ABR support.
  
### Version 5.40.0.5133
- [Update] Improved Widevine workflow. Applied changed WV key rotation in iOS and matched up iOS workflow with Android
- [Update] Applied latest DAA(Dolby Audio for Applications v3.5) library. AC3 and AC4 codecs are combined into Dolby codec
- [Add] Added WebView in iOS for internal test
- [Update] Applied the latest GoogleInteractiveMediaAds.framework

### Version 5.39.0.5127
- [Update] Improved Low-Latency performance.
- [Update] Supported DASH SPD(Suggested Presentation Delay) feature.
- [Update] Improved Mpeg-TS Parser.

### Version 5.38.0.5122
- [Add] Added Playback Rate (speed control) feature. 
- [Update] Improved Low-Latency performance. 
- [Update] Removed 32bit architecture (armv7, armv7s, i386) 
- [Add] Added ASiD watermarking feature.
- [Add] Added property for Unity.
- [Update] Improved stability using the getProgramDateTime method.
- [Update] Improved HW decoder to support HEVC main10 & mainSP.

### Version 5.36.0.5117
- [Add] Added Low-Latency feature.
- [Update] Support for Swift 4 (xcode 9.3)
- [Update] Improved stability using Widevine DRM. 

### Version 5.35.0.5108
- [Add] Added widevine callback after receiving data from LicenseServer.
- [Update] Improved external subtitles performance.
- [Add] Supported HW decoding on HEVC codec after iOS 11. 
- [Update] Improved dynamic thumbnail performance.
- [Update] Improved subtitles performance.
- [Update] Improved stability of the subtitle parser.
- [Update] Improved stability of playback in the offline mode.
- [Update] Improved stability of playback using Widevine DRM.
- [Update] Improved audio codec init routine.
- [Update] Improved start-up time for PD(progressive download) content.
- [Update] Improved file parser.

### Version 5.34.0.5102
- [Updated] Changed setProperty/getProperty to treat integer value.
- [Add] Supported Dolby AC4 codec.
- [Update] Updated VAST samples (AD point, skippable,...).
- [Add] Supported AirPlay
- [Update] Updated swift samples to support VPAID.
- [Update] Improved HLS Widevine module to support multi-key.
- [Optimization] Improved start time logic.

### Version 5.33.0.5097
- [Optimization] Improved all build settings.


###  Version 5.33.0.5096
- [Add] Supported below features of HLS V7.
- [Update] Added codecID value in TrackInfomation.
- [Update] Improved the TTML decoder.

* Version 5.32.1.5092
- [Update] Support for Swift 3
- [Optimization] Improved video decoder module to endure the decoding fails.
- [Optimization] Improved caption renderer rescaling logic.
- [Optimization] Improved TTML text multi tracks in ID3 tags.

### Version 5.32.0.5090
- [Add] Property added to enable TTML text tracks in ID3 tags.
- [Update] added NXHttpStateDelegate in NXStatisticsAPI to receive HTTP state information. 
- [Update] Updated video layout to support rotation in background.

### Version 5.31.1.5086
- [Update] Updated Verimatrix module
- [Update] Improved caption handling
- [Update] Improved TTML subtitle parser.

### Version 5.31.0.5084
- [Update] Improved DTS HPX performances.
- [Update] Improved animation effects on video render.

###  Version 5.31.0.5083
- [Update] Support custom caption attributes.
- [Update] OpenSSL version 1.0.2k.
- [Optimization] Supported animation effects on video render.
- [Optimization] Improved redirection processing with MSS.
- [Fix] Missed text frame when calling setMediaStream with the same track.
- [Fix] Resized font size depending on rotation.
- [Optimization] Supported close in opening status.
- [Fixed] Handled an exceptional case that widevine license server responses with invalid data.

### Version 5.30.1.5079
- [Update] Added a new sample code version including more API references.
- [Update] Improved reconnectNetwork API for supporting DASH and Smooth Streaming.
- [Optimization] Improved TTML renderer.
- [Optimization] Improved NxPlayerView layout calculation.

### Version 5.30.0.5075
- [Fix] Fixed CTS wrap-around logic.

### Version 5.30.0.5074
- [Update] Updated to redraw captionView right after rotating.
- [Update] Updated to find stream logic at CompletedAsyncCmdSetMediaStream.
- [Update] Improved video quality in devices with retina displayes.
- [Update] Extended API setExternalSubtitle to disable external subtitle (backwards compatible).
- [Update] Support added for byte-range request with redirection server in DASH content.
- [Update] Improved ​DTS HPX performances.
- [Add] Added backgroundMode property in NxPlayer to play continuously in background (backwards compatible).
- [Add] Added APis for supporting multi-delegate feature.
- [Optimization] Improved TTML caption renderer.
- [Improvement] Elimination of meaningless warnings. 
- [Fix] Fixed wrong mediaType in completedAsyncCmdMediaOnOff.
- [Fix] Changed return values of NEXPLAYERHLSAES128DescrambleCallbackFunc and NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc for matching with several callbacks.
- [Fix] Fixed wrong positions of image type caption.

### Version 5.29.0.5068
- [Add] Support NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc.
- [Add] Support Http redirection in DASH protocol.
- [Add] Added APIs setMediaOnOff and isMediaOnOff, to disable/enable the media stream of content(audio/video/text).
- [Update] Support ARC.
- [Fix] Improved NexPlayer playback routine in IPV6 network.
- [Fix] Fixed an error that it is not working ABR when playing Smooth Streaming content for some specific cases.
- [Fix] Added exception routine that if http response data recevied from server is bigger than 2KB, it isn't sent to UI.
- [Fix] Fixed the issue where closed caption was flikered.

### Version 5.28.1.5062
- [Fixed] Fixed the issue where audio did not play in encrypted DASH content.
- [Update] Improved the LogLevel module. 

### Version 5.28.0.5058
- [Fixed] Fixed an issue where the player sent the wrong parameter of nexPlayer:mediaTypeChangedTo: delegate method.
- [Fixed] Added captionType in NXContentInfo.
- [Fixed] Fixed the issue where the player didn't call deinit of AudioRenderer in certain cases.
- [Added] Added completedAsyncCmdSetMediaStreamWithResult delegate.
- [Fixed] Fixed an issue where the player returned an incorrect eNEXPLAYER_HTTP_INVALID_RESPONSE event value.
- [Fixed] Fixed an issue of the unmatching A/V sync when playing some contents.
- [Fixed] Fixed an issue of the returned error when re-initiailizing codec.
- [Fixed] Fixed an issue where all types of C-level DRM callback APIs mismatched in the 64-bit system.
- [Fixed] Fixed all types of DRM and descramblers for the 64-bit environment.
- [Fixed] Fixed an issue of the player showing incorrect subtitles in certain contents.
- [Fixed] Fixed an issue where the dynamic thumbnail did not work in certain cases.
- [Fixed] Fixed an issue of the player not playing certain contents downloaded through offline playback.
- [Fixed] Fixed an issue of the incorrect track change in some certain cases.
- [Fixed] Fixed an issue of the player not switching media streams normally in some contents.
- [Fixed] Fixed an issue of the WMV8 content not playing properly.

### Version 5.27.1.5056
- [Fixed] Fixed an issue ​where ​​the ​3GPP subtitle didn't show properly in specific cases​.​
- [Fixed] Fixed an issue​ where​ the seeking​ action​ while buffering​ failed in specific cases.​
- [Update] Updated the ​Verimatrix ViewRight Web Client to version

### Version 5.27.0.5053
- [Add] Added ​the ​resume and pause feature​s​ for offline download​ing.​
- [Fixed] Fixed ​when the ​SRT/SMI subtitle ​was ​not erased for specific cases​.​
- [Fixed] Fixed a crash caused by ​an ​invalid TimedMeta frame.
- [Add] Added ​a ​feature of external license file support.
- [Add] Added samples for VAST integration.
- [Add] Added APIs for support​ing ​C-level DRM callback​s.​
- [Update] Improved ​the ​TTML renderer.
- [Add] Added ​the ​Dynamic Thumbnail feature for HLS and Smooth Streaming.
- [Add] Added ​the ​client​-​side timeshift feature.
- [Add] Added properties for setting ​a ​proxy server.
- [Add] Added an external ABR Delegate to receive track ​switch ​even​​t​s​.
- [Add] Now supporting DASH subtitle​s.

### Version 5.26.3.5044
- [Update] Updated the ​Verimatrix ViewRight Web Client to version 3.8.1.1 with iOS 9 support​.​
- [Add] Added DTS-HPX integration.
- [Add] Added new APIs : setExternalSubtitle to NXPlayer for setting external subtitle​s​ during playback.
- [Add] Added nexPlayer:didReceiveInformativeEvent:details : method to NXPlayerDelegate :​ ​protocol to support​ the​ remote subtitle​s​ download feature ​on ​iOS SDK.
- [Add] Added NexInformativeEvent type : NexInformativeEventDownloadBegan, NexInformativeEventDownloadFinished and defined ​the ​detailed event parameter keys : pkNexInformativeEventURL, kNexInformativeEventResult
- [Add] Added new APIs : setTargetBandwidth and setABREnabled to NXPlayerABRController
- [Add] Added a new Property NXPropertyContinueDownloadAtPause to enable buffering in pause state.
- [Add] Added NexAudioPostProcessingAdapter API class and delegate protocol to support external audio processing.
- [Add] Added DolbyIntegration and NexDolbySoundSettings classes to support ​Dolby approval with AC3 codec and integration.

### Version 5.25.5.5036
- [Update] Updated Verimatrix ViewRight Web Client to version 3.8.1.0 with iOS 9 support
- [Add] Added NexVideoTextureReceiver API class
- [Add] Added addHTTPHeaderFields: API method to NXPlayer
- [Add] Added goToCurrentLivePosition: API method to NXPlayer

### Version 5.24.1.5029
- [Update] Update support for Swift 2.0 in iOS SDK

### Version 5.24.0.5028
- [Add] Added Offline playback feature on iOS SDK
- [Add] Added support for Swift in iOS SDK
- [Add] Added iOS Statistics API 
- [Fixed] Can’t disable logging

### Version 5.23.0.5014
- [Add] Added nexPlayer:onModifyHTTPRequest: method to NXPlayerDelegate protocol to support NXPropertyEnableModifyHTTPRequest when used to modify HTTP requests sent to the remote server.

### Version 5.22.1.5013
- [Fixed] Removed private API call that prevents App Store Review approval.

### Version 5.22.0.5012
- [Update] Updated Verimatrix ViewRight Web Client to version 3.7 with 64-bit architecture support.
- [Add] Added support for iOS 8 Video Toolbox (hardware accelerated) H.264 decoder.
- [Add] Added APIs for caption renderer control: NXCaptionRenderController.h - captionAttribute, captionHidden, clearCaptionView
- [Add] Added property to decide rendering mode (text or caption mode) for CEA 608 closed captions: NXProperty.h - NXPropertyCEA608TextMode

### Version 5.21.1.5009
- [Update] Improved linking flexibility

### Version 5.21.0.5005
- [Update] Added support for 64-bit architecture.
- [Add] Added new APIs: changeMinBandwidth, changeMaxBandwidth, changeBandwidthMin: Max to set a maximum or minimum limit (or both) to control which tracks will be played in multi-track content, regardless of the bandwidth available.

### Version 5.20.0.4726
- [Add] Added new properties: numDecodingVideoFrames and numRenderingVideoFrames.
- [Update] Update WebVTT caption renderer.

### Version 5.19.0.4722
- [Add] Added new callbacks: onHTTPResponse() and onHTTPRequest()

### Version 5.18.0.4720
- [Add] Added a new API: getSARInfo.
- [Update] Improved stability of startFromTime API.
- [Update] Improved handling of timed metadata.

### Version 5.17.0.4715
- [Add] Added new function to extract all the ID3 metadata, including customised tags, on the content.
- [Add] Added a callback for simple caption text.
- [Updated] Improved stability of VMDRM feature. 

### Version 5.16.0.4707
- [Add] Supports Verimatrix ViewRight 3.5 
- [Add] Plain text rendering of additional streaming caption formats supported: CEA708 closed captions and WebVTT
- [Add] Added DASH DRM session delegate, NXDashDRMSessionDelegate.h.
- [Add] Added a new NXPlayerView property,  captionHidden, to hide captions. 
- [Update] NXPlayerView.CEA608CaptionView deprecated.  May return nil when captions are not CEA608. Use captionHidden instead.

### Version 5.15.6.4695
- [Fixed] Increase stack size for all tasks.

### Version 5.15.5.4690
- [Fixed] Removed absolute addressing - apply PIE.

### Version 5.15.4.4687
- [Fixed] Changed identifierForVender instead of UDID.

### Version 5.15.3.4685
- [Fixed] Fixed an issue with CFF PD.

### Version 5.15.2.4390
- [Fixed] Support large local files.

### Version 5.15.2.4298
- [New] Support 3GPP Timed Text
- [New] Support CFF Timed Text
- [New] Support Armv7s architecture
- [Fixed] Fixed an issue with Smooth Streaming captions
- [Fixed] Fixed issues with parsing of PIFF content
- [Updated] Updated HTTP header option to remove "Content-length:0".

### Version 5.11.5.4122
- [New] Added DECE UV Descrambler callback.
- [New] IGNORE_ABNORMAL_SEGMENT_TIMESTAMP property is added for supporting download file skip feature in HLS.
- [New] Added property "START_WITH_AV".
- [New] Added exception routine to prevent crashing in getContentInfo function. 
- [Fixed] Fixed an issue with distorted H264 content. H264 decoder is updated. 
- [Fixed] Fixed issues with wrong subtitle frames being delivered in the case of Pause - Resume repetition. 
- [Fixed] Fixed an issue in Live content where even when BufferSeek Range was available, Seekable Range sometimes returned INVALID_4BYTE value. 
- [Fixed] Full support for all HLS Version 4 (07) Multi Stream use cases added.
- [Fixed] Fixed an issue with Audio duration being shorter than Video duration. 
- [Fixed] Fixed an issue with PIFF DRM - Reader updated.   
- [Fixed] Fixed an issue with subtitles on SmoothStreaming Content. 
- [Fixed] Fixed an issue with initialization of ContentInformatoion function. 
- [Fixed] Fixed an issue with PIFF DRM content. PIFF DRM can now be handled.
- [Fixed] Fixed issues with TrackDown and TrackDisable situation with HLS. (Freezing video problem)
- [Updated] Enabled server-side timeshift feature of HLS. 
- [Updated] Seek processing time is improved.
- [Updated]Improved server-side timeshift of HLS.
- [Removed]Removed property "MAX_SKIP_FRAME_CNT"
- [Removed]Removed property "SMOOTH_SKIPPING"

### Version 5.9.0.3470
- [NEW API] NXPropertySetLiveBackOff 
- [NEW API] NXPropertySetLiveBackOffset
- [NEW API] NXHTTPCredentialsProvider::
    HTTPCredentialHeadersForHTTPStatusCode:responseData: 
- [NEW API] NXSmoothStreamFragmentDescrambler::
    descrambleSmoothStreamingFragmentForPlayer:inputBuffer:
    inputBufferSize:outputBuffer:outputBufferSize:
    mediaFileURL:parentPlaylistURL:
    (Added mediaFileURL and parentPlaylistURL parameters)
- [NEW API] NXManifestAndPlaylistDescrambler
- [NEW API] NXPlayer::manifestAndPlaylistDescrambler
- [NEW API] NXPDBlockDescrambler
- [NEW API] NXPlayer::PDBlockDescrambler
- [NEW API] NXPiffPlayReadyDescrambler
- [NEW API] NXPlayer::piffPlayReadyDescrambler
- [NEW API] NXPlayerDelegate::nexPlayer:playlistReceived:forURL:
- [API CHANGE] NXPlayer::addRTSPHeaderField:forMethods: now works even if the header field already exists; if the header field exists, the new value replaces the original value.
- [New] Support for HLS Version 4
- [New] Support for LiveBackOff (moving the "live" streaming point back away from the actual live position via  NXPropertySetLiveBackOff).
- [Fixed] Fixed an issue where two or or more "Set-Cookie" headers in the same response were not being handled. 
- [Fixed] Fixed an issue with PIFF local content
- [Fixed] Fixed an issue playing SmoothStreaming content
- [Fixed] Fixed an issue handling the user-agent tag.
- [Fixed] Fixed an issue handling ID3TimedMeta information
- [Fixed] Fixed an issue with PIFF PlayReady DRM (added Sample Encryption Box size check)
- [Fixed] Fixed an issue with the server-side timeshift feature.
- [Fixed] Fixed an issue where SSL sockets might occasionally have been leaked.
- [Update] Improved robustness of local caption support
- [Update] Improved robustness of smooth streaming subtitles
- [Update] Improved general streaming robustness
- [Update] Improved handling of H.264 content
- [Update] Improved handling of AVI container format
- [Update] Fixed issue causing video freeze in certain cases during HLS track switching
