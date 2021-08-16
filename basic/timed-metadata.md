# Timed Metadata

You can listen to Timed Metadata events with NexPlayer iOS SDK. ID3, EMSG DATA and SCTE35 formats are supported.

## Setting Up The Listener

Timed metadata events are reported within the *nexPlayer(_ nxplayer: NXPlayer!, updatedMetaData metaData: [AnyHashable : Any]!)* method of the `NXPlayerDelegate`. This method is called when new timed metadata is ready. Timed metadata includes additional information about the playing content that may be displayed to the user and this information may change at different times through the content. Each time new metadata is available for display, this method is called.

A sample implementation might look like below:

```swift
class YourListener: NXPlayerDelegate {
func nexPlayer(_ nxplayer: NXPlayer!, updatedMetaData metaData: [AnyHashable : Any]!) {
    let keys = [
        kNXTimedMetaKeySessionInfo,
        kNXTimedMetaKeyTitle,
        kNXTimedMetaKeyArtist,
        kNXTimedMetaKeyAlbum,
        kNXTimedMetaKeyGenre,
        kNXTimedMetaKeyYear,
        kNXTimedMetaKeyLyrics,
        kNXTimedMetaKeyTrackNum,
        kNXTimedMetaKeyComment,
        kNXTimedMetaKeyText,
    ]
    
    for  key in keys {
        if let metadata = metaData[key] as? String {
            print("Metadata[\(key)] = \(metadata)")
        }
    }
    
    if let imgData:Data = metaData[kNXTimedMetaKeyImage] as? Data {
        //let image = UIImage(data: imgData)
        print("Metadata image size = \(imgData.count)")
    }
    
    if let extraData = metaData[kNXTimedMetaKeyExtraData] as? [String: NxTimedMetaExtraTag] {
        for key in extraData.keys {
            guard let tag = extraData[key] else {
                continue
            }
            
            if let tagId = tag.tagID {
                print("Metadata extraTag ID = \(tagId)")
            }
            
            if let text = tag.text {
                print("Metadata extraTag Text = \(text)")
            }
            
            if let mimeType = tag.mimeType {
                print("Metadata extraTag MimeType = \(mimeType)")
            }
            
            if let data = tag.data {
                print("Metadata extraTag data size = \(data.count)")
            }
        }
    }
    
}
```

?> Do not forget to include these header files in your Bridging Header for swift

```
#import <NexPlayerSDK/NXTimedMetaKeys.h>
#import <NexPlayerSDK/NxTimedMetaExtraTag.h>
```

## Properties

### NXPropertyTimedID3MetaKey (521)

Allows custom ID3 tags added to timed metadata in content to be recognized and handled by NexPlayer.

When customized ID3 tags with additional information have been added to the timed metadata in content, this property can be used to help NexPlayer recognize and pass those ID3 tags and the extra information they contain to an application.

This property must be set before NexPlayer.open is called.

**Type:** String

**Values:** a list of the customized ID3 tag names separated by semicolons (;)

**Default:** nothing

**See Also**

- NexID3TagText.getExtraDataID
- NexID3TagInformation.getArrExtraData
- NexID3TagInformation.setArrExtraData

### NXPropertyEnableID3TTML (522)

Sets whether or not to display TTML text tracks in ID3 tags automatically when they are included in content.

In the case, when both CEA closed captions and TTML text tracks in ID3 tags are included in content, this property can be used to set whether to display the TTML text tracks in ID3 tags or the closed captions automatically.

By default, this property is set to 0 to disable TTML text tracks in ID3 tags automatically if they exist in content (as was the behavior of NexPlayer previously). If for some reason it would be preferable that TTML captions in ID3 tag be displayed instead of the CEA closed captions text tracks, this property should be set to 1 using setProperty. This property should only be called once, immediately after calling init but before calling open.

```swift
nxplayer.setProperty(NXPropertyEnableID3TTML, toValue: 1)
```

This property should only be called once, after calling init but before calling open.

!> Do not use with `PARTIAL_PREFETCH` property. 

**Values:**

- 0 : TTML text tracks in ID3 tags ignored; CEA closed captions enabled
- 1 : TTML text tracks in ID3 tags enabled; CEA closed captions ignored

**Default:** 0

## API Reference

### NXPlayer.setCustomID3Tags

```swift
nxplayer.setCustomID3Tags(["CustomTag1", "CustomTag2"])
```

Allows custom ID3 tags added to timed metadata in content to be recognized and handled by NexPlayer.

When customized ID3 tags with additional information have been added to the timed metadata in content, this property can be used to help NexPlayer recognize and pass those ID3 tags and the extra information they contain to an application.

**Parameters**
 
| Name | Description  |
|------|-------------------------|
| tags   | Custom ID3 tags as an array. |
