# Low latency

Low latency technology can make the user view the live content as close to real-time as possible.

### How to enable low latency mode

You can enable the low latency mode by using the below properties.

```swift
nexPlayer.setProperty(NXPropertyLiveViewOption, 
                toValue: Int(NXPropertyLiveViewLowLatency))
nexPlayer.setProperty(NXPropertyPartialPrefetch, value: 1 as NSObject)
```

### How to adjust the latency

You can further configure and optimise the playback by using these options:

#### Buffering option 1

Manual Mode the latency value is set by `NXPropertyInitialBufferingDuration` and `NXPropertyReBufferingDuration` of NexProperty. It should set the reliable value depending on the bitrate of content and network environment.

```swift
nexPlayer.setProperty(NXPropertyLowLatencyBufferOption, 
                value: NXPropertyLowLaytencyBufferOptionNone as NSObject)
```

* Case 1.  
    For Ultra Low Latency This mode would be suitable for a managed network maintaining constant bandwidth(ex. Video services based on broadband). The latency might be around 1000ms. 

```swift
player.setProperty(NXPropertyInitialBufferingDuration, value: 500 as NSObject)
player.setProperty(NXPropertyReBufferingDuration, value: 500 as NSObject)
```

?> Buffering may frequently occur when bandwidth (Throughput) is not sufficient to deliver a segment or chunk in time.

* Case 2.  
    For Low Latency This mode would be suitable for public networks such as WiFi and LTE. The latency might be around 3000ms. 

```swift
player.setProperty(NXPropertyInitialBufferingDuration, value: 2000 as NSObject)
player.setProperty(NXPropertyReBufferingDuration, value: 2000 as NSObject)
```

?> Buffering will rarely occur, but the latency will be slightly longer than the initial buffering time you set up.

* Case 3.  
    Adjust latency for HLS. In the case of HLS, the player has a disadvantage in low latency perspective than DASH:
    * The player should reload the playlist in order to figure out the URL for the next segment.
    * According to the HLS spec., the player MUST wait for at least the duration of the last segment in the Playlist before attempting to reload the Playlist file again.
    * HLS does not have the availabilityStartTime of the segment that is defined in DASH. Therefore, the player does not know when the next segment becomes available. For this reason, we would recommend setting the buffering time to a little bit longer value than the target duration. If the target duration is 2 seconds, then we recommend setting the buffering time as below. Otherwise, buffering may occur frequently.

```swift
player.setProperty(NXPropertyInitialBufferingDuration, value: 4000 as NSObject)
player.setProperty(NXPropertyReBufferingDuration, value: 4000 as NSObject)
```


#### Buffering option 2

Auto Buffer Mode. The latency value is calculated by the player at runtime. During playback, the latency may increase or decrease because it may change depending on the network environment.  

Example :

```swift
nexPlayer.setProperty(NXPropertyLowLatencyBufferOption, 
                value: NXPropertyLowLaytencyBufferOptionAutoBuffer as NSObject)
```

#### Buffering option 3

Constant Buffer Mode. The latency value is calculated by the player at the beginning of playback and maintains the value unchanged during playback. The latency increases more than when using Auto Buffer Mode, but the rebuffering will be reduced, and try to maintain constant latency after rebuffering.

Example :

```swift
nexPlayer.setProperty(NXPropertyLowLatencyBufferOption, 
                value: NXPropertyLowLaytencyBufferOptionConstBuffer as NSObject)
```
