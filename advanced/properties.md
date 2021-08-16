
# Properties

There are a wide array of properties that can be adjusted to control the behavior of various aspects of the player, from buffer time (how many seconds of streaming content are buffered before playback begins) to the behavior of the player under various error conditions (whether or not to allow audio-only playback if an unsupported video codec is detected, for example).

Properties can be set and retrieved through:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

Properties are identified with an integer identifier from the NXProperty enumeration.

The value of each property is an unsigned integer. For some properties, it may be necessary to cast this to a different type. See the individual property documentation for details. If no type is specified, it is safe to treat the property as an unsigned integer.

## enum NXProperty

Property identifiers.
These identify properties that can be set and retrieved with:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

### NXPropertyTimestampDifferenceVDispWait

The number of milliseconds (as a negative number) that video is allowed to run ahead of audio before the player waits for audio to catch up. For example, -20 means that if the current video time is more than 20msec ahead of the audio time, the current video frame will not be displayed until the audio catches up to the same time stamp. This is used to adjust video and audio synchronization.

- **Type:** int(should be negative) 
- **Default:** -20 (20msec) 
- **Units:** msec

### NXPropertyTimestampDifferenceVDispSkip

 The number of milliseconds that video is allowed to run behind audio before the system begins skipping frames to maintain synchronization. For example, 200 means that if the current video time is more than 200msec behind the audio time, the current video frame will be skipped. This is used to adjust video and audio synchronization.

 - **Type:** unsigned int 
 - **Units:** msec 
 - **Default:** 200 (0.2 sec)

### NXPropertySocketConnectionTimeout

Amount of time to wait before timing out when establishing a connection to the server. If the connection to the server (the socket connection) cannot be established within the specified time, an error event will be generated and playback will not start.

Set this to zero to disable timeout (NexPlayer will wait indefinitely for a connection).

- **Type:** unsigned int 
- **Default:** 0 (infinite) 
- **Units:** msec (0 for infinite)

### NXPropertyRTPPortMin 

The minimum port number to be used when receiving RTP data. This sets the minimum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- **Default:** 12000

### NXPropertyRTPPortMax

The maximum port number to be used when receiving RTP data. The maximum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- **Default:** 30000

### NXPropertyProxyAddress

Sets the proxy address. :{String} 

- **Default:** null

### NXPropertyProxyPort

Sets the proxy port number. 

- **Type:** integer 
- **Default:** 0
 
### NXPropertyAVInitOption 

Controls when video initialization happens. This can be any of the following **Values:**
 
 - **NXPropertyAVInitOption_Partial** If there is an audio track, wait for audio initialization to complete before initializing video.

 - **NXPropertyAVInitOption_All** Begin video initialization as soon as there is any video data, without any relation to the audio track status.
 
- **Default:** NXPropertyAVInitOption_All

### NXPropertyPlayableForNotSupportAudioCodec

If set to 1, allows media playback even if the audio codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- **Type:** unsigned int 
- **Default:** 0

### NXPropertyPlayableForNotSupportVideoCodec

If set to 1, allows media playback even if the video codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- **Type:** unsigned int
- **Default:** 0

### NXPropertyUseEyePleaser

If more than this number of frames are skipped during rendering, the remaining frames up to the next keyframe are forcibly discarded and playback resumes from the next keyframe.

- **Type:** unsigned int 
- **Default:** 0xFFFFFFFF
 

### NXPropertyUserAgentString 

RTSP/HTTP User Agent value. 

-  **Type:** String

### NXPropertyFirstDisplayVideoFrame

Controls what is displayed while the player is waiting for audio data. If this is set to zero, the player will not display the first video frame until the audio is ready to play. Whatever was previously displayed will continue to be visible (typically a black frame) while it is waiting for audio data.

If this is set to 1, and video data becomes available prior to audio data, the first video frame will be displayed as a still image until audio data is available. 

Once audio has started, the behavior for both settings is the same; this only affects what is displayed while the player is waiting for audio data.

Under old versions of the SDK (prior to the addition of this property), the default behavior was as though this property were set to zero.

 - **Type:** boolean 
 - **Default:** 1
 - **Values:**
	- **0:** Show nothing.
	- **1:** Show first video frame.

### NXPropertySourceOpenTimeOut 

Sets the amount of time to wait for an open request to complete. This is used when NexPlayer tries to open new media. If there is no response from the server for longer than the amount of time specified here, the open request will be stopped and `nexPlayer:completedAsyncCmdOpenWithResult:playbackType:` will be called with the result, namely the error code, NXErrorMediaOpenTimeout.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 300000 (300 seconds)

### NXPropertySocketOperationTimeout

The maximum waiting time till an HTTP request/response message arrives to NexPlayer. If the reply does not arrive within this time after HTTP request message is sent to the streaming server, it will be regarded as an error.

- **Type:** unsigned int 
- **Default:** 30,000 (30 seconds
- **Units:** msec (0 for infinite)  

### NXPropertySeekRangeFromRAPoint 

Sets the range where NexPlayer will seek to a Random Access point rather than the exact target position provided in the seekToAdjustedTime API.

> **Warning** This property is only valid when the second parameter, exact, in the seekToAdjustedTime API is true.

Setting this value is a kind of option for the seekToAdjustedTime API and can be used to minimize the time required to seek in content by taking advantage of Random Access points in the content. A Random Access point is a specific position that the parser is allowed to seek to directly.

This value sets the range where NexPlayer will seek from a Random Access point given by the parser to a target position that equals msec(milliseconds), the first parameter in the seek() API.

If the exact parameter, the second parameter in the seekToAdjustedTime API, is true and the difference between a Random Access point and the target position is within this value, seekToAdjustedTime will find and seek to the exact target position. If the exact parameter is set to true and the difference between a Random Access point and the target position is beyond this range, seek will give up the accurate target point and will instead seek to and play from the Random Access point.

For example, if NexPlayer is seeking to 10000 ms exactly (exact = true) and there is a Random Access point at 7000 ms, if this property is set to less than 3000 ms, the player will ignore the exact target value and will instead play from 7000 ms. On the other hand, if this property is set to more than 3000 ms, then NexPlayer will seek exactly to 10000 ms and begin playback.

> **Warning** Please remember that in order to seek to a target position, audio or video frames have to be decoded. If too large of a value is set here, it may cause the seek process to consume an excessive amount of time especially in high resolution video content.

- **Type:** unsigned int 
- **Units:** msec (1/1000 sec) 
- **Default:** 10000 (10 seconds)

### NXPropertySetToSkipBFrame 

If set to true, unconditionally skips all B-frames without decoding them.

- **Type:** boolean 
- **Default:** 0

**NXPropertyTooMuchLostFrameDuration** Maximum amount of silence to insert to make up for lost audio frames. Under normal operation, if audio frames are lost (if there is a time gap in received audio frames), silence will be inserted automatically to make up the gap.

However, if the number of audio frames lost represents a span of time larger than the value set for this property, it is assumed that there is a network problem or some other abnormal condition and silence is not inserted.

This prevents, for example, a corruption in the time stamp in an audio frame from causing the system to insert an exceptionally long period of silence (which could possibly prevent further audio playback or cause other unusual behavior).

- **Type:** unsigned int 
- **Units:** msec (1/1000 sec) 
- **Default:** 20000 (20 seconds)

### NXPropertySupportLocal

If set to 1, enables local file playback support.

- **Type:** boolean
- **Default:** 1

### NXPropertySupportPD

If set to 1, enables progressive download support.

- **Type:** boolean
- **Default:** 1

### NXPropertySupportWMS 

If set to 1, enables Microsoft Windows Media Streaming support.

- **Type:** boolean
- **Default:** 0

### NXPropertySupportRDT 

If set to 1, enables Real Media Streaming support.

- **Type:** boolean
- **Default:** 0

### NXPropertySupportAppleHTTP

If set to 1, enables Apple HTTP Live Streaming (HLS) support.
 
- **Type:** boolean
- **Default:** 1

### NXPropertySupportDash 

If set to 1, enables DASH support.

- **Type:** boolean
- **Default:** 1

### NXPropertyH264Profile

Limits the H.264 profile that can be selected from an HLS playlist. Under normal operation, the track with the highest supported H.264 profile is selected from an HLS playlist. If this property is set, no track with a profile higher than this value will be selected. This should be set to zero for no limit.

- **Type:** unsigned integer
- **Default:** 0 (use any profile),

### NXPropertyIgnoreAudioLostFrame 

Suppresses automatic silence insertion for lost audio frames. During normal RTSP streaming operation, if an audio frame is lost (for example, due to a bad connection), the NexPlayer engine inserts a frame of silence into the audio stream to maintain synchronization. Enabling this setting suppresses that function. This may improve performance in some cases where the RTSP server doesn’t send an audio stream. This should be used with caution as it can cause the audio and video streams to lose synchronization.

- **Default:** 0 (disabled)
- **Values:**
	- **0:** disabled
	- **1:** enabled

### NXPropertyIgnoreAVSync

Bypasses AV synchronization. When this property is enabled, AV synchronization is bypassed. As soon as data is received, it is immediately presented to the user.

> **Warning** This will almost certainly cause the audio and video to lose synchronization, and video playback speed will be unpredictable and vary depending on the speed of the connection and the speed by which the local system can decode frames. This may be useful for playing back a live video feed where frames are sent by the server at the correct intervals for playback.
 
- **Default:** 0 (disabled)
- **Values:**
	- **0:** disabled
	- **1:** enabled

### NXPropertySupportMSSmoothStreaming 

If set to 1, this enables MS Smooth Streaming support.

 - **Type:** boolean
 - **Default:** 1

### NXPropertyHTTPCredentials 

Adds additional HTTP headers to use to supply credentials when a 401 response is received from the server. The string should be in the form of zero or more HTTP headers
(header name and value), and each header (including the last) should be terminated with a CRLF sequence, for example:
 
```id: test1\r\npw: 12345\r\n```

The particulars of the headers depend on the server and the authentication method being used.

- **Type:** String
 

### NXPropertyUseSyncTask

Sets whether or not NexPlayer should use SyncTask feature. SyncTask may improve decoding performance.

> **Note** This property must be set before initializing NexPlayer or opening and playing content.

- **Type:** unsigned int
- **Default:** 0 
- Values :
	- **0:** Do not use SyncTask.
	- **1:** Use SyncTask.

### NXPropertySetCookie 

Controls whether the player honors cookies sent by the server.
 
- **Type:** unsigned int
- **Default:** 1
- **Values:**
	- **0:** Ignore HTTP cookie headers sent by the server.
	- **1:** Cookie headers received from a streaming server along with the initial manifest or playlist are included with further HTTP requests during the session.

### NXPropertySetLiveBackOff 

Sets the SmoothStreamingLiveBackOff property when playing Smooth Streaming content. This property sets the duration of content (closest to live) that cannot yet be accessed or downloaded by the player. It is like setting how long to wait before asking for the latest fragment in a live presentation, and thus basically sets the played "live" point back from the actual live content available on the server.

The end-to-end latency of the player (what is being played "live" in the player compared to what is available live on the server) is at least the duration ofLiveBackOff added to the duration set for LivePlaybackOffset with NXPropertySetLiveBackOffset.

- **Type:** unsigned int
- **Units:**msec
- **Default:** 6000

### NXPropertySetLiveBackOffset 

Sets the Smooth Streaming LivePlaybackOffset property when playing Smooth Streaming content. This property sets the duration away from the live position to start playback when joining a live presentation when the LiveView option is set to "Recent", but excludes the `LiveBackOff` duration (set by NXPropertySetLiveBackOff).

As a result, live content will be played behind the actual live position by a duration determined by BOTH `LiveBackOff` and the value for `LivePlaybackOffset` set here.

Setting this property enables faster startup because it allows a buffer to be built up as fast as bandwidth will support (potentially faster than real time), which creates a buffer against network jitter. It does however also increase end-to-end latency, which means what is played "live" in the player is farther behind the actual live playing point of the content.

- **Type:** unsigned int 
- **Units:** msec
- **Default:** 7000

### NXPropertyIgnoreAbnormalSegmentTimestamp 

Ignores abnormal segment timestamps. If it is 1 or enabled, NexPlayer will ignore abnormal segment timestamps. If it is 0 or disabled, NexPlayer will not ignore any abnormal segment timestamps.

 - **Type:** boolean
 
> **Warning** This property is not supported in this API version.

### NXPropertyEnableModifyHTTPRequest 

Allows the application to modify the content of an HTTP Request that NexPlayer is about to send to a remote HTTP server. When this property is set equal to 1 (enabled), NexPlayer invokes `nexPlayer:onModifyHttpRequest:` with the HTTP Request as an argument. The application can return the modified version of the HTTP Request that will actually be sent.

- **Values:**
	- **0:** Disabled. Don’t deliver any HTTP Request.
	- **1:** Enabled. Deliver HTTP Request to modify on the application side.

> **See Also** `NXPlayerDelegate.h::NXPlayerDelegate:nexPlayer:onModifyHTTPRequest:` for more information.

### NXPropertyOpenMediaFileFromSpecifiedTS 

Allows NexPlayer to begin downloading content media files from a specified time stamp in the content.

> **Warning** This property is currently only supported for VOD in HTTP Live Streaming (HLS).
 
NexPlayer allows users to start playback in the middle of a content file with the start api, but typically, before playback can begin, the player still opens content from the first media file available and then has to receive all of the media files between the first file and the point where the user would like to start playback.

When playback is to start in the middle of content, this property allows the player to skip receiving the unneeded earlier media files based on the time stamp value set by the application, and instead begin downloading media files from a position closer to the specified time stamp instead.

This property can thus reduce the time needed to open and start playing a media file in the middle of VOD content.

> **Note** This property must be set before NexPlayer.open is called.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 s)
- **Default:** 0xFFFFFFFF


### NXPropertyWebVTTWaitOpen 

Avoids waiting for the first WebVTT segment to download when starting to play content. This property can be used when playing WebVTT content. By default, NexPlayer waits until the first WebVTT segment is downloaded before content begins to play so that no caption text will be missed.

However, if this property is disabled (set to 0), the player will start playing content as soon as possible (instead of waiting until the first WebVTT segment is fully downloaded). This may be preferred if content should start playing as quickly as possible (although initial WebVTT text may be missed).

This property should be called once, immediately after calling init but before calling open.

- **Type:** boolean
- **Default:** 1
- **Values:**
	- **0:** Content starts playing before first WebVTT segment is downloaded.
	- **1:** Content starts playing after first WebVTT segment is downloaded.


### NXPropertySegmentTSReliable 

Sets whether or not to trust a content segment’s timestamp when playback starts. 

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 1
- **Values:**
	- **0:** Adjust the timestamp during playback.
	- **1:** Trust the timestamp during playback.

### NXPropertySuggestedPresentationDelayTime 

This property overrides the suggestedPresentationDelay value of the DASH manifest.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 2000 (2 sec)

### NXPropertyEnableSpdSyncToGlobalTime 

Enables synchronization to UTC time(SPD).  

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 0
- **Values:**
	- **0:** SPD disabled.
	- **1:** SPD enabled.

### NXPropertySpdSyncDiffTime 

If the current playback is not more synchronized than this value, the player will speed up playback and make sync.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 300 (300 msec)

### NXPropertySpdTooMuchDiffTime 

If playback is out of sync than this value, the player will jump to synchronize the video rather than make it by speeding up.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 5000 (5 seconds)

### NXPropertySetHWdecoderPixelFormat 

Sets iOS HW decoder pixel format of output property `kCVPixelBufferPixelFormatTypeKey`. This property is to set a pixel format for decoded video format. Have to set it before start to play.

- **Type:** int
- **Default:** 0 (kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange)
- **Values:**
	- **0:** If you want to develop iOS application, you should use this.`kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange`
	- **1:** If you want to develop Unity application, you should use this. `kCVPixelFormatType_32BGRA`

### NXPropertySetMaxCaptionLength 

Set it to extend max caption length.

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 8192

### NXPropertyRFCBufferPageSize 

Controls the size of each page in the remote file cache. Use caution when adjusting this value. Improper settings may adversely affect performance, or may cause some content to fail to play.

See NXPropertyRFCBufferCount for a detailed description.

- **Type:** unsigned int
- **Units:** kilobytes
- **Default:** 512

### NXPropertyCEA608TextMode 

This property sets whether CEA 608 closed captions should be rendered in caption mode or text mode. 

- **Type:** boolean
- **Default:** 0
- **Values:**
	- **0:** Render CEA 608 closed captions in caption mode.
	- **1:** Render CEA 608 closed captions in text mode.

## Types

### Classes 

- struct NexAudioPostProcessingParams
    
 The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio post-processor, which implements the NexAudioPostProcessingAdapterDelegate protocol.

- struct NexVideoRawBits
 
 This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

- struct NEXPLAYERRemoteFileIOInterface
    
 A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

- struct NXCEA608CellInfo
 
 CEA-608 caption cell information.

- struct NXSARInfo
 
 SAR (Sample Aspect Ratio) of H.264 contents.

### Macros

\#define NXDuration_Unknown (0xFFFFFFFFU)

For live streams where duration of content cannot be determined, this type can be passed in place of NXDuration.

### Typedefs

- typedef struct NexAudioPostProcessingParams NexAudioPostProcessingParams

 The characteristics of audio samples to be provided by `NexAudioPostProcessingAdapter` to the audio post-processor, which implements the `NexAudioPostProcessingAdapterDelegate` protocol.

- typedef void(∧UpdatedTextureBlock) (NexVideoTexture ∗texture)
 
 This method is called when a new video texture is available to be rendered from the caller.

- typedef struct NexVideoRawBits NexVideoRawBits
 
 This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

- typedef enum NXDRMDataType_ NXDRMDataType
 
 Type of data being passed for DRM descrambling.

- typedef void ∗NEXFileHandle
 
 File handle used in Remote File I/O callbacks.

- typedef enum _NEXFileMode NEXFileMode
 
 File open mode.

- typedef enum _NEXFileSeekOrigin NEXFileSeekOrigin
 
 Origin for Remove File I/O callback seek operations.

- typedef struct NEXPLAYERRemoteFileIOInterface_ NEXPLAYERRemoteFileIOInterface
 
 A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

- typedef NSUInteger NXDuration
 
 Represents the duration of the content as a span of time in milliseconds.

- typedef void ∗NXFileHandle

 Opaque file handle.

- typedef enum NXFileMode_ NXFileMode
 
 Mode for opening a file.

- typedef enum NXFileSeekOrigin_ NXFileSeekOrigin
 
 Origin when seeking within a file.

- typedef enum NXDRMType_ NXDRMType
 
 DRM types.

- typedef enum NXKeepAliveSendMode_ NXKeepAliveSendMode

 Keep alive send modes.

- typedef enum NXFileFormat_ NXFileFormat

 File formats.

- typedef enum NXRTSPOptions_ NXRTSPOptions
 
 RTSP options.

### Enumerations

### NXBufferInfoMediaType

This enumeration defines the possible stream type for NXBufferInfoMediaType.
 
```
enum NXBufferInfoMediaType { 
	NXBufferInfoMediaTypeVideo = 0x0, 
	NXBufferInfoMediaTypeAudio = 0x2,
	NXBufferInfoMediaTypeText = 0x3 
}
```

### NXBufferingState

This enumeration defines the possible buffering state for NXBufferingState.

```
enum NXBufferingState { 
	NXBufferingStatePaused** = 0x0, 
	NXBufferingStateResume** = 0x1 
}
```

### NXDeviceInfoConnectionType

NexPlayer connection types.

```
enum NXDeviceInfoConnectionType { 
	NXDeviceInfoConnectionTypeUnknown, 
	NXDeviceInfoConnectionTypeNone, 
	NXDeviceInfoConnectionTypeWWAN, 
	NXDeviceInfoConnectionTypeWiFi 
}
```

### NXDRMDataType_    

Type of data being passed for DRM descrambling.       

```
enum NXDRMDataType_ { 
	NXDRMDataTypeVideo = 0, 
	NXDRMDataTypeAudio = 1 
}
```
    

### NexHLSTSDescrambleResult

This enumeration defines the possible return values from a NXHLSTSDescrambler method.

```
enum NexHLSTSDescrambleResult { 
	NexHLSTSDescrambleResultSucceed = 0, 
	NexHLSTSDescrambleResultNeedMoreBuffer = 1, 
	NexHLSTSDescrambleResultError
}
```

### NXHttpStateInfoFileType

An enumeration of the possible types of files being handled by NexPlayer during playback.

```       
enum NXHttpStateInfoFileType{
	NXHttpStateInfoFileTypeUnknown = 0, 
	NXHttpStateInfoFileTypeMPD = 1, 
	NXHttpStateInfoFileTypeSegment = 2, 
	NXHttpStateInfoFileTypeInitialSegment = 3,
	NXHttpStateInfoFileTypeKey = 4, 
	NXHttpStateInfoFileTypeSegmentIndex = 5 
}
```      

### _NEXFileMode

File open mode.

```
enum _NEXFileMode { 
	NEX_FILE_READ = 1, 
	NEX_FILE_WRITE = 2, 
	NEX_FILE_READWRITE = 3, 
	NEX_FILE_CREATE = 4 
}
```

### _NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

```
enum _NEXFileSeekOrigin { 
	NEX_SEEK_BEGIN = 0, 
	NEX_SEEK_CUR = 1, 
	NEX_SEEK_END = 2 
}
```
    
### NXOpenMode    

Open modes
    
```
enum NXOpenMode {
	NXOpenModeAuto = 0, 
	NXOpenModeLocal = 1, 
	NXOpenModeStreaming = 2, 
	NXOpenModeLocalBundle = 3,
    NXOpenModeLocalDocs = 4, 
    NXOpenModeStoreStream = 5 
}
```

### NXOnOffDefault 

```   
enum NXOnOffDefault { 
	NXDefault = 0, 
	NXOff = 1, 
	NXOn = 2 
}
```

### NXPlaybackType

Playback types.

```
enum NXPlaybackType { 
	NXPlaybackTypeLocal = 0, 
	NXPlaybackTypeStreaming = 1 
}
```

### NXTransportType

Transport layers (TCP and UDP) for RTP and RTCP packets.


```
enum NXTransportType { 
	NXTransportTypeTCP = 0, 
	NXTransportTypeUDP = 1 
}
```

### NXPlayerState

Possible states of the player (paused, stopped, etc.).

```
enum NXPlayerState {
    NXPlayerStateNone = 0, 
    NXPlayerStateClose = 1, 
    NXPlayerStateStop = 2, 
    NXPlayerStatePlay = 3,
    NXPlayerStatePause = 4 
}
```

### NXRTSPMethod

RTSP method identifiers.

```
enum NXRTSPMethod {
    NXRTSPMethodNone = 0x00000000, 
    NXRTSPMethodDescribe = 0x00000001, 
    NXRTSPMethodSetup = 0x00000002, 
    NXRTSPMethodPlay = 0x00000004,
    NXRTSPMethodPause = 0x00000008, 
    NXRTSPMethodTeardown = 0x00000010, 
    NXRTSPMethodOptions = 0x00000020, 
    NXRTSPMethodRedirect = 0x00000040,
    NXRTSPMethodSetParameter = 0x00000080, 
    NXRTSPMethodGetParameter = 0x00000100, 
    NXRTSPMethodAnnounce = 0x00000200, 
    NXRTSPMethodPlaylist = 0x00000400,
    NXRTSPMethodAll = 0x0000FFFF 
}
```

### NXCodecID

Codec type identifiers

```
enum NXCodecID {
	NXCodecID_UNKNOWN = 0x00000000, 
	NXCodecID_MPEG4V = 0x10020100, 
	NXCodecID_HEVC = 0x10010400, 
	NXCodecID_H264 = 0x10010300,
	NXCodecID_H263 = 0x10010200, 
	NXCodecID_WMV = 0x10060000, 
	NXCodecID_WMV1 = 0x10060100,
	NXCodecID_WMV2 = 0x10060200,
	NXCodecID_WMV3 = 0x10060300, 
	NXCodecID_DIVX = 0x10040000, 
	NXCodecID_WVC1 = 0x10060400,
	NXCodecID_AAC = 0x20020000,
	NXCodecID_AACPlus = 0x20020100, 
	NXCodecID_WMA = 0x20070000, 
	NXCodecID_WMA1 = 0x20070100, 
	NXCodecID_WMA2 = 0x20070200,
	NXCodecID_MP3 = 0x20010200, 
	NXCodecID_AC3 = 0x20030000, 
	NXCodecID_AC4 = 0x20030200, 
	NXCodecID_EAC3 = 0x20030100,
	NXCodecID_DTS = 0x20040000, 
	NXCodecID_EXTERNAL_SMI = 0x30030100, 
	NXCodecID_EXTERNAL-SRT = 0x30040100, 
	NXCodecID_3GPP_TIMEDTEXT = 0x30010100,
	NXCodecID_TEXT_WEBVTT = 0x300C0100, 
	NXCodecID_TEXT_CC_CEA = 0x300D0100, 
	NXCodecID_TEXT_TTML = 0x300B0100, 
	NXCodecID_VOB_SUB = 0x30060100,
	NXCodecID_MICRODVD_SUB = 0x30070100, 
	NXCodecID_DIVX_XSUB = 0x300E0000, 
	NXCodecID_DIVX_XSUBPLUS = 0x300E0100, 
	NXCodecID_AMR = 0x20180000 
}
```

### NXCEA608Color

CEA 608 Colors

```
enum NXCEA608Color {
    NXCEA608Color_White = 0, 
    NXCEA608Color_White_Semitrans = 1, 
    NXCEA608Color_Green = 2, 
    NXCEA608Color_Green_Semitrans = 3,
    NXCEA608Color_Blue = 4, 
    NXCEA608Color_Blue_Semitrans = 5, 
    NXCEA608Color_Cyan = 6, 
    NXCEA608Color_Cyan_Semitrans = 7,
    NXCEA608Color_Red = 8, 
    NXCEA608Color_Red_Semitrans = 9, 
    NXCEA608Color_Yellow = 10, 
    NXCEA608Color_Yellow_Semitrans = 11,
    NXCEA608Color_Magenta = 12, 
    NXCEA608Color_Magenta_Semitrans = 13, 
    NXCEA608Color_Black = 14,
    NXCEA608Color_Black_Semitrans = 15,
    NXCEA608Color_Transparent = 16, 
    NXCEA608Color_Default = 17, 
    NXCEA608Color_Last = NXCEA608Color_Default 
}
```

### NXCEA608Charset

CEA 608 Character Set IDs.

```
- enum NXCEA608Charset {
	NXCEA608Charset_Unicode = 0, 
	NXCEA608Charset_Private1 = 1, 
	NXCEA608Charset_Private2 = 2, 
	NXCEA608Charset_KSC_5601_1987 = 3,
	NXCEA608Charset_GB_2312_80 = 4 
}
```

### NXMediaType

Media types

```
enum NXMediaType {
	NXMediaTypeUnknown = 0, 
	NXMediaTypeAudio = 1, 
	NXMediaTypeVideo = 2, 
	NXMediaTypeText = 3,
	NXMediaTypeAV = 4 
}
```

### NXCEA608Channel

CEA 608 Channel IDs.

```
enum NXCEA608Channel {
	NXCEA608Channel_None = 0, 
	NXCEA608Channel_Ch1 = 1, 
	NXCEA608Channel_Ch2 = 2, 
	NXCEA608Channel_Ch3 = 3,
	NXCEA608Channel_Ch4 = 4 
}
```

### NXDebugMsgCat

Debugging Messages to include.

```
enum NXDebugMsgCat {
	NXDebugMsgCat_RTSP = 0x00, 
	NXDebugMsgCat_RTP_RECV = 0x01, 
	NXDebugMsgCat_RTP_RECV_END = 0x02, 
	NXDebugMsgCat_RTCP_RR_SEND = 0x03,
	NXDebugMsgCat_RTCP_BYE_RECV = 0x04, 
	NXDebugMsgCat_CONTENT_INFO = 0x05, 
	NXDebugMsgCat_HTTP_RESPONSE = 0x06, 
	NXDebugMsgCat_DOWNLOADED_BUFF = 0x07,
	NXDebugMsgCat_DECODING = 0x08, 
	NXDebugMsgCat_H264_SEI_PICTIMING = 0x09, 
	NXDebugMsgCatEYE_PLEASER_STATE = 0x10, 
	NXDebugMsgCat_HTTP_REQUEST = 0x11,
	NXDebugMsgCat_TIMESHIFT_BUFFERFULL = 0x12 
}
```

### NXFileMode_

Mode for opening a file.

```
enum NXFileMode_ { 
	NXFileModeRead = 1, 
	NXFileModeWrite = 2, 
	NXFileModeReadWrite = 3, 
	NXFileModeCreate = 4 
}
```

### NXFileSeekOrigin_

Origin when seeking within a file.

```
enum NXFileSeekOrigin_ { 
	NXFileSeekOriginBeginning = 0, 
	NXFileSeekOriginCurrent = 1, 
	NXFileSeekOriginEnd = 2 
}
```

### NXDRMType_

DRM types.

```
enum NXDRMType_ { 
	NXDRMTypePayload = 0x01, 
	NXDRMTypePacket = 0x10, 
	NXDRMTypeFrame = 0x20
}
```

### NXScale

Video image scaling modes.

```
enum NXScale {
    NXScale_None = 0, 
    NXScale_OriginalSize = 1, 
    NXScale_FitInView = 2, 
    NXScale_FillView = 3,
    NXScale_Stretch = 4 
}
```

### NXKeepAliveSendMode_

Keep alive send modes.

```
enum NXKeepAliveSendMode_ {
    NXKeepAliveSendMode_None = 0x00000000, 
    NXKeepAliveSendMode_PauseState = 0x00000001, 
    NXKeepAliveSendMode_PlayState = 0x00000002, 
    NXKeepAliveSendMode_PausePlayState = 0x00000003,
    NXKeepAliveSendMode_AllState = 0x000000FF 
}
```

### NXFileFormat_

File formats.

```
enum NXFileFormat_ {
	NXFileFormatMP4 = 0x00000001, 
	NXFileFormatAMRNB = 0x00000002, 
	NXFileFormatAMRWB = 0x00000004, 
	NXFileFormatADIFAAC = 0x00000008,
	NXFileFormatMP3 = 0x00000010, 
	NXFileFormatADTSAAC = 0x00000020, 
	NXFileFormatAVI = 0x00000040,
	NXFileFormatASF = 0x00000080,
	NXFileFormatRMFF = 0x00000100, 
	NXFileFormatMKV = 0x00000200, 
	NXFileFormatPDCF = 0x00000400,
	NXFileFormatOGM = 0x00000800,
	NXFileFormatOGG = 0x00001000, 
	NXFileFormatMPEG_PS = 0x00002000, 
	NXFileFormatMPEG_TS = 0x00004000, 
	NXFileFormatFLV = 0x00008000,
	NXFileFormatQCELP = 0x00010000, 
	NXFileFormatFLAC = 0x00020000, 
	NXFileFormatAPE = 0x00040000,
	NXFileFormatMOV = 0x00080000,
	NXFileFormatWAV = 0x00100000, 
	NXFileFormatNONE = 0x7FFFFFFF 
}
```

### NXRTSPOptions_

RTSP options

```
enum NXRTSPOptions_ {
	NXRTSPOptionsSendModeNone = 0x00000000, 
	NXRTSPOptionsDescribe = 0x00000001, 
	NXRTSPOptionsFirstSetup = 0x00000002, 
	NXRTSPOptionsEverySetup = 0x00000004,
	NXRTSPOptionsFirstPlay = 0x00000008, 
	NXRTSPOptionsEveryPlay = 0x00000010, 
	NXRTSPOptionsFirstPause = 0x00000020, 
	NXRTSPOptionsEveryPause = 0x00000040,
	NXRTSPExtraOptionsWaitResponse = 0x00010000, 
	NXRTSPExtraOptionsNoWaitResponse = 0x00020000
}
```

### NXRTSPOptions_

These are the available log levels for the `setLogLevel: (NXPlayer)`.

```      
- enum NXLogLevel {
    NXLogLevelError = -3, 
    NXLogLevelWarning = -2, 
    NXLogLevelDisabled = -1, 
    NXLogLevelInformation = 0,
    NXLogLevelDebug = 1, 
    NXLogLevelVerbose = 2, 
    NXLogLevelAboveVerbose = 3, 
    NXLogLevelExtraVerbose = 4 
}
```       

### NexAvailableBitrate

This enumeration defines the possible options for the `setVideoBitrates:len:withOption: (NXPlayer)`.

```
enum NexAvailableBitrate {
	NexAvailableBitrateNone = 0, 
	NexAvailableBitrateMatch = 1, 
	NexAvailableBitrateNearest = 2, 	
	NexAvailableBitrateHigh = 3,
	NexAvailableBitrateLow = 4, 
	NexAvailableBitrateInsideRange = 5 
}
```       

### NexInformativeEvent

This enumeration defines the possible events for `NXPlayer::didReceiveInformativeEvent:details:`.

```
enum NexInformativeEvent { 
	NexInformativeEventDownloadBegan = 0, 
	NexInformativeEventDownloadFinished = 1 
}
```

### NexBandwidthSegmentOption

This enumeration defines the possible options for the `NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:`. One of the following NexBandwidthSegmentOption values, indicating how to handle the buffered content when the track switches:
       
```       
enum NexBandwidthSegmentOption { 
	NexBandwidthSegmentOptionDefault = 0, 
	NexBandwidthSegmentOptionQuickMix = 1, 
	NexBandwidthSegmentOptionLateMix = 2 
}
```       

### NexBandwidthTargetOption 
      
This enumeration defines the possible options for the `NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:`. This can be a guide on how to use the target bandwidth value set. One of the following NexBandwidthTargetOptionoptions:       

```
enum NexBandwidthTargetOption { 
	NexBandwidthTargetOptionDefault = 0, 
	NexBandwidthTargetOptionBelow = 1, 
	NexBandwidthTargetOptionAbove = 2, 
	NexBandwidthTargetOptionMatch = 3 
}
```
       
### NexDynamicThumbnailOption 

This enumeration defines IDs for the possible options when handling Dynamic Thumbnail information in HLS & Smooth Streaming content. These are possible values for the uId parameter in `NxPlayer::setOptionDynamicThumbnailwithOption: andParam1: andParam2:`.


```
enum NexDynamicThumbnailOption { 
	NexDynamicThumbnailOptionNone = 0, 
	NexDynamicThumbnailOptionInterval = 1 
}
```

### enum NexDynamicThumbnailOption

Possible types of media which can be played by NexPlayer during playback. The primary use of NXHttpStateInfoMediaType is for representing a media type of NXHttpStateInfoFileTypeSegment.

```
enum NexDynamicThumbnailOption { 
	NexDynamicThumbnailOptionNone = 0, 
	NexDynamicThumbnail = 1 
}
```

### Typedef Documentation

### NexAudioPostProcessingParams 

The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio postprocessor, which implements the NexAudioPostProcessingAdapterDelegate protocol.

```
typedef struct NexAudioPostProcessingParams NexAudioPostProcessingParams
```

### NEXFileHandle

File handle used in Remote File I/O callbacks.

This is the file handle used in calls to the various Remote File I/O callback functions. This value is returned by the file-open callback, and can be any value that the remote file callbacks can use to uniquely identify the open file instance.

```
typedef void∗ NEXFileHandle
```

### NEXFileMode

File open mode.

This is passed by NexPlayer in calls to the `NEXPLAYERRemoteFile_OpenFt` callback.

This is a bitfield, so the constants can be combined with the bitwise-or operator.

- NEX\_FILE\_WRITE | NEX\_FILE\_CREATE Open file for writing; create if it doesn’t exist
- NEX\_FILE\_READ | NEX\_FILE\_WRITE Same as NEX\_FILE\_READWRITE

```
typedef enum_NEXFileMode NEXFileMode
```

### NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

```
typedef enum _NEXFileSeekOrigin NEXFileSeekOrigin
```

**See Also**

 - NEXPLAYERRemoteFile_SeekFt
 - NEXPLAYERRemoteFile_Seek64Ft


### NEXPLAYERRemoteFileIOInterface

A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

This structure provides replacements for the standard operating system file I/O functions. Basically, to play back local content that is not available via the standard operating system file APIs, all calls to open or read from the file are directed to the function pointers in this structure instead.

This structure is passed to the Remote File I/O Interface when registering the callbacks.

More information about each function pointer can be found in the documentation.

```
typedef struct NEXPLAYERRemoteFileIOInterface_ NEXPLAYERRemoteFileIOInterface
```

**See Also**

- NEXPLAYERRemoteFile_OpenFt
- NEXPLAYERRemoteFile_CloseFt
- NEXPLAYERRemoteFile_ReadFt
- NEXPLAYERRemoteFile_SeekFt
- NEXPLAYERRemoteFile_Seek64Ft
- NEXPLAYERRemoteFile_WriteFt
- NEXPLAYERRemoteFile_SizeFt

### NexVideoRawBits

This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

```
typedef structNexVideoRawBits NexVideoRawBits
```

### NXDRMDataType

Type of data being passed for DRM descrambling.

The NXDRMDescrambler protocol handles both audio and video data; this enumeration is used to distinguish between the two when data is passed to the descrambling method.

```
typedef enum NXDRMDataType_ NXDRMDataType
```

### NXDRMType

 DRM types that are returned by DRM descramblers to indicate at what stage the descrambling takes place. Not all DRM descrambling protocols support all types; see the individual descrambler protocol documentation for details.

```
typedef enum NXDRMType_ NXDRMType
```

### NXFileFormat

Possible file format values that can be used for `NXContentInfo::fileFormat`.

```
typedef enum NXFileFormat_ NXFileFormat
```

### NXFileHandle

Opaque file handle. This is an arbitrary value used to identify files in calls to NXRemoteFileIOInterfacemethods. The meaning of this is unique to a given implementation of NXRemoteFileIOInterface, and return values from different implementations should not be mixed.

```
typedef void ∗NXFileHandle
```

**See Also**

- NXRemoteFileIOInterface for more details.

### NXFileMode

Mode for opening a file. Identifies different methods for opening or creating a file. This is is passed to implementations of the `NXRemoteFileIOInterface` protocol to indicate how a file should be opened.

```
typedef enum NXFileMode_ NXFileMode
```

**See Also**

- NXRemoteFileIOInterfacefor more details.

### NXFileSeekOrigin

Origin when seeking within a file. Identifies different origins for seeking within a file. This is is passed to implementations of the NXRemoteFileIOInterface protocol to indicate where to measure the seek offset from.

```
typedef enum NXFileSeekOrigin_ NXFileSeekOrigin
```

**See Also**

- NXRemoteFileIOInterfacefor more details.

### NXKeepAliveSendMode

Keep alive send modes. These are possible values for the `property::NXPropertyKeepAliveSendMode`

See that property for details.

```
typedef enum NXKeepAliveSendMode_ NXKeepAliveSendMode**
```

### NXRTSPOptions

RTSP options. These are possible values for the `::NXPropertyRTSPOptionsSendMode` property.

```
typedef enum NXRTSPOptions_ NXRTSPOptions
```

### UpdatedTextureBlock

This method is called when a new video texture is available to be rendered from the caller.

```
typedef void(∧UpdatedTextureBlock)(NexVideoTexture ∗texture)
```

Parameters

- texture: The new video texture available for rendering.

### Enumeration Type Documentation

### enum _NEXFileMode

File open mode.  This is passed by NexPlayer in calls to the `NEXPLAYERRemoteFile_OpenFt` callback.

This is a bit field, so the constants can be combined with the bitwise-or operator.

```
// Open file for writing; create if it doesn’t exist
NEX_FILE_WRITE | NEX_FILE_CREATE 

// Same as NEX\_FILE\_READWRITE
NEX_FILE_READ | NEX_FILE_WRITE 
```

- `NEX_FILE_READ` Open for reading
- `NEX_FILE_WRITE` Open for writing
- `NEX_FILE_READWRITE` Open for reading and writing
- `NEX_FILE_CREATE` Create the file if it doesn’t exist

### enum _NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

### enum NexAvailableBitrate

This enumeration defines the possible options for the setVideoBitrates:len:withOption: (NXPlayer).

- `NexAvailableBitrateNone` No restriction on subtracks other than the bitrates selected inbitrates.
- `NexAvailableBitrateMatch` Only use subtracks which have exact same bitrate as the selected bitrates passed inbitrates.
- `NexAvailableBitrateNearest` Only use subtracks which have the nearest bitrates to the target bitrates.
- `NexAvailableBitrateHigh` Only use subtracks which have bitrates equal to or higher than the target bitrate.
- `NexAvailableBitrateLow` Only use subtracks which have bitrates equal to or lower than the target bitrate.
- `NexAvailableBitrateInsideRange` Only use subtracks which have bitrates inside the range defined by the bitrates.

### enum NexBandwidthSegmentOption

This enumeration defines the possible options for the `NXPlayerABRController::setTargetBandwidth:withSegmentOption:withTargetOption:`. One of the following NexBandwidthSegmentOptionvalues, indicating how to handle the buffered content when the track switches:

- `NexBandwidthSegmentOptionDefault` Default. NexPlayer will decide between NexBandwidthSegmentOptionQuickMix (switching tracks quickly) and NexBandwidthSegmentOptionLateMix (playing buffered content and changing tracks more slowly).
- `NexBandwidthSegmentOptionQuickMix` NexPlayer will clear the buffer as much as possible and will start to download a new track so the user can switch faster.
- `NexBandwidthSegmentOptionLateMix` NexPlayer will preserve and play the content segments already
buffered, and will download a new track.

### enum NexBandwidthTargetOption

This enumeration defines the possible options for the NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:. This can be a guide on how to use the target bandwidth value set. One of the following NexBandwidthTargetOptionoptions:

- `NexBandwidthTargetOptionDefault` Default target option (NexBandwidthTargetOptionBelow).
- `NexBandwidthTargetOptionBelow` Select a track with a bandwidth below the target bandwidth.
- `NexBandwidthTargetOptionAbove` Select a track with a bandwidth above the target bandwidth.
- `NexBandwidthTargetOptionMatch` Select the track that has a bandwidth that matches the set target. Otherwise send an error and no new target bandwidth will be selected.

### enum NexDynamicThumbnailOption

This enumeration defines IDs for the possible options when handling Dynamic Thumbnail information in HLS & Smooth Streaming content. These are possible values for theuIdparameter in `NxPlayer::setOptionDynamicThumbnailwithOption: andParam1: andParam2:`.

### enum NexHLSTSDescrambleResult

This enumeration defines the possible return values from a NXHLSTSDescrambler method.

### enum NexInformativeEvent

This enumeration defines the possible events for NXPlayer::didReceiveInformativeEvent:details:.

* NexInformativeEventDownloadBegan Download of a URL began. Parameter keys in details: kNexInformativeEventURL.
* NexInformativeEventDownloadFinished Download of a URL finished. Parameter keys in details: kNexInformativeEventURL, and kNexInformativeEventResult.

### enum NXBufferInfoMediaType

This enumeration defines the possible stream type forNXBufferInfoMediaType.

- `NXBufferInfoMediaTypeVideo` Video stream type.
- `NXBufferInfoMediaTypeAudio` Audio stream type.
- `NXBufferInfoMediaTypeText` Text stream type.

### enum NXBufferingState

This enumeration defines the possible buffering state for NXBufferingState.

### enum NXCEA608Channel

CEA 608 Channel IDs. These are possible values for `NXPlayer::selectedCEA608Channel`.

They set the channel from which CEA 608 closed captions will be received. While there are four channels to receive caption information from the NTSC line 21 fields, as channels 1 and 2 share field 1 and channels 3 and 4 share field 2, the most common channels used to receive captions are channels 1 and 3. These channels can represent the same information in different languages and are often intended to be selected by the user from the application.

- `NXCEA608Channel_None` No CEA 608 captions (disable)
- `NXCEA608Channel_Ch1` NTSC line 21 field 1 closed captions (first channel); CEA 608 Caption Channel 1.
- `NXCEA608Channel_Ch2` NTSC line 21 field 1 closed captions (second channel); CEA 608 Caption Channel 2.
- `NXCEA608Channel_Ch3` NTSC line 21 field 2 closed captions (first channel); CEA 608 Caption Channel 3.
- `NXCEA608Channel_Ch4` NTSC line 21 field 2 closed captions (second channel); CEA 608 Caption Channel 4.

### enum NXCEA608Charset

CEA 608 Character Set IDs. These are used to choose the character set to display CEA 608 closed caption information.

- `NXCEA608Charset_Unicode` Unicode character set.
- `NXCEA608Charset_Private1` For use with a private, non-standard character set. May be ignored.
- `NXCEA608Charset_Private2` For use with a private, non-standard character set. May be ignored.
- `NXCEA608Charset_KSC_5601_1987` Korean character set.
- `NXCEA608Charset_GB_2312_80` Chinese character set.

### enum NXCEA608Color

CEA 608 Colors. These are used to indicate the foreground and background colors associated with CEA 608 closed captions. Note that only the semi-transparent options will be used for background color of captions.

### enum NXCodecID

Codec type identifiers. These are used with NXContentInformation::audioCodec, NXContentInformation::videoCodec and NXContentInformation::captionType.

### enum NXDebugMsgCat

Debugging Messages to include. These are possible values forn exPlayer:debugMessage:category: (NXPlayerDelegate-p) and set the debugging messages to be provided.

- `NXDebugMsgCat_RTSP` Debugging information related to the RTSP connection status.
- `NXDebugMsgCat_RTP_RECV` Debugging information associated with the start of an RTP packet receipt.
- `NXDebugMsgCat_RTP_RECV_END` Debugging information associated with the end of an RTP packet receipt.
- `NXDebugMsgCat_RTCP_RR_SEND` Debugging information associated with the transmission of an RTCP RR (Receiver Report) packet.
- `NXDebugMsgCat_RTCP_BYE_RECV` This occurs when an RTCP BYE packet is received.
- `NXDebugMsgCat_CONTENT_INFO` General information about the content that is currently playing.
- `NXDebugMsgCat_HTTP_RESPONSE` Debugging information of HTTP Response.
- `NXDebugMsgCat_DOWNLOADED_BUFF` Debugging information of downloaded buffer.
- `NXDebugMsgCat_DECODING` Debugging information of decoding event.
- `NXDebugMsgCat_H264_SEI_PICTIMING` Debugging information for handling H.264 SEI picture timing information.
- `NXDebugMsgCat_EYE_PLEASER_STATE` Debugging information of Eye-Pleaser State.
- `NXDebugMsgCat_HTTP_REQUEST` Debugging information of HTTP request.
- `NXDebugMsgCat_TIMESHIFT_BUFFERFULL` Debugging information of full of buffer for TimeShift.

### enum NXDeviceInfoConnectionType

NexPlayer connection types.

- `NXDeviceInfoConnectionTypeUnknown` Unknown connection type.
- `NXDeviceInfoConnectionTypeNone` Not connected.
- `NXDeviceInfoConnectionTypeWWAN` Cellular connection.
- `NXDeviceInfoConnectionTypeWiFi` WiFi connection.

### enum NXDRMDataType_

Type of data being passed for DRM descrambling. The NXDRMDescrambler protocol handles both audio and video data; this enumeration is used to distinguish between the two when data is passed to the descrambling method.

### enum NXDRMType_

DRM types. These are returned by DRM descramblers to indicate at what stage the descrambling takes place. Not all DRM descrambling protocols support all types; see the individual descrambler protocol documentation for details.

- `NXDRMTypePayload` Descrambling is done at the payload level.
- `NXDRMTypePacket` Descrambling is done at the packet level.
- `NXDRMTypeFrame` Descrambling is done individually for each frame.

### enum NXFileFormat_

File formats. These are possible file format values that can be used for NXContentInfo::fileFormat.

- `NXFileFormatMP4` MP4.
- `NXFileFormatAMRNB` AMR-NB.
- `NXFileFormatAMRWB` AMR-WB.
- `NXFileFormatADIFAAC` ADIFAAC.
- `NXFileFormatMP3` MP3.
- `NXFileFormatADTSAAC` ADTSAAC.
- `NXFileFormatAVI` AVI.
- `NXFileFormatASF` ASF.
- `NXFileFormatRMFF` RMFF.
- `NXFileFormatMKV` MKV.
- `NXFileFormatPDCF` PDCF.
- `NXFileFormatOGM` OGM.
- `NXFileFormatOGG` OGG.
- `NXFileFormatMPEG_PS` MPEG-PS.
- `NXFileFormatMPEG_TS` MPEG-TS.
- `NXFileFormatFLV` FLV.
- `NXFileFormatQCELP` QCELP.
- `NXFileFormatFLAC` FLAC.
- `NXFileFormatAPE` APE.
- `NXFileFormatMOV` MOV.
- `NXFileFormatWAV` WAV.

### enum NXFileMode_

Mode for opening a file. Identifies different methods for opening or creating a file. This is is passed to implementations of the NXRemoteFileIOInterface protocol to indicate how a file should be opened.

- `NXFileModeRead` Read
- `NXFileModeWrite` Write
- `NXFileModeReadWrite` Read and Write
- `NXFileModeCreate` Create

### enum NXFileSeekOrigin_

Origin when seeking within a file. Identifies different origins for seeking within a file. This is is passed to implementations of the NXRemoteFileIOInterface protocol to indicate where to measure the seek offset from.

- `NXFileSeekOriginBeginning` Beginning of file
- `NXFileSeekOriginCurrent` Current position
- `NXFileSeekOriginEnd` End of file

### enum NXKeepAliveSendMode_

Keep alive send modes. These are possible values for the  property::NXPropertyKeepAliveSendMode

- `NXKeepAliveSendMode_None` None.
- `NXKeepAliveSendMode_PauseState` Pause only.
- `NXKeepAliveSendMode_PlayState` Play only.
- `NXKeepAliveSendMode_PausePlayState` Pause and play.
- `NXKeepAliveSendMode_AllState` All.

### enum NXLogLevel

These are the available log levels for the setLogLevel: (NXPlayer).
The higher the log level, the more logs will be enabled. The following are the log levels in ascending order :

1. NXLogLevelError (Lowest level)
2. NXLogLevelWarning
3. NXLogLevelInformation
4. NXLogLevelDebug
5. NXLogLevelVerbose
6. NXLogLevelAboveVerbose
7. NXLogLevelExtraVerbose (Highest level)

> **Note** NXLogLevelDisabled disables the log.

* `NXLogLevelError` Enables error level log only.
* `NXLogLevelWarning` Enables warning level log and below.
* `NXLogLevelDisabled` Log disabled.
* `NXLogLevelInformation` Enables information level log and below (default)
* `NXLogLevelDebug` Enables debug level log and below.
* `NXLogLevelVerbose` Enables verbose level log and below.
* `NXLogLevelAboveVerbose` Enables above verbose level log and below. This will have more logs than the verbose level.
* `NXLogLevelExtraVerbose` Enables extra verbose level log and below. This will have more logs than the above verbose level.

### enum NXMediaType

Media types. These are used with NXMediaStreamInfo::typeto indicate the type of the stream (audio or video) described by `NXMediaStreamInfo`.

* `NXMediaTypeUnknown` Unknown media type.
* `NXMediaTypeAudio` Audio only stream.
* `NXMediaTypeVideo` Video only stream.
* `NXMediaTypeText` Text stream.
* `NXMediaTypeAV` A/V stream.

### enum NXOpenMode

Open modes. These are possible argument values for mode parameter in open: (NXPlayer).

- `NXOpenModeAuto` Select streaming play for "http:", "https:", "rtsp:" and "mms:" addresses, local play for everything else.
- `NXOpenModeLocal` Plays a local file, given a local path or a URL starting with "file://".
- `NXOpenModeStreaming` Plays streaming video; if a path (not a URL) is given, it is assumed to be a path to an SDP file for an RTSP stream.
- `NXOpenModeLocalBundle` Plays a local file from the current application bundle (a relative path should be passed)
- `NXOpenModeLocalDocs` Plays a local file from the application documents area (the area where files are placed if added via iTunes)
- `NXOpenModeStoreStream` New source type value for storing HLS Stream.

### enum NXPlaybackType

Playback types.

- `NXPlaybackTypeLocal` Content is local (local path or "file://" URL)
- `NXPlaybackTypeStreaming` Content is streaming (including on-demand, progressive download or live)

### enum NXPlayerState

Possible states of the player (paused, stopped, etc.). The current player state is available through `NXPlayer::state`.

- `NXPlayerStateNone` No current valid state (for example API not initialized)
- `NXPlayerStateClose` Content is currently closed.
- `NXPlayerStateStop` Content is open and stopped.
- `NXPlayerStatePlay` Content is open and playing.
- `NXPlayerStatePause` Content is open and paused during playback.

### enum NXRTSPMethod

RTSP method identifiers. These are used withaddRTSPHeaderField:forMethods: (NXPlayer)

- `NXRTSPMethodNone` No RTSP method.
- `NXRTSPMethodDescribe` RTSP DESCRIBE method (request presentation description, generally SDP)
- `NXRTSPMethodSetup` RTSP SETUP method (specify ports, transport, etc.)
- `NXRTSPMethodPlay` RTSP PLAY method (request playback)
- `NXRTSPMethodPause` RTSP PAUSE method (pause playback)
- `NXRTSPMethodTeardown` RTSP TEARDOWN method (stop media streams and terminate session)
- `NXRTSPMethodOptions` RTSP OPTIONS.
- `NXRTSPMethodRedirect` RTSP REDIRECT.
- `NXRTSPMethodSetParameter` RTSP GET PARAMETER.
- `NXRTSPMethodGetParameter` RTSP SET PARAMETER.
- `NXRTSPMethodAnnounce` RTSP ANNOUNCE.
- `NXRTSPMethodPlaylist` RTSP PLAYLIST.
- `NXRTSPMethodAll` Indicates all current and future RTSP method types.

### enum NXRTSPOptions_

RTSP options. These are possible values for the::NXPropertyRTSPOptionsSendModeproperty.

* `NXRTSPOptionsSendModeNone` No send-mode options specified.
* `NXRTSPOptionsDescribe` Send RTSP OPTIONS before RTSP DESCRIBE.
* `NXRTSPOptionsFirstSetup` Send RTSP OPTIONS before the first RTSP SETUP Request.
* `NXRTSPOptionsEverySetup` Send RTSP OPTIONS before every RTSP SETUP Request.
* `NXRTSPOptionsFirstPlay` Send RTSP OPTIONS before the first RTSP PLAY Request.
* `NXRTSPOptionsEveryPlay` Send RTSP OPTIONS before every RTSP PLAY Request.
* `NXRTSPOptionsFirstPause` Send RTSP OPTIONS before the first RTSP PAUSE Request.
* `NXRTSPOptionsEveryPause` Send RTSP OPTIONS before every RTSP PAUSE Request.
* `NXRTSPExtraOptionsWaitResponse` Wait for extra OPTIONS response timeout.
* `NXRTSPExtraOptionsNoWaitResponse` Do not wait for extra OPTIONS response timeout.

### enum NXScale

Video image scaling modes. These are various possible automatic video scaling modes that can be set for NXPlayerView::autoScaling.

* `NXScale_None` No automatic scaling.
* `NXScale_OriginalSize` Original video size.
* `NXScale_FitInView` Fit video to container (as large as possible without cropping; maintain aspect ratio)
* `NXScale_FillView` NexPlayer will fill the parent container (crop and maintain aspect ratio)
* `NXScale_Stretch` Stretch to container dimensions (does not maintain aspect ratio)

### enum NXTransportType

Transport layers (TCP and UDP) for RTP and RTCP packets.

- `NXTransportTypeTCP` RTP/RTCP over TCP.
- `NXTransportTypeUDP` RTP/RTCP over UDP.
