# Optimizing the Playback

There are a wide array of properties that can be adjusted to control the behavior of various aspects of the player. Properties are identified with an integer identifier from the NXProperty enumeration.

### NXPropertyAVSyncOffset

Adjusts A/V synchronization by of setting video relative to audio. Positive values cause the video to play faster than the audio, while negative values cause the audio to play faster than the video. Under normal operation, this can be set to zero, but in some cases where the synchronization is bad in the original content, this can be used to correct for the error.

While A/V synchronization is generally optimized internally by NexPlayer, there may occasionally be devices which need to be offset in order to improve overall A/V synchronization. For examples of how to set AV_SET_OFFSET based on the device in use, please see the Sample Application code as well as the introductory section A/V Synchronization section.

Appropriate values for any other problematic devices need to be determined experimentally by testing manually.

* **Type:** integer
* **Unit:** msec (1/1000 sec)
* **Range:** -2000∼+2000
* **Default:** 0

### NXPropertyAudioOnlyTrack

Sets whether to enable or disable the Audio Only track in HLS content. This property should be called after init but before calling open.

- **Type:** int
- **Default:** 1
- **Values:**
    - **0:** Audio Only track disabled.
    - **1:** Audio Only track enabled.

### NXPropertyStartWithAV

Starts video together with or separately from audio. This property starts to play audio and video together when starting, if the video timestamp is slower than audio’s timestamp.

If it is 1, it forces the video and audio to start at the same time. If it is 0, it lets the video and audio to start separately.

* **Type:** boolean
* **Default:** 0 (video and audio will start separately, based on the timestamps)

### NXPropertyPreferAV

Controls whether NexPlayer prefers tracks with both audio and video content. Under normal operation (when this property is set to 0), if the available network bandwidth drops below the minimum needed to play the current track without buffering, the player will immediately switch to a lower bandwidth track, if one is available, to minimize any time spent buffering.

If this property is set to 1, the player will attempt to choose only tracks that include both audio and video content, even if that causes some buffering. However, if the buffering becomes too severe or lasts for an extended time, the player may eventually switch to an audio-only track anyway.

* **Type:** unsigned int
* **Default:** 0 (immediate switching)
* **Values:**
    - **0:** Normal behavior (immediate switching)
    - **1:** Prefer tracks with both audio and video

### NXPropertyApplsLiveViewOption

Live HLS playback option. 

- **Values:**

    * **NXPropertyHLSLiveViewRecent** Starts playback from the 3rd segment from the last. For example, if manifest have 1.ts, 2.ts, 3.ts, 4.ts, 5.ts then playback will start from the beginning of 3.ts.

    * **NXPropertyHLSLiveViewRecentByTargetDuration** Start playback from the most recently received media segement (.ts) files, based on the value set for the EXT-X-TARGETDURATION tag in the HLS live playlist. (The player will begin playback at the media segment that immediately precedes the media segment that is three times (x3) the target duration before the latest media segment file loaded). As a concrete example, if the target duration is set to 12 seconds and the total duration of currently loaded media segments is 48 seconds, playback will begin at the media file that immediately precedes the media segment with the timestamp at 12 (48-36) seconds. If this example HLS playlist includes media segment files 1.ts (duration of 10 seconds), 2.ts (9 sec), 3.ts (11 sec), 4.ts (10 sec), and 5.ts (8 sec), then playback will begin at the first media segment, 1.ts, because it immediate precedes the 2.ts segment (where the timestamp at 12 seconds occurs).

    * **NXPropertyHLSLiveViewFirst** Unconditionally start HLS playback from the first entry in the HLS playlist.

    * **NXPropertyLiveViewLowLatency** Playback starts from a position close to real-time and frame skipping may occur during playback to maintain low latency.

    ?> Note: When EXT-X-PROGRAM-DATE-TIME exists, playback will start from the first segment that is matching with the current time. 

- **Type**: unsigned integer

- **Default**: NXPropertyHLSLiveViewRecent

### NXPropertyLowLatencyBufferOption

Set a low latency buffer option. This must be one of the following **Values:**

* **Values:**
    * **NXPropertyLowLaytencyBufferOptionNone** The latency value is set by INITIAL_BUFFERING_DURATION and RE_BUFFERING_DURATION of NexProperty. It should set the reliable value depending on the bitrate of content and network environment.
    * **NXPropertyLowLaytencyBufferOptionAutoBuffer** The latency value is calculated by the player at runtime. During playback, the latency may increase or decrease because it may change depending on the network environment.
    * **NXPropertyLowLaytencyBufferOptionConstBuffer** The latency value is calculated by the player at the beginning of playback and maintains the value unchanged during playback. The latency increases more than when using Auto Buffer Mode, but the rebuffering will be reduced and will try to maintain constant latency after rebuffering.

- **Type**: unsigned int

- **Default**: NXPropertyLowLaytencyBufferOptionNone

### NXPropertyPreferBandwidth

Sets preferred bandwidth when switching tracks during streaming play. Under normal operation (when this property is zero), if the available network bandwidth drops below the minimum needed to play the current track without buffering, the player will immediately switch to a lower bandwidth track, if one is available, to minimize any time spent buffering.

If this property is set, the player will attempt to choose only tracks above the specified bandwidth, even if that causes some buffering. However, if the buffering becomes too severe or lasts for an extended time, the player may eventually switch to a lower-bandwidth track anyway.

* **Type:** unsigned int
* **Units:** kbps (kilobits/sec)
* **Default:** 0 (immediate switching)
* **Values:**
    * **0:** No preferred bandwidth (immediate switching)

?> 0: Preferred bandwidth in kbps

### NXPropertyPreferLanguage

Sets the language of both audio and text played in multi-stream content. It can be used to set the preferred language of audio and text streams to be displayed in content, before NexPlayer begins playing content.

This property should be set by calling setProperty:toValue: (NXPlayer) after init and before open is called, as demonstrated in the following sample code:

```swift
player.setProperty(NXPropertyPreferLanguage, value: "eng" as NSObject)
```

* **Type:** String
* **Default:** null
* **Values:** Accurate language labels as Strings. For example, “eng” for English.

?> Note: Accurate language labels (not the name of a text stream) should be used for the values of this property.

### NXPropertyPreferLanguageAudio

Sets the language to use for audio in multi-stream content, before content is played. This property can be used to set the preferred language of audio streams to be used in content, before NexPlayer begins playing content.

This property should be set by calling setProperty after init and before open is called.

To set the preferred language for both audio and text streams to the same language, use the NXPropertyPreferLanguage instead.

* **Type:** String
* **Default:** null
* **Values:** Accurate language labels as Strings. For example, “eng” for English.

?> Warning: To change any media stream while content is playing, the method setVideoStream:audioStream:textStream:trackAttributes: should be called instead.

?> Note: Accurate language labels (not the name of a text stream) should be used for the values of this property.

### NXPropertyPreferLanguageText

Sets the language to use for text in multi-stream content, before content is played.

This property can be used to set the preferred language of text streams to be displayed in content,before NexPlayer begins playing content.

This property should be set by calling setProperty: after init and before open is called.

* **Type:** String
* **Default:** null
* **Values:** Accurate language labels asStrings. For example, “eng” for English.

?> Warning: To change any media stream while content is playing, the method setVideoStream:audioStream:textStream:trackAttributes: should be called instead. To set the preferred language for both audio and text streams to the same language, use the NXPropertyPreferLanguage instead.

?> Note: Accurate language labels (not the name of a text stream) should be used for the values of this property.

### NXPropertyNotOpenPlayAudio

Prevents the audio track from playing back when set to TRUE (1).

* **Type:** boolean
* **Default:** 0

### NXPropertyNotOpenPlayText

Prevents the text (subtitle) track from playing back when set to TRUE (1).

* **Type:** boolean
* **Default:** 0

### NXPropertyNotOpenPlayVideo

Prevents the video track from playing back when set to TRUE (1).

* **Type:** boolean
* **Default:** 0