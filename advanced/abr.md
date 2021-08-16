# Controlling the ABR

There are wide array of properties that can be adjusted to control the behavior of various aspects of the player. Properties are identified with an integer identifier from the NexProperty enumeration.

## Properties

### NXPropertySupportABR (116)

If set to 1, enables Adaptive Bit Rate (ABR) support.

**Type:** boolean

**Default:** 1

### NXPropertyMaxBW (117)

When usinG ABR, this is the maximum allowable bandwidth.

Any track with a bandwidth greater than this value will not be played back.

?> To take effect, this property should be set before calling `NexPlayer.open.NexPlayer.setProperty(MAX_BW)` can be used to set the bandwidth limit for initial segments of content, which are downloaded shortly after NexPlayer opens. To change the maximum allowable bandwidth dynamically while content is playing, please call the method changeMaxBandWidth instead.
 
This property should be set to zero for no maximum.

**Unit:** bps (bits per second)

**Default:** 0 (no maximum)

### NXPropertyMinBW (516)

When using ABR, this is the minimum allowable bandwidth.

Any track with a bandwidth smaller than this value will not be played back.

?> To dynamically set a minimum bandwidth allowed while content is playing, please call the method `NexABRController::changeMinBandWidth()` instead. This property should be set to zero for no minimum.
 
**Unit:** bps (bits per second)

**Default:** 0 (no minimum)

### NXPropertyMaxHeight (126)

Limits the maximum height (in pixels) of the video tracks that can be selected during streaming play.

This is used to prevent NexPlayer from attempting to play tracks that are encoded at too high a resolution for the device to handle effectively. NexPlayer will instead select a track with a lower resolution.

**Unit:** pixels

**Default:** 0x7FFFFFFF

### NXPropertyMaxWidth (125)

Limits the maximum width (in pixels) of the video tracks that can be selected during streaming play.

This is used to prevent NexPlayer from attempting to play tracks that are encoded at too high a resolution for the device to handle effectively. NexPlayer will instead select a track with a lower resolution.

**Unit:** pixels

**Default:** 0x7FFFFFFF
 
### NXPropertyStartNearestBW (555)

Sets a target bandwidth (before playing the content) when selecting which track to play as playback starts.

While NexPlayer automatically chooses an ideal track to play based on several factors including device capability and network conditions, there may be situations in which starting playback from a track with a bandwidth near a particular bandwidth is desired.

When this property is set, NexPlayer selects and starts playing the track in content that has the bandwidth closest to the set bandwidth value, initially ignoring other factors.

Note that as playback continues, the track played may change as NexPlayer judges all factors that influence streaming playback and chooses the best option.

This property should be called after init but before calling open.

**Unit:** bps (bits per second)

**Default:** null

**Values:** The target bandwidth value, in bits per second (bps). Note that if `NXPropertyStartNearestBW` is set to 0, NexPlayer will play normally, as if this property has not been set.

### NXPropertyEnableTrackdown (131)

Allows NexPlayer to switch to a lower bandwidth track if the resolution or bitrate of the current track is too high for the device to play smoothly.

Under normal operation, NexPlayer switches tracks based only on current network conditions. When this property is enabled, NexPlayer will also switch to a lower bandwidth track if too many frames are skipped during playback.

This is useful for content that is targeted for a variety of devices, some of which may not be powerful enough to handle the higher quality streams.
 
The `NXPropertyTrackdownVideoRatio` property controls the threshold at which the track change will occur, if frames are being skipped.

**Default:** 0

**Values:**

- 0: Normal behavior (switch based on network conditions only)
- 1: Switch based on network conditions and device performance.

### NXPropertyTrackdownVideoRatio (132)

This property controls the ratio of skipped frames that will be tolerated before a track change is forced, if `NXPropertyEnableTrackdown ` is enabled.

The formula used to determine if a track switch is necessary is:

```
(^100) *(RenderedFrames / DecodedFrames) < NXPropertyTrackdownVideoRatio
```

In other words, if this property is set to 70, and `NXPropertyEnableTrackdown` is set to 1, NexPlayer will require that at least 70% of the decoded frames be displayed. If less than 70% can be displayed (greater than 30% skipped frames), then the next lower bandwidth track will be selected.

A performance-based track switch **permanently** limits the maximum bandwidth of tracks that are eligible for playback until the content is closed. For this reason, setting this ratio higher than the default value of 70 is strongly discouraged (This differs from the bandwidth-based algorithm, which continuously adapts to current network bandwidth).

**Range:** 0 to 100

**Default:** 70

### NXPropertyHLSRunmode (133)

Controls the algorithm used for bitrate switching when playing an HLS stream.

**Default:** 0

**Values:**

- **0:** Use a more aggressive algorithm: up-switching happens sooner.
- **1:** Use a more conservative algorithm: up-switching happens only if a significant amount of extra bandwidth is available beyond that required to support the given bitrate.

## API Reference

### NXPlayerABRController Clas

This interface must be implemented in order for the application to set a minimum or maximum allowable bandwidth, or both, for playing streaming content.

#### changeBandwidthMin

```objc
- (NXError) changeBandwidthMin: (NSUInteger)minMax:(NSUInteger)max
```

This method sets the minimum and maximum bandwidth for streaming content in NexPlayer, dynamically during
playback.

?> To dynamically change the minimum and maximum bandwidth in the middle of playback, please use this method. To take effect, this method should be called after calling open. Note that the minimum, and maximum bandwith can also be set before play begins by setting the properties, NXPropertyMinBW, with changeMinBandwidth. and NXPropertyMaxBW, with changeMaxBandwidth.

This applies in cases where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the minimum, and over the maximum bandwidth when determining whether a track change is appropriate, even if it detects less, and more bandwidth available.

Note that to remove a minimum and maximum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set both of min, and max to 0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| min | Minimum bandwidth in kbps (kilobits per second). To reset to no minimum bandwidth,min = 0x00000000.  |
| max | Maximum bandwidth in kbps (kilobits per second). To reset to no maximum bandwidth,max = 0x00000000. |

**Returns**

NXErrorNone for success, or a non-zero NexPlayer error code in the event of a failure.

#### changeMaxBandwidth

```objc
- (NXError) changeMaxBandwidth: (NSUInteger)max
```
This method sets the maximum bandwidth for streaming content in NexPlayer, dynamically during playback.

?> To dynamically change the maximum bandwidth in the middle of playback, please use this method. To take effect, this method should be called after calling open. Note that the maximum bandwith can also be set before play begins by setting the `NXProperty,NXPropertyMaxBW`, with `changeMaxBandwidth`.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track over the maximum bandwidth when determining whether a track change is appropriate, even if it detects more bandwidth available.

Note that to remove a maximum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set max to 0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| max | Maximum bandwidth in kbps (kilo bits per second). To reset to no maximum bandwidth, set max= 0x00000000. |

**Returns**

NXErrorNone for success, or a non-zero NexPlayer error code in the event of a failure.

#### changeMinBandwidth

```objc
- (NXError) changeMinBandwidth: (NSUInteger)min
```

This method sets the minimum bandwidth for streaming content in NexPlayer, dynamically during playback.

?> To dynamically change the minimum bandwidth in the middle of playback, please use this method. To take effect, this method should be called after callin gopen. Note that the minimum bandwith can also be set before play begins by setting the `NXProperty,NXPropertyMinBW`, with `changeMinBandwidth`.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the minimum bandwidth when determining whether a track change is appropriate, even if it detects less bandwidth available.

Note that to remove a minimum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set min to0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| min | Minimum bandwidth in kbps (kilo bits per second). To reset to no minimum bandwidth, set min= 0x00000000.|

**Returns**

NXErrorNone if successful, otherwise nil if there was an error.

#### setABREnabled

```objc
- (NXError) setABREnabled: (BOOL)enabled
```

This method sets whether or not ABR methods should be used.

In general, NexPlayer plays streaming content, including content with multiple tracks at different bandwidths such as HLS, by choosing the optimal track according to network conditions and device performance. This is the default behavior of NexPlayer and this occurs when ABR is enabled (or calling `NXPlayerABRController::setABREnabled` with the parameter enabled set to YES).

However, there may be instances when an application may want to set limits on which tracks should be selected and played by NexPlayer in order to provide a specific user experience, and to force NexPlayer to stay on a particular bandwidth track, regardless of network conditions. In cases like this, in order to keep playing a track at a target bandwidth (set with `NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption:`) this method must be called to disable NexPlayer’s ABR behavior (with the parameter enabled set to NO).

?> This method must be called with enabled set to NO before calling NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption: if the application should continue playing the target bandwidth regardless of network conditions.

**Parameters**

| Name  | Description  | 
|---|---|
| enabled |- **YES** : ABR enabled. NexPlayer will handle track changes automatically. <br>- **NO** : ABR disabled. NexPlayer will continue playing the target bandwidth track set, regardless of network conditions.

**Returns**

NXErrorNone if successful, otherwise non-zero if there was an error.

**See Also**

`NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption:`


#### setTargetBandwidth

```objc
- (NXError) setTargetBandwidth: (NSUInteger)targetBwBpssegmentOption:(NexBandwidthSegmentOption)segOptiontargetOption:(NexBandwidthTargetOption)targetOption
```
This method sets the target bandwidth for streaming playback dynamically during playback.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the target bandwidth and over the target bandwidth when determining whether a track change is appropriate, even if it detects less and more bandwidth available.

**Parameters**

| Name  | Description  | 
|---|---|
| targetBwBps | Target bandwidth in bps (bits per second). |
| segOption | One of the following NexBandwidthSegmentOption values, indicating how to handle buffered content when the track changes: <br> - **NexBandwidthSegmentOptionDefault = 0** : Default (NexPlayer will decide between NexBandwidthSegmentOptionQuickMix (changing tracks quickly) and NexBandwidthSegmentOptionLateMix (playing buffered content and changing tracks more slowly)). <br> -**NexBandwidthSegmentOptionQuickMix = 1** : NexPlayer will clear the buffer as much as possible and will start to download new track so user can see a new track faster. <br>- **NexBandwidthSegmentOptionLateMix = 2** : NexPlayer will preserve and play the content segments already buffered and will download a new track.
| targetOption | How to use the target bandwidth value set. One of the following NexBandwidthTargetOption options: <br>- **NexBandwidthTargetOptionDefault = 0** : Default target option (NexBandwidthTargetOptionBelow). <br>- **NexBandwidthTargetOptionBelow = 1** : Select a track with a bandwidth below the target bandwidth. <br>- **NexBandwidthTargetOptionAbove = 2** : Select a track with a bandwidth above the target bandwidth. <br>- **NexBandwidthTargetOptionMatch = 3** : Select the track that has a bandwidth that matches the target set; otherwise send an error and no new target bandwidth is selected.

?> This method should be called after open: (NXPlayer).

**Returns**

NXErrorNone if successful, otherwise non-zero if there was an error.

**See Also**

- `setABREnabled:`

### NXPlayerABRControllerTrackChangeParams Struct

Bandwidth information for ABRControl.

This structure is used by `NXABRDelegate` protocol to control ABR track switch and it includes bandwidth information.

**Public Attributes**

- `netBW` The current network bandwidth.
- `curTrackBW` The current track bandwidth.
- `nextTrackBW` The target track bandwidth.


### NXABRDelegate Protocol

This protocol defines a delegate protocol for the application to receive an ABR Track switch event from NexPlayer.

NexPlayer will call the methods provided in this interface automatically during playback to notify the application when an ABR Track switch event has occurred.

In most cases, the handling of this event is optional; NexPlayer will continue to play content normally without the application doing anything special in response to the event received.

#### willChangeABRTrackWithParams

```
- (NSUInteger) - nexPlayer:willChangeABRTrackWithParams:
```

**Parameters**

| Name  | Description  | 
|---|---|
| nxplayer | The NXPlayer instance that this delegate has been assigned to.|
| params | The NXPlayerABRControllerTrackChangeParams structure which consists of bandwidth information.|

**Returns**

The exact track bandwidth that the user wants to set to forcibly.