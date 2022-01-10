# NexPlayer Logs

NexPlayer provides different log levels, which makes it easier to understand what is happening in the background, both in the application and native layers. They are essential to understand each step NexPlayer makes while opening, playing or closing any content.


```swift
let player: NXPlayer = NXPlayer()
player.setLogLevel(.extraVerbose)
```

This method should be set before creating the NXPlayer instance. Log data is output as part of initialization, so if this is set after creating the instance, some log data may be lost.

You can select different levels for the logs:

- NXLoglevelError (-3): Enables error level log only
- NXLogLevelWarning (-2): Enables warning log level and below
- NXLogLevelDisabled (-1): Log disabled
- NXLogLevelInformation (0): Enables information level log and below (default)
- NXLogLevelDebug (1): Enables debug level log and below
- NXLogLevelVerbose (2): Enables verbose log level and below
- NXLogLevelAboveVerbose (3): Enables above verbose log level and below. This will have more logs than the verbose level.
- NXLogLevelExtraVerbose (4): Enables extra verbose level log and below. This will have more logs than the above verbose level.

You can also enable futher logging by enabling the logs for NexPlayer protocol module:

```swift
player.setProperty(NXPropertyLogLevel, value: 11 as NSObject)
```

All the logs will be printed in the XCode console while debugging. You can also access the logs using the MacoS Console app if you are not using XCode. You should select the connected device from the left side if you are using the Console application.
