# Closed Captions

## Subtitles

The NexPlayer supports a variety of subtitle formats including:

1. Local subtitle files (.srt/.smi/.sub)
2. 3GPP and CFF (TTML) timed text
3. CEA 608 closed captions
4. EIA 708 closed captions
5. Web Video Text Tracks (WebVTT)

?> In content where both CEA 608/708 closed captions and WebVTT text tracks exist, NexPlayer will automatically display the WebVTT text cues but this can be changed by setting the NexProperty. `NXPropertyEnableWebVTT` to 0 with setProperty.

### Local Subtitles

For subtitles, the path of the subtitle file or the URL to load the subtitle file should be passed to the player in the *subtitlePath* parameter of NexPlayer.open when content is opened. When streaming content contains subtitles, however, this *smiPath* should be set to *null* to avoid undefined behavior.

?> Only use NexPlayer.open to load local subtitles.

### Other Caption Formats

* *NXCEA608CellInfo*:  
    CEA-608 caption cell information. This structure is used by to store CEA 608 closed caption cell information and is passed to **NXCEA608CaptionView** to be displayed.
* *NXCEA608CaptionView*:  
    This view receives and displays CEA 608 closed captions. This interface must be implemented in order for CEA 608 closed captions to be displayed.
* *NXPlayerCEA608CaptionUpdateReceiver*:  
    Specifies a receiver to be notified of changes to the current CEA 608 closed caption information.

```swift
// Somewhere in the class code
nexPlayer.cea608CaptionUpdateReceiver = self

extension NexVideoPlayer: NXPlayerCEA608CaptionUpdateReceiver {
    func nexPlayer( _ nxplayer: NXPlayer!, 
                    updatedCaption caption: NXCEA608Caption!, 
                    for channel: NXCEA608Channel) {
        ...
    }
}
```

* *NXPlayerContentInfoUpdateReceiver*:  
    Specifies a receiver to be notified of changes to the current content information.

### Rendering Captions with NexCaption Painter

* *NXCaptionAttribute*:  
    This interface controls the color, size, background, alignment, font, bold of the captions used.
* *NXCaptionRenderController*. This class does three things:  
    1. Caption attribute with the info.
    2. Visibility of captions.
    3. Clear the captions.  

This classes allow you to make your own caption style modifiying the properties of the captions.

## Properties

### NXPropertyEnableCEA708 & NXPropertyEnableEIA708

Enables rendering and display of CEA 708 closed captions in content when available.

While CEA 608 closed captions are always enabled, it is necessary to set this property to 1 in order for NexPlayer to support CEA 708 closed captions.  
In the case where content contains both CEA 608 and CEA 708 closed captions and this property enables CEA 708 closed captions, the application will have to handle choosing which captions to render and display to the user.

```swift
nexPlayer.setProperty(NXPropertyEnableEIA708, value: 1 as NSObject);
nexPlayer.setProperty(NXPropertyEnableCEA708, value: 1 as NSObject);
```

* **Type:** boolean
* **Default:** 0
* **Values:**
	 * 0: CEA 708 closed captions disabled.
	 * 1: CEA 708 closed captions enabled.

### NXPropertyEnableWebVTT

Sets whether or not to display WebVTT text tracks automatically when they are included in content. In the case when both CEA 708 closed captions and WebVTT text tracks are included in content, this property can be used to set whether to display the WebVTT text tracks or the closed captions automatically.

By default, this property is set to 1 to enable WebVTT text tracks automatically if they exist in content (as was the behavior of NexPlayer previously). If for some reason it would be preferable that CEA 708 closed captions be displayed instead of the WebVTT text tracks, this property should be set to 0 with by with setProperty.

This property should only be called once, immediately after calling init but before calling open.

* **Type:** boolean
* **Default:** 1 (WebVTT text tracks enabled)
* **Values:**
    * 0 : WebVTT text tracks ignored; CEA 708 closed captions enabled
    * 1 : WebVTT text tracks enabled; CEA 708 closed captions ignored