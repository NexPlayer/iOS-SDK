# NexPlayer Error Codes

#### `NXErrorHasNoEffect` 

Method has no effect. The same command has been called already in the same state or the command is invalid.

#### `NXErrorInvalidParameter` 

Parameter is invalid. This error will be called if the UI has wrong parameters such as NULL.

#### `NXErrorInvalidState` 

State is invalid. The command is invalid at the current state. E.g. pause() is called when the current state is stopped

#### `NXErrorInvalidCodec`

File contains invalid syntax. The content file contains invalid syntax. It should be checked whether or not the content is a normal DRM file.

#### `NXErrorNotSupportAudioCodec` 

The audio codec is not supported. NexPlayer does not support the audio codec of the content. E.g. The content is not yet supported by NexPlayer or a customer could not include codecs of NexPlayer SDK due to licensing issues.

#### `NXErrorNotSupportVideoCodec` 

The video codec is not supported. NexPlayer does not support the video codec of the content. E.g. The content is not yet supported by NexPlayer or the customer did not include codecs of NexPlayer SDK due to licensing issues.

#### `NXErrorNotSupportVideoResolution` 

The video resolution is not supported. The resolution of the content is too high to play back. E.g. The device has a resolution limit of 1080P but the content is 4K.

#### `NXErrorNotSupportMedia` 

The content format is not supported or is not playable A/V track. The format of the content is not supported. The content has unavailable protocol(HLS,DASH, etc) or no playable A/V track which has audio or video codecs that are not supported.

#### `NXErrorCodec` 

The codec reported an error. Audio or video decoding error. E.g.  NexPlayer get a failure during parsing the content for playback or during decoding the audio or video bitstreams.

#### `NXErrorUnknown` 

Unknown error. This error is a kind of internal error such as "system failure". E.g. NexPlayer returns this when memory allocation is failed for unknown reasons. It's mostly an error that the user can not handle. Please contact a NexPlayer developer for more details.

#### `NXErrorNotSupportToSeek` 

The media source does not support seeking. The only Iframe content(Content is composed of I, B, and P frames), chunked mode based PD content, or live content with an wide interval between each Iframe cannot be seeked.

#### `NXErrorNotSupportPVXFile` 

The text is not supported. The content has an unsupported text type. 

#### `NXErrorProtocolNetRequestTimeout` 

The media source open timed out. There is no response from the server within the set time of SOURCE_OPEN_TIMEOUT property while calling open(). The default value of the SOURCE_OPEN_TIMEOUT property is 300 seconds.

#### `NXErrorDataInactivityTimeout` 

The response timed out. There is no response from the server within the set time of DATA_INACTIVITY_TIMEOUT property. The default value of the DATA_INACTIVITY_TIMEOUT property is 60 seconds.

#### `NXErrorNetworkProtocol` 

Network or protocol error. Network related error such as socket errors. Ex. socket open fail, connect fail, bind fail etc.

#### `NXErrorMediaNotFound` 

The content media was not found. The content media was not found on the server. Ex. 403 forbidden, 404 not found etc.      

#### `NXErrorDrmDecryptFailed` 

The content DRM decrypt fail. The default error of content DRM Decrypt Fail

#### `NXErrorDrmInitFailed` 

The content DRM initialization fail. Ex. Invalid License URL.

#### `NXErrorProtocolInvalidURL` 

The URL is invalid.

#### `NXErrorProtocolInvalidResponse` 

The syntax of the response is invalid. Ex. Mandatory header is missed in the response.

#### `NXErrorProtocolContentInfoParsingFail` 

ContentInfo parse fail. (SDP, ASF Header, Playlist...)

#### `NXErrorProtocolNetConnectionClosed` 

Socket connection closed.

#### `NXErrorProtocolNetRequestTimeout` 

Response is not arrived until timeout.

#### `NXErrorHTTPStatusCode` 

The HTTP response data recevied from the Server is error. It's not 200 in HTTP response. Ex. 500, 503 etc

#### `NXErrorProtocolDisabledMedia` 

No track to play due to a bitrate/resolution limit. E.g. The MIN_BW property is set to 2 Mbps and the playlist of playing contain has only 500 Kbps and 1 Mbps tracks.

#### `NXErrorProtocolNetRecvFail` 

Failed to download the key file to decrypt the file that has been encrypted with AES.
		
#### `NXErrorProtocolInvalidResponse` 

The user called a part of HTTP Downloader before creating or initializing.

#### `NXErrorProtocolContentInfoParsingFail` 

A parameter from the UI is null or an incorrect value when HTTP downloader sends the message.

#### `NXErrorProtocolNoProtocol` 

Http downloader failed to allocate or free memory.
            
#### `NXErrorProtocolNoMedia` 

System related error.            

#### `NXErrorProtocolNetOpenFail` 

Http downloader writing failure.

#### `NXErrorProtocolNetConnectFail` 

The user attempted to call the same method many times. All duplicates (except the first one) will be regarded as an error.

#### `NXErrorProtocolNetRecvFail` 

Http downloader received an invalid response from the server.

#### `NXErrorNotSupportFeature` 

NexPlayer detected an unsupported feature(i.e. recording or timeshift) or called a specific feature.

#### `NXErrorInvalidLicense` 

NexPlayer initialization failed by License File.

#### `NXErrorInvalidSDK` 

NexPlayer initialization failed by the invalid SDK. Error while creating or initializing NexPlayer.

#### `NXErrorNotActivatedAppID` 

Error while creating or initializing NexPlayer. The current app id is not activated

#### `NXErrorTimeLocked` 

SDK has expired

