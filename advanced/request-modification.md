# HTTP Request Modification

In order to modify an HTTP Request with NexPlayer:

1. Add the following code:

```swift
player.setProperty(NXPropertyEnableModifyHTTPRequest, value: true as NSObject)
```

After **init** but before calling **open** in order to set the property NXPropertyEnableModifyHTTPRequest to enabled.

2. The following override code must also be included for NXPlayerDelegate:

```swift
extension NexPlayerView: NXPlayerDelegate {

    ...

    func nexPlayer(_ nxplayer: NXPlayer!, onModifyHttpRequest requestString: String!) -> String! {
        var strData: String = ""
        print("HTTP\\_REQUEST - requestLength: \(requestString.size()).")
        strData = requestString
        print("HTTP\\_REQUEST DATA: \(strData)")
        print("HTTP\\_REQUEST DATA SET END!!! strData.length: \(strData.size()).")
        return strData
    }
}
```

See *onModifyHttpRequest* for more information.