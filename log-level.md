# Log Level

Event logs recod events taking place in execution of NexPlayer in order to provide an audit trail that can be used to understand the player life cycle and to diagnose problems that may appear. They are essential to understand each step NexPlayer makes while opening, playing or closing any content.

You can select different levels for the logs:

- NXLoglevelError (-3): Enables error level log only
- NXLogLevelWarning (-2): Enables warning log level and below
- NXLogLevelDisabled (-1): Log disabled
- NXLogLevelInformation (0): Enables information level log and below (default)
- NXLogLevelDebug (1): Enables debug level log and below
- NXLogLevelVerbose (2): Enables verbose log level and below
- NXLogLevelAboveVerbose (3): Enables above verbose log level and below. This will have more logs than the verbose level.
- NXLogLevelExtraVerbose (4): Enables extra verbose level log and below. This will have more logs than the above verbose level.


NexPlayer provides an static method to control the amount of diagnostic information output. 

```swift
NXPlayer.setLogLevel(NXLogLevel)
```
This method should be set before creating the NXPlayer instance. Log data is output as part of initialization, so if this is set after creating the instance, some log data may be lost.

In case you have different instances of players in you application and you want to set the log level of them independently you can call the same method in the player instance.

```swift
NXPlayer.setLogLevel(.aboveVerbose)

let player1: NXPlayer = NXPlayer()
let player2: NXPlayer = NXPlayer()
player1.setLogLevel(.disabled)
player2.setLogLevel(.extraVerbose)
```

-
WHAT TO DO ABOUT THIS? I think we don´t need to use it anymore.

player.setProperty(NXPropertyLogLevel, value: NXPropertyLogLevel_RTP as NSObject)

```objC
/**
 * \ingroup prop
 * \brief Sets the log level.
 *
 * <b>Values:</b>
 * - NXPropertyLogLevel_Debug
 * - NXPropertyLogLevel_RTP	
 * - NXPropertyLogLevel_RTCP
 * - NXPropertyLogLevel_Frame
 * 
 */
	NXPropertyLogLevel							= 35,
```