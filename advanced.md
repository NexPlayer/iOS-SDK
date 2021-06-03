# Advanced Usage

### Informative Event Keys

#### NSString∗ kNexInformativeEventResult = @"@"Result" [static]

Detailed parameter key for NexInformativeEventDownloadFinished events. The value type is NSNumber, which
contains a NXError.

#### NSString∗ kNexInformativeEventURL = @"@"URL" [static]

Detailed parameter key for `NexInformativeEventDownloadBegan` and `NexInformativeEventDownloadFinished` events. The value type is NSString.

### Callback Types

**Modules**

- **C-level API Functions** Callback function for descrambling HLS-TS encrypted content (HTTP Live Streaming content encrypted at the segment level).

**Typedefs**

- `typedef unsigned int(∗NEXPLAYERGetPlaylistInfoCallbackFunc) (char ∗pUrl, char ∗pPlaylist, unsigned uiPlaylistSize, void ∗pUserData)` Callback function for receiving updates to the HLS playlist data.
 
- `typedef int(∗NEXPLAYERMPDDescrambleCallbackFunc)(char ∗pMpdUrl, unsigned int dwMpdUrlLen, char ∗pMpd, unsigned int dwMpdLen, unsigned int ∗pdwNewMpdLen, void ∗pUserData)` Callback function to handle content with an encrypted playlist or manifest.
 
- `typedef int(∗NEXPLAYERHLSAES128DescrambleCallbackFunc)(unsigned char ∗pInBuf, unsigned int dwInBufSize, unsigned char ∗pOutBuf, unsigned int ∗pdwOutBufSize, char ∗pSegmentUrl, char ∗pMpdUrl, char ∗pKeyAttr, unsigned int dwSegmentSeq, unsigned char ∗pKey, unsigned int dwKeySize, void ∗pUserData)
` Callback function for receiving AES128 encrypted HLS content.
       
- `typedef int(∗NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc) (unsigned char ∗pInBuf, unsigned int dwInBufSize, unsigned char ∗pOutBuf, unsigned int ∗pdwOutBufSize, char ∗pSegmentUrl, long long qByteRangeOffset, long long qByteRangeLength, char ∗pMpdUrl, char ∗pKeyAttr, unsigned int dwSegmentSeq, unsigned char ∗pKey, unsigned int dwKeySize, void ∗pUserData)` Callback function for receiving AES128 encrypted HLS content with byte range.
 
- `typedef int(∗NEXPLAYERHLSIsSupportKeyCallbackFunc) (char ∗pMpdUrl, char ∗pKeyAttr, void ∗pUserData)` Callback function that verifies whether or not a key attribute is supported by the DRM module.
 
- `typedef int(∗NEXPLAYERPiffPlayReadyDescrambleCallbackFunc)(unsigned char∗pInputBuffer, unsigned int dwInputBufferSize, unsigned char∗pOutputBuffer, unsigned int ∗pdwOutputBufferSize, unsigned char ∗pSampleEncBox, unsigned int dwSampleEncBoxLen, unsigned int dwSampleIDX, unsigned int dwTrackID, void ∗pUserData)` Callback function for descrambling PlayReady encrypted content in a PIFF file.
 
- `typedef int(∗NEXPLAYERDashDrmSessionOpenCallbackFunc )(long long ∗pSH, char ∗pDrmInfo, unsigned int dwDrmInfoSize, void ∗pUserData)` Callback function to open DASH DRM Session.
 
- `typedef int(∗NEXPLAYERDashDrmSessionCloseCallbackFunc)(long long hSH, void ∗pUserData)` Callback function to close DASH DRM Session. This function will only be called when the parameter `pSH` of `NEXPLAYERDashDrmSessionOpenCallbackFunc` is not -1.

- `typedef int(∗NEXPLAYERDashDrmSessionSetCencBoxCallbackFunc ) (long long hSH, char ∗pBoxName, char ∗pBoxData, unsigned int dwBoxDataSize, void∗pUserData)` Callback function to transfer CencBox.

- `typedef int(∗NEXPLAYERDashDrmSessionDecryptIsobmffFrameCallbackFunc ) (long long hSH, char ∗pIV, unsigned int dwIVLen, char ∗pEncFrame, unsigned int dwEncFrameLen, char ∗pDecFrame, unsigned int ∗pdwDecFrameLen, void ∗pUserData)` Callback function to decrypt an encrypted frame.
 
- `typedef int(∗NEXPLAYERGetPDBlockCallbackFunc ) (char∗pBlockBuf, long long ulOffset, int uiBlockSize, void ∗pUserData)`
 Callback function for receiving blocks of Progressive Download (PD) content.

- `typedef int(∗NEXPLAYERPDEnvelopHeaderParsingCallbackFunc ) (char∗pData, long long qOffset, int iDataSize, unsigned int ∗puContentOffset, void ∗pUserData)` Callback function for parsing headers of Progressive Download (PD) content.

- `typedef NEXFileHandle(∗NEXPLAYERRemoteFile_OpenFt ) (char ∗pFileName, NEXFileMode iMode, void ∗pUserData)` Remote File I/O callback for opening a file.

- `typedef int(∗NEXPLAYERRemoteFile_CloseFt ) (NEXFileHandle hFile, void ∗pUserData)` Remote File I/O callback for closing a file.

- `typedef ssize_t(∗NEXPLAYERRemoteFile_ReadFt ) (NEXFileHandle hFile, void ∗pBuf, unsigned int uiSize, size_t uiCount, void ∗pUserData)` Remote File I/O callback for reading a file.

- `typedef int(∗NEXPLAYERRemoteFile_SeekFt ) (NEXFileHandle hFile, int iOffset, NEXFileSeekOrigin iOrigin, void ∗pUserData)` Remote File I/O callback for seeking a file.

- `typedef long long(∗NEXPLAYERRemoteFile_Seek64Ft ) (NEXFileHandle hFile, long long iOffset, NEXFileSeekOrigin iOrigin, void ∗pUserData)` Remote File I/O callback for seeking a file.

- `typedef ssize_t(∗NEXPLAYERRemoteFile_WriteFt ) (NEXFileHandle hFile, char ∗pBuf, size_t dwSize, void ∗pUserData)` Remote File I/O callback for writing to a file.

- `typedef long long(∗NEXPLAYERRemoteFile_SizeFt ) (NEXFileHandle hFile, void ∗pUserData)` Remote File I/O callback for getting the size of a file.

### typedef Documentation

#### typedef int(*NEXPLAYERDashDrmSessionCloseCallbackFunc) (long long hSH, void *pUserData)

Callback function to close DASH DRM Session. This function will only be called when the parameter `pSH` of `NEXPLAYERDashDrmSessionOpenCallbackFunc` is not -1.

**Parameters**

| Name  | Description  | 
|---|---|
|hSH | DRM session handle |
|pUserData      |   The user data passed when the callback was registered. |

#### typedef int(∗NEXPLAYERDashDrmSessionCloseCallbackFunc) (long long hSH, void ∗pUserData)

Callback function to decrypt an encrypted frame.

**Parameters**

| Name  | Description  | 
|---|---|
| hSH | DRM Session handle.|
| pIV | Initial vector.|
| dwIVLen | Byte length of initial vector.|
| pEncFrame | Encrypted frame.|
| dwEncFrameLen | Byte length of encrypted frame.|
| pDecFrame | Decrypted frame. |
| pdwDecFrameLen| Byte length of decrypted frame.
| pUserData | The user data passed when the callback was registered. |

#### typedef int(∗NEXPLAYERDashDrmSessionOpenCallbackFunc) (long long ∗pSH, char ∗pDrmInfo, unsigned int dwDrmInfoSize, void ∗pUserData)
Callback function to open DASH DRM Session.

**Parameters**

| Name  | Description  | 
|---|---|
|pSH| DRM session handle. The initial value is -1 which indicates that DRM Session is not opened, therefore `NEXPLAYERDashDrmSessionCloseCallbackFunc` will not be called.|
|pDrmInfo| Contains all the ContentProtection tags in MPD.|
|dwDrmInfoSize |The byte length of pDrmInfo.|
|pUserData |The user data passed when the callback was registered.|

#### typedef int(∗NEXPLAYERDashDrmSessionSetCencBoxCallbackFunc) (long long hSH, char ∗pBoxName, char ∗pBoxData, unsigned int dwBoxDataSize, void ∗pUserData)

Callback function to transfer CencBox.

**Parameters**

| Name  | Description  | 
|---|---|
|hSH |DRM session handle.|
|pBoxName| The box name as a NULL-terminated string :seig, tencorpssh.|
|pBoxData |The payload information of the box.|
|dwBoxDataSize| Byte length of pBoxData.|
|pUserData| The user data passed when the callback was registered.|

#### typedef int(∗NEXPLAYERGetPDBlockCallbackFunc) (char ∗pBlockBuf, long long ulOffset, int uiBlockSize, void ∗pUserData)

Callback function for receiving blocks of Progressive Download (PD) content.

This is called each time NexPlayer receives a block of Progressive Download (PD) content. NexPlayer sends
the received block and the block’s size with this callback.

**Parameters**

| Name  | Description  | 
|---|---|
|pBlockBuf | The array containing the data from the PD block. |
|ulOffset | The offset of the block’s starting position from the beginning of the content.|
|uiBlockSize | The size of the PD block received.|
|pUserData | The user data passed when the callback was registered.|

**Returns**

Zero, but has no meaning and should be ignored.

#### typedef unsigned int(∗NEXPLAYERGetPlaylistInfoCallbackFunc) (char ∗pUrl, char ∗pPlaylist, unsigned int uiPlaylistSize, void ∗pUserData)

Callback function for receiving updates to the HLS playlist data.

This is called every time that the player receives an HLS playlist. This can happen in several cases:

- When the initial (master) playlist is received
- When the player switches to a new track and loads the playlist for that track
- While playing live content, if the server updates the playlist

Whenever `NEXPLAYERHLSTSDescrambleCallbackFunc` is called with a TS or audio file to be descrambled, that
TS or audio file will always be from the playlist most recently received by this callback.

**Parameters**

| Name  | Description  | 
|---|---|
| pUrl| The URL of the playlist.|
| pPlaylist| The contents of the playlist, as text.|
| uiPlaylistSize| The size of pPlayList, in bytes, not including any terminating *NULL*.|
| pUserData |The user data passed when the callback was originally registered.|

**Returns**

The callback should return zero for success and -1 in case of an error.

#### typedef int(∗NEXPLAYERHLSAES128DescrambleCallbackFunc) (unsigned char ∗pInBuf, unsigned int dwInBufSize, unsigned char ∗pOutBuf, unsigned int ∗pdwOutBufSize, char ∗pSegmentUrl, char ∗pMpdUrl, char ∗pKeyAttr, unsigned int dwSegmentSeq, unsigned char ∗pKey, unsigned int dwKeySize, void ∗pUserData)

Callback function for receiving AES128 encrypted HLS content.

When registered, this callback function is called every time AES128 encrypted HLS content is received.

**Parameters**

| Name  | Description  | 
|---|---|
|pInBuf| A pointer to the input buffer.|
|dwInBufSize |The size of the input buffer, inbytes.|
|pOutBuf| A pointer to the output buffer where decrypted content is stored.|
|pdwOutBufSize| A pointer to the size of the decrypted segment, in bytes.|
|pSegmentUrl| A pointer to the URL of the segment of content.|
|pMpdUrl |A pointer to the original URL of the content playlist.|
|pKeyAttr| A pointer to the decryption Key information.|
|dwSegmentSeq| The sequence number of the TS segment file.|
|pKey| A pointer to the decryption Key. This parameter is only meaningful when dwKeySize is greater than 0 (i.e. a key has been downloaded).|
|dwKeySize |The size of the decryption Key. This parameter will be zero if no key has been downloaded.|
|pUserData| The user data passed when the callback was registered.|

**Returns**

The callback should return zero for success and -1 in case of an error.

#### typedef int(∗NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc)(unsigned char ∗pInBuf, unsigned int dwInBufSize, unsigned char ∗pOutBuf, unsigned int ∗pdwOutBufSize, char ∗pSegmentUrl, long long qByteRangeOffset, long long qByteRangeLength, char ∗pMpdUrl, char ∗pKeyAttr, unsigned int dwSegmentSeq, unsigned char ∗pKey, unsigned int dwKeySize, void ∗pUserData)

Callback function for receiving AES128 encrypted HLS content with byte range.

When registered, this callback function is called every time AES128 encrypted HLS content is received.

**Parameters**

|Name  | Description  | 
|---|---|
|pInBuf| A pointer to the input buffer.|
|dwInBufSize |The size of the input buffer, in bytes.|
|pOutBuf|A pointer to the output buffer where decrypted content is stored.|
|pdwOutBufSize| A pointer to the size of the decrypted segment, in bytes.|
|pSegmentUrl| A pointer to the URL of the content segment.|
|qByteRangeOffset|The offset of the byte range.|
|qByteRangeLength|The length of the byte range.|
|pMpdUrl| A pointer to the original URL of the content playlist.|
|pKeyAttr| A pointer to the decryption Key information.|
|dwSegmentSeq| The sequence number of the TS segment file.|
|pKey| A pointer to the decryption Key. This parameter is only meaningful when dwKeySize is greater than 0 (i.e. a key has been downloaded).|
|dwKeySize| The size of the decryption Key. This parameter will be zero if no key has been downloaded.|
|pUserData| The passed user data when the callback was registered.|

**Returns**

The callback should return zero for success and -1 in case of an error.

#### typedef int(∗NEXPLAYERHLSIsSupportKeyCallbackFunc) (char ∗pMpdUrl, char ∗pKeyAttr, void ∗pUserData)

Callback function that verifies whether or not a key attribute is supported by the DRM module.

This callback is called when NexPlayer meets #EXT-X-KEY tags while NexPlayer is parsing playlists. If the
callback returns a non-zero value, NexPlayer will not call DRM functions even if that function is registered.

**Parameters**

|Name  | Description  | 
|---|---|
|pMpdUrl| The URL of the playlist.|
|pKeyAttr| Key information of the segment that has been received.|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

If the DRM is supporting that key attribute, then it should return zero(0). Then NexPlayer will call DRM callbacks depending on the encryption method. If the DRM does not support the key, then it should return a non-zero value. In this case, NexPlayer will not call the DRM callbacks and it will decrypt using its internal decryption function.

#### typedef int(∗NEXPLAYERMPDDescrambleCallbackFunc) (char ∗pMpdUrl, unsigned int dwMpdUrlLen, char ∗pMpd, unsigned int dwMpdLen, unsigned int ∗pdwNewMpdLen, void ∗pUserData)

Callback function to handle content with an encrypted playlist or manifest.

NexPlayer calls this function whenever it receives the manifest or top level of a playlist so that the playlist or manifest can be decrypted (in the case it happens to be encrypted).

**Parameters**

|Name  | Description  | 
|---|---|
|pMpdUrl| The original URL of the top-level MPD. In the case of redirection, this will be the URL before redirection.|
|dwMpdUrlLen| The length of the manifest or playlist URL, in bytes.|
|pMpd| The top level playlist or manifest.|
|dwMpdLen| The size of the manifest or playlist, in bytes.|
|pdwNewMpdLen| The size of the decrypted manifest or playlist.|
|pUserData |The user data passed when the callback was registered.|

**Returns**

The callback should return zero for success and -1 in case of an error.

#### typedef int(∗NEXPLAYERPDEnvelopHeaderParsingCallbackFunc) (char ∗pData, long long qOffset, int iDataSize, unsigned int ∗puContentOffset, void ∗pUserData)

Callback function for parsing headers of Progressive Download (PD) content.

This is called when NexPlayer receives a header of Progressive Download (PD) content. NexPlayer sends the received header and its size with this callback.

**Parameters**

|Name | Description  | 
|---|---|
|pData| The array containing the data of the PD header.|
|qOffset| The offset of the header’s starting position.|
|iDataSize| The size of the PD header received.|
|puContentOffset| The offset of content.|
|pUserData| The user data passed when the callback was registered.|

**Returns**

- Success : 0
- Need More Data : -1
- DRM error code : <-1
- Remark : When it is not DRM content, return 0 with puContentOffset=0;

#### typedef int(∗NEXPLAYERPiffPlayReadyDescrambleCallbackFunc) (unsigned char ∗pInputBuffer, unsigned int dwInputBufferSize, unsigned char ∗pOutputBuffer, unsigned int ∗pdwOutputBufferSize, unsigned char ∗pSampleEncBox, unsigned int dwSampleEncBoxLen, unsigned int dwSampleIDX, unsigned int dwTrackID, void ∗pUserData)

Callback function for descrambling PlayReady encrypted content in a PIFF file.

**Parameters**

|Name  | Description  | 
|---|---|
| pInputBuffer | The encrypted data to be descrambled.|
| dwInputBufferSize | The size of the encrypted data, in bytes.|
| pOutputBuffer | The location at which to place the descrambled output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
| pdwOutputBufferSize|The size of the decrypted data. The callback must set this value. This may be equal to or smaller than dwInputBufferSize, but not larger.
| pSampleEncBox| The SampleEncryptionBox, as detailed in the [MS-SSTR] Smooth Streaming Protocol Specification. |
|dwSampleEncBoxLen| The length, inbytes, of the data atpSampleEncBox.|
| dwSampleIDX| The index of the media object (frame or sample, depending on media format) being descrambled.|
|dwTrackID| Media Track ID, from TfhdBox, as defined in the [MS-SSTR] Smooth Streaming Protocol Specification.|
| pUserData| The user data passed when the callback was originally registered.|

**Returns**

The callback should return zero if the data was successfully descrambled. In the case of an error, it should return -1.

#### typedef int(∗NEXPLAYERRemoteFile_CloseFt) (NEXFileHandle hFile, void ∗pUserData)

Remote File I/O callback for closing a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace the system calls normally used for opening and accessing files.

**Parameters**

|Name  | Description  | 
|---|---|
|hFile| File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of file to be closed.|
|pUserData| The user data passed when the callback was originally registered.|


**Returns**

0 if successful, or -1 if an error occurred.

#### typedef NEXFileHandle(∗NEXPLAYERRemoteFile_OpenFt) (char ∗pFileName, NEXFileMode iMode, void ∗pUserData)

Remote File I/O callback for opening a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace the system calls normally used for opening and accessing files.

**Parameters**

|Name  | Description  | 
|---|---|
| pFileName| Path and filename of the file to be opened. This is the path that the application originally passed to NexPlayer, so the application may treat it in any way appropriate in the callback.|
|iMode |Specifies how the file is to be opened; see NEXFileMode for details.|
 pUserData| The user data passed when the callback was originally registered.|

**Returns**

The handle of the opened file, or -1 if an error occurred.

#### ssize_t(∗NEXPLAYERRemoteFile_ReadFt) (NEXFileHandle hFile, void ∗pBuf, unsigned int uiSize, size_t uiCount, void ∗pUserData)

Remote File I/O callback for reading a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace
the system calls normally used for opening and accessing files.

The actual number of bytes to read is (uiSize∗uiCount).

**Parameters**

| Name  | Description  | 
|---|---|
| hFile| File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of file to read from.|
| pBuf| Buffer to receive the data.|
| uiSize| Record size, in bytes.|
| uiCount| Number of records to read.|
| pUserData| The user data passed when the callback was originally registered.|

**Returns**

- >0: The number ofbytesactually read
- 0: Reached the end of the file.
- -1: An error occurred.

#### typedef long long(∗NEXPLAYERRemoteFile_Seek64Ft) (NEXFileHandle hFile, long long iOffset, NEXFileSeekOrigin iOrigin, void ∗pUserData)

Remote File I/O callback for seeking a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace
the system calls normally used for opening and accessing files.

This sets the location in the file at which the next read operation will occur.

**Note**

> This supports seek offsets of up to 64-bits. Implement this callback if you wish to support files over 2GB in size.

**Parameters**

| Name  | Description  | 
|---|---|
|hFile| File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of file to be seeked.|
|iOffset| Seek destination, as an offset in bytes from iOrigin|
|iOrigin| Origin for iOffset. See NEXFileSeekOrigin for possible values.|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

New offset from beginning of file, or -1 if an error occurred.

#### typedef int(∗NEXPLAYERRemoteFile_SeekFt) (NEXFileHandle hFile, int iOffset, NEXFileSeekOrigin iOrigin, void ∗pUserData)

Remote File I/O callback for seeking a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace
the system calls normally used for opening and accessing files.

This sets the location in the file at which the next read operation will occur.



>**Note**  This supports seek offsets of up to 32-bits. For large offsets, NEXPLAYERRemoteFile_Seek64Ft will be called instead. If the 64-bit callback is not registered, file with sizes over 2GB will not be supported.

**Parameters**

| Name  | Description  | 
|---|---|
|hFile| File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of file to be seeked.|
|iOffset| Seek destination, as an offset in bytes from iOrigin|
|iOrigin |Origin for iOff set. See NEXFileSeekOrigin for possible values.|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

New offset from beginning of file, or -1 if an error occurred.

#### typedef long long(∗NEXPLAYERRemoteFile_SizeFt) (NEXFileHandle hFile, void ∗pUserData)

Remote File I/O callback for getting the size of a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace
the system calls normally used for opening and accessing files.

This callback should return the size of the file without modifying the position to which the file has been seeked (if
the seek location must be moved to determine the size, this function should move it back afterwards).

**Parameters**

| Name  | Description  | 
|---|---|
|hFile | File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of the file for which the size should be retrieved.|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

```
The actual number of bytes written, or -1 if an error occurred.
```

#### typedef ssize_t(∗NEXPLAYERRemoteFile_WriteFt) (NEXFileHandle hFile, char ∗pBuf, size_t dwSize, void ∗pUserData)

Remote File I/O callback for writing to a file.

This is one of several callback functions that can be registered using the Remote File I/O Interface in order to replace the system calls normally used for opening and accessing files.

**Parameters**

| Name  | Description  | 
|---|---|
|hFile| File handle (as returned by NEXPLAYERRemoteFile_OpenFt) of file to be written to.
|pBuf |The data to write to file|
|dwSize| The number of bytes to write to file|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

The actual number of bytes written, or -1 if an error occurred.

### C-level API Functions

Callback function for descrambling HLS-TS encrypted content (HTTP Live Streaming content encrypted at the segment level). This callback is called every time an HLS segment is received. The segment may be either a TS file or an audio file. The player does not attempt to detect whether or not a segment is encrypted, but rather passes all segments directly to the callback, if one is registered.

**Parameters**

| Name  | Description  | 
|---|---|
|pInputBuffer| The segment (TS file or audio file) that has been received.|
|uiInputBufferSize |The size of the data at pInputBuffer, in bytes.|
|pOutputBuffer| The location at which to place the descrambled output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
|puiOutputBufferSize| The size of the decrypted data. The callback must set this value. This may be equal to or smaller than uiInputBufferSize, but not larger.|
|pMediaFileURL| The URL of the segment media file (TS file or audio file).|
|pPlaylistURL| The URL of the immediate parent playlist (the playlist directly referecing the media file).|
|pUserData| The user data passed when the callback was originally registered.|

**Returns**

The callback should return zero if the data was successfully descrambled. In the case of an error, it should
return -1.

#### void NEXPLAYEREngine_registerGetPDBlockCallBackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERGetPDBlockCallbackFunc pGetPDBlockCallbackFunc, void ∗ pUserData )

Registers a callback function to receive a pointer for Progressive Download (PD) block and block’s size. PD data is decrypted using this information.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pGetPDBlockCallbackFunc|Callback function to register.|
|pUserData| Additional data to pass to callback function when it is called.|

**See Also**

- NEXPLAYERGetPDBlockCallbackFunc

#### void NEXPLAYEREngine_registerGetPlaylistInfoFuncCallBackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERGetPlaylistInfoCallbackFunc pGetPlaylistInfoCallbackFunc, void ∗ pUserData )

Registers a callback function to receive HLS playlist content every time a new HLS playlist is received.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pGetPlaylistInfoCallbackFunc|Callback function to register|
|pUserData| Additional data to pass to callback function when it is called|

**See Also**

- NEXPLAYERGetPlaylistInfoCallbackFunc

#### void NEXPLAYEREngine_registerHLSAES128DescrambleCallbackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERHLSAES128DescrambleCallbackFunc pDescrambleCallbackFunc, void ∗ pUserData )

Registers a callback function to handle AES128 encrypted HLS content.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pDescrambleCallbackFunc|Callback function to register.|
|pUserData| Additional data to pass to callback function when it is called.|

**See Also**

- NEXPLAYERHLSAES128DescrambleCallbackFunc

#### void NEXPLAYEREngine_registerHLSAES128DescrambleWithByteRangeCallbackFunc (NEXPLAYERENGINE_handlehEngine, NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc pDescrambleCallbackFunc, void ∗ pUserData )

Registers a callback function to handle AES128 encrypted HLS content with ByteRange.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pDescrambleCallbackFunc|Callback function to register.|
|pUserData| Additional data to pass to callback function when it is called.|

**See Also**

- NEXPLAYERHLSAES128DescrambleWithByteRangeCallbackFunc

#### void NEXPLAYEREngine_registerHLSIsSupportKeyCallbackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERHLSIsSupportKeyCallbackFunc pHLSIsSupportKeyCallbackFunc, void ∗ pUserData )
Registers a callback function that verifies whether or not a key attribute is supported by the DRM module.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pHLSIsSupportKey|Callback function to register.|
|pUserData| Additional data to pass to the callback function when it is called.|

#### void NEXPLAYEREngine_registerHLSTSDescrambleCallBackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERHLSTSDescrambleCallbackFunc pDescrambleCallbackFunc, void ∗ pUserData )

Registers an HLS/TS descrambling callback function.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pDescrambleCallbackFunc|Callback function to register|
|pUserData| Additional data to pass to the callback function when it is called.|

**See Also**

- NEXPLAYERHLSTSDescrambleCallbackFunc

#### void NEXPLAYEREngine_registerMPDDescrambleCallbackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERMPDDescrambleCallbackFunc pDescrambleCallbackFunc, void ∗ pUserData )

Registers a callback function to handle encrypted manifests or playlists in content.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pDescrambleCallbackFunc|Callback function to register.|
|pUserData| Additional data to pass to callback function when it is called.|

**See Also**

- NEXPLAYERMPDDescrambleCallbackFunc

#### void NEXPLAYEREngine_registerPDEnvelopHeaderParsingCallBackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERPDEnvelopHeaderParsingCallbackFunc pPDEnvelopHeaderParsingCallbackFunc, void ∗ pUserData )

Registers a callback function to receive a pointer of Progressive Download (PD) Header and header’s size. Header data is parsed using this information.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pPDEnvelopHeaderParsingCallbackFunc|Callback function to register.|
|pUserData| Additional data to pass to the callback function when it is called.|

**See Also**

- NEXPLAYERPDEnvelopHeaderParsingCallbackFunc


#### void NEXPLAYEREngine_registerPIFFPlayReadyDescrambleCallBackFunc (NEXPLAYERENGINE_handle hEngine, NEXPLAYERPiffPlayReadyDescrambleCallbackFunc pDescrambleCallbackFunc, void ∗ pUserData )

Registers a PIFF PlayReady descrambling callback function.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pDescrambleCallbackFunc|Callback function to register|
|pUserData| Additional data to pass to callback function when it is called.|

**See Also**

- NEXPLAYERPiffPlayReadyDescrambleCallbackFunc

#### void NEXPLAYEREngine_registerRemoteFileIOInterface (NEXPLAYERENGINE_handle hEngine, NEXPLAYERRemoteFileIOInterface ∗ pRemoteFileIOInterface, void ∗ pUserData )

Registers a set of callback functions for Remote File I/O.

See Remote File I/O for more information.

**Parameters**

| Name  | Description  | 
|---|---|
|hEngine| The handle of the NexPlayer engine.|
|pRemoteFileIOInterface|Structure containing pointers to functions to register|
|pUserData| Additional data to pass to callback function when it is called|

**See Also**

- NEXPLAYERRemoteFileIOInterface


## Class Documentation

### NexAudioPostProcessingAdapter Class Reference

This class provides the application a way to adapt an audio post-processor. The audio processor can be implemented by conforming the `NexAudioPostProcessingAdapterDelegate` protocol.

> **Note** The application is responsible for the memory residence of the instance of this class.

#### - (id) initWithNexPlayer: (NXPlayer ∗) player delegate:(id\<NexAudioPostProcessingAdapterDelegate\>) delegate

The designated initializer.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance where the audio post-processor, delegate, will be attached to|
| delegate |The audio post-processor instance in the application.|

#### - (void) setMultiChannelEnabled: (BOOL)enableforCodecType:(NXCodecID) codecType

This method sets whether or not to have more than 2 audio channels (i.e. 5.1 channels), if the decoder of the codec type supports multi-channel output. The value of the enable argument (YES or NO) affects the value of NexAudioPostProcessingParams::inChannels in ’params’ of audioAdapter:shouldPostProcessWithParams:.

| Name  | Description  | 
|---|---|
| enable | Set to YES to enable multi-channel output from the decoder of ’codecType’.|
| codecType |The decoder type to be configured for multi-channel output.|


#### - (NXPlayer *) player [read], [nonatomic], [weak]

The NXPlayer instance passed in to initWithPlayer:delegate.

### NexAudioPostProcessingAdapterDelegate Protocol Reference

Defines the interface for the audio post-processor provided by the application.

#### (NSUInteger) audioAdapter: (NexAudioPostProcessingAdapter ∗) adapter processBuffer:(void ∗) pBuffer length:(NSUInteger) length

Called to request the delegate to perform post-processing, if audioAdapterShouldPostProcess: returned YES.

**Parameters**

| Name  | Description  | 
|---|---|
| adapter | The calling audio processing adapter.|
| pBuffer |The buffer contains samples, which are updated by the output samples after|
| length | The length of pBuffer in bytes.|

**Returns**

The length of output stored in the buffer pointed by pBuffer, in bytes.

#### - (BOOL) audioAdapter: (NexAudioPostProcessingAdapter ∗) adapter shouldPostProcessWithParams:(NexAudioPostProcessingParams) params

Called when NexPlayer; asks the audio post-processor instance that implements this protocol, if it can handle the audio samples described by ’params’.

**Parameters**

| Name  | Description  | 
|---|---|
| adapter | The calling NexAudioPostProcessingAdapter instance.|
| params |Describes the characteristics of audio samples, which are provided by the audioAdapter:processBuffer:length: method.|

###  NexAudioPostProcessingParams Struct Reference

The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio post-processor, which implements the `NexAudioPostProcessingAdapterDelegate` protocol.

**Public Attributes**

- `NXCodecID codecId`
    Decoder type that generates audio samples.
- `NSUInteger inChannels`
    Number of channels of the input audio samples.
- `NSUInteger outChannels`
    Number of channels of the output audio samples should be generated by the audio post-processor.
- `NSUInteger samplesPerChannel`
    Number of samples in ’pBuffer’ argument of audioAdapter:processBuffer:length: method of NexAudioPostProcessingAdapterDelegate.

### NexClientTimeShiftController Class Reference

**Instance Methods**

- `(id) - initWithNexPlayer:param:`
- `(void) - enable`
- `(void) - disable`

### NexClientTimeShiftParams Class Reference

**Instance Methods**

- `(id) - initWithBufferPath:`

**Properties**

- NSString ∗ fileBufferPath
- NSUInteger timeshiftBufferSize
- NSUInteger timeshiftDuration
- NSUInteger maxBackwardDuration

### NEXPLAYERRemoteFileIOInterface_ Struct Reference

A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

This structure provides replacements for the standard operating system file I/O functions. Basically, to play back local content that is not available via the standard operating system file APIs, all calls to open or read from the file are directed to the function pointers in this structure instead.

This structure is passed to the Remote File I/O Interface when registering the callbacks.

More information about each function pointer can be found in the documentation.

**Public Attributes**

- `NEXPLAYERRemoteFile_OpenFt` Open
- `NEXPLAYERRemoteFile_CloseFt` Close
- `NEXPLAYERRemoteFile_ReadFt` Read
- `NEXPLAYERRemoteFile_SeekFt` Seek
- `NEXPLAYERRemoteFile_Seek64Ft` Seek64
- `NEXPLAYERRemoteFile_WriteFt` Write
- `NEXPLAYERRemoteFile_SizeFt` Size

**See Also**

- NEXPLAYERRemoteFile_OpenFt
- NEXPLAYERRemoteFile_CloseFt
- NEXPLAYERRemoteFile_ReadFt
- NEXPLAYERRemoteFile_SeekFt
- NEXPLAYERRemoteFile_Seek64Ft
- NEXPLAYERRemoteFile_WriteFt
- NEXPLAYERRemoteFile_SizeFt

#### NEXPLAYERRemoteFile\_CloseFt NEXPLAYERRemoteFileIOInterface\_::Close

Close callback (see NEXPLAYERRemoteFile_CloseFt)

#### NEXPLAYERRemoteFile\_OpenFt NEXPLAYERRemoteFileIOInterface\_::Open

Open callback (see NEXPLAYERRemoteFile_OpenFt)

#### NEXPLAYERRemoteFile_ReadFt NEXPLAYERRemoteFileIOInterface_::Read

Read callback (see NEXPLAYERRemoteFile_ReadFt)

#### NEXPLAYERRemoteFile_SeekFt NEXPLAYERRemoteFileIOInterface_::Seek

Seek callback (see NEXPLAYERRemoteFile_SeekFt)

#### NEXPLAYERRemoteFile_Seek64Ft NEXPLAYERRemoteFileIOInterface_::Seek64

Seek64 callback (see NEXPLAYERRemoteFile_Seek64Ft)

#### NEXPLAYERRemoteFile_SizeFt NEXPLAYERRemoteFileIOInterface_::Size

Size callback (see NEXPLAYERRemoteFile_SizeFt)

#### NEXPLAYERRemoteFile_WriteFt NEXPLAYERRemoteFileIOInterface_::Write

Write callback (see NEXPLAYERRemoteFile_WriteFt)

### NexVideoRawBits Struct Reference

This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

**Protected Attributes**

- `uint8_t∗planes [NEXVIDEORAWBITS_NUM_MAX_PLANES]`
    Pointers to video planes up to ’numPlanes’.
- `size_t numPlanes`
    Number of video planes in ’planes’.
- `size_t width`
    Width in pixels of the Y plane, planes[0].
- `size_t height`
    Height in pixels of the Y plane, planes[0].
- `size_t pitch`
    Line stride in bytes of the Y plane, planes[0].

### NexVideoTexture Class Reference

This class represents data of decoded video picture.

**Properties**

- `BOOL isRawbits`
    This property determines whether or not the video picture is in raw bits property or pixelBuffer property.
- `CVPixelBufferRef pixelBuffer`
    This property contains the information of a decoded video picture inCVPixelBufferReftype.
- `NexVideoRawBits rawbits`
    This property contains the information of a decoded video picture inNexVideoRawBitstype.

#### - (BOOL) isRawbits [read], [write], [nonatomic], [assign]

This property determines whether or not the video picture is in rawbits property or pixelBuffer property.

YES if the video picture can be retrieved with rawbits property. NO if the video picture can be retrieved with pixelBuffer property.

#### - (CVPixelBufferRef) pixelBuffer [read], [nonatomic], [assign]

This property contains the information of a decoded video picture in CVPixelBufferRef type.

Valid only if is Rawbits is NO.

#### - (NexVideoRawBits) rawbits [read], [write], [nonatomic], [assign]

This property contains the information of a decoded video picture in NexVideoRawBits type. Valid only if is Rawbits is YES.

### NexVideoTextureReceiver Class Reference

This class provides a way to receive decoded video pictures when a video frame is decoded and becomes available for rendering.

#### + (id) receiverWithPlayer: (NXPlayer ∗) player receivedTexture:(UpdatedTextureBlock) receivedTexture

This method instantiates a NexVideoTextureReceiver instance and requests for the video texture update through the receivedTexture block.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance to request updated video textures.|
| receivedTexture | The block will be invoked with updated video textures.|

**See Also**

- UpdatedTextureBlock

#### - (NexVideoTexture∗) videoTexture [read], [nonatomic], [strong]

The latest video texture received from the NXPlayer instance.

### NXABRDelegate Protocol Reference

This protocol defines a delegate protocol for the application to receive an ABR Track switch event from NexPlayer.

NexPlayer will call the methods provided in this interface automatically during playback to notify the application when an ABR Track switch event has occurred.

In most cases, the handling of this event is optional; NexPlayer will continue to play content normally without the application doing anything special in response to the event received.

#### - (NSUInteger) - nexPlayer:willChangeABRTrackWithParams:

**Parameters**

| Name  | Description  | 
|---|---|
| nxplayer | The NXPlayer instance that this delegate has been assigned to.|
| params | The NXPlayerABRControllerTrackChangeParams structure which consists of bandwidth information.|

**Returns**

The exact track bandwidth that the user wants to set to forcibly.

### NXAsfPlayReadyDescrambler Protocol Reference

A protocol you can implement if you wish to implement ASF PlayReady descrambling.

See NXPlayer::asfPlayReadyDescrambler for additional information.

#### - (int) descramblePlayReadyAsfForPlayer: (NXPlayer ∗) player inputBuffer:(unsigned char ∗) pInputBuffer inputBufferSize:(unsigned int) uiInputBufferSize outputBuffer:(unsigned char ∗) pOutputBuffer outputBufferSize:(unsigned int ∗) puiOutputBufferSize initialVector:(unsigned char ∗) pIVBuffer initialVectorSize:(unsigned int) dwIVBufferSize

Called by the player when there is data available for descrambling.

Note that the descramble method will be called for all data of the requested type (specified by DRMType) even if the data is not encrypted. This is because the player has no way to determine if the data is clear text or encrypted. This method must make that determination separately.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance that this descrambler has been assigned to.|
| pInputBuffer | The original (possibly scrambled) input data.|
| uiInputBufferSize | The size (in bytes) of the input buffer.|
| pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location.|
| puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller than uiInputBufferSize, but not larger.|
| pIVBuffer | The initial vector.|
| dwIVBufferSize | The size (in bytes) of the initial vector|

**Returns**

- 0 if successful
- -1 if there was an error

### NXBoundingBox Struct Reference

This structure is used to store the BoundingBox information which overrides default caption positions.

**Public Attributes**

- `NSUInteger **topPercent**`
- `NSUInteger leftPercent`
    Top position using percent based on the top display edge of caption view.
- `NSUInteger widthPercent`
    Left position using percent based on the left display edge of caption view.
- `NSUInteger heightPercent`
    Width using percent of caption view.

### NXBufferInfo Class Reference

This class retrieves the specified buffer information.

> **Note** Do not create instance of this class directly. Instead, use the NXStatisticsAPI::bufferInfo property.
 
**Example code:**

``` 
NXStatisticsAPI *statisticsAPI = [[NXStatisticsAPI alloc] initWithPlayer: player];
NSUInteger bufferSize = [statisticsAPI.bufferInfo bufferSize: NXBufferInfoMediaTypeAudio];
...
```

**See Also**

- NXStatisticsAPI::bufferInfo

#### - (NSUInteger) bufferedSize: (NXBufferInfoMediaType) mediaType

This method gets the buffered size of current media stream.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The buffered size.

#### - (NXBufferingState) bufferingState: (NXBufferInfoMediaType) mediaType

This method gets the buffering state of current media content.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The buffering state of the current media content.

#### - (NSUInteger) bufferRate: (NXBufferInfoMediaType) mediaType

This method gets the buffer rate : (Buffered size)∗100 / (Total buffer size), or how much percentage full the current buffer is.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The buffer rate of current media stream.

#### - (NSUInteger) bufferSize: (NXBufferInfoMediaType) mediaType

This method gets the buffer size of current media stream.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The buffer size of current media stream.

#### - (NSUInteger) firstFrameCTS: (NXBufferInfoMediaType) mediaType

This method gets the CTS of first frame in the buffer.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The CTS of first frame in the buffer. If there is no frame, return NXBufferInfoValueNotAvailable.

#### - (NSUInteger) initialBufferingSize: (NXBufferInfoMediaType) mediaType

This method gets the initial buffering size of current media stream.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The Initial buffering size of current media stream.

#### - (NSUInteger) initialBufferingTime: (NXBufferInfoMediaType) mediaType

This method gets the initial buffering time of current media stream.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The initial buffering time of current media stream.


#### - (NSUInteger) lastFrameCTS: (NXBufferInfoMediaType) mediaType

This method gets the CTS of last frame in the buffer.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The CTS of last frame in the buffer. If there is no frame, return NXBufferInfoValueNotAvailable.

#### - (NSUInteger) totalDuration: (NXBufferInfoMediaType) mediaType

This method gets the total duration of frames in the buffer.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The total duration of all the frames in the buffer, in milliseconds.

#### - (NSUInteger) totalFrameCount: (NXBufferInfoMediaType) mediaType

This method gets the total count of frames in the buffer.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The total count of all the frames in the buffer.

### NXCaptionAttribute Class Reference

This interface represents the values of the caption attributes for captions.

The caption style attributes set with this interface can be used to change the caption text appearance in the application UI, to allow users to change how caption text is displayed.

#### - (BOOL) autoAdjustment [read], [write], [nonatomic], [assign]

Sets the automatic adjustment for the caption position.

Default value is YES

> **Note**
In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

#### - (UIColor∗) backgroundColor [read], [write], [nonatomic], [strong]

This property sets the background color.

If this value isnil, the background color will be rendered in the default content defined value or transparent if it is not defined.

#### - (CGFloat) backgroundColorOpacity [read], [write], [nonatomic], [assign]

This property sets the background color opacity.

If the value is `NAN`, background color opacity will be rendered in the default content defined value or Opaque(100) if it is not defined.

> **Note** In case of CEA608 caption, NXCaptionView::useCEA608CustomView should be set to YES to use this property.

#### - (NXBoundingBox) boundingBox ** [read] **, ** [write] **, ** [nonatomic] **, ** [assign]**

Sets the BoundingBox information for captions.

If one of the values is NAN, captions will be rendered in the default content defined area.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

Default value is `NAN` for all the attribute.

**See Also**

- NXCaptionAttribute::NXBoundingBox

#### - (NXCaptionEdgeStyle) edgeStyle [read], [write], [nonatomic], [assign]

This property sets the edge style of the CEA 608 closed caption or WebVTT text track text.

Available edge styles are defined by the `NXCaptionEdgeStyle` enumeration and include:

- `NXCaptionEdgeStyle_None` No edge style.
- `NXCaptionEdgeStyle_DropShadow` Caption text displayed with a drop shadow effect.
- `NXCaptionEdgeStyle_Raised` Caption text displayed as if embossed or "raised" out of the screen.
- `NXCaptionEdgeStyle_Depressed` Caption text displayed as if pressed or "depressed" into the screen.
- `NXCaptionEdgeStyle_Uniform` Caption text displayed with a uniform edge effect.

> **Note** In order to an edge style or shadow to be displayed, the property shadow Color must be set in addition to setting the `edgeStyle` with this property. If `shadowColor` is `nil`, no edge style will be displayed.

**See Also**

The shadowColor property

#### - (NXTriState) fontBold [read], [write], [nonatomic], [assign]

Enable/Disable bold font.

If the value isNXTriState_Default, the fontBold will be rendered in the default content defined value or
non-bold if it is not defined.

Default value is NXTriState_Default.

> **Note** In case of CEA608 caption, NXCaptionView::useCEA608CustomView should be set to YES to use this property.

**See Also**

NXCaptionAttribute::NXTriState

#### - (UIColor∗) fontColor [read], [write], [nonatomic], [strong]

This property sets the font color.

If this value is nil, the font color will be rendered in the default content defined value or transparent if it is not defined.

Default value is content described

#### - (CGFloat) fontColorOpacity [read], [write], [nonatomic], [assign]

This property sets the font color opacity.

If the value is NAN, font color opacity will be rendered in the default content defined value or Opaque(100) if it is not defined.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

#### - (NXTriState) fontItalic [read], [write], [nonatomic], [assign]

Enable/Disable italic font.

If the value isNXTriState_Default, fontItalic will be rendered in the default content defined value or non-italic if it is not defined.

Default value is NXTriState_Default.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

**See Also**

- NXCaptionAttribute::NXTriState

#### - (NSString∗) fontName [read], [write], [nonatomic], [strong]

This property sets the fontName.

If the value isnil, font will be rendered in the default content defined value or system font if it is not defined.

> **Note** The possible value will be the one of value in [UIFont familyNames]. 

#### - (CGFloat) fontSize [read], [write], [nonatomic], [assign]

This property sets the font size (in points).

If this value is `NAN`, the caption will be rendered in the default content defined value.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

Default value is NAN.

#### - (NSUInteger) fontSizeScale [read], [write], [nonatomic], [assign]

Sets the font size scale as a percentage.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

Default value is 100

#### - (NXTriState) fontUnderline [read], [write], [nonatomic], [assign]

Enable/Disable underlined font.

If the value is NXTriState_Default, fontUnderline will be rendered in the default content defined value or
non-underline if it is not defined.

Default value is NXTriState_Default.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property. If the edge style is uniform, underline color will be the same as font color

**See Also**

NXCaptionAttribute::NXTriState

#### - (NXHorizontalAlignment) horizontalAlignment [read], [write], [nonatomic], [assign]

Sets the horizontal alignment for captions.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.
 
Default value is NXHorizontalAlignment_Default

**See Also**

NXCaptionAttribute::NXHorizontalAlignment

#### - (UIColor∗) shadowColor [read], [write], [nonatomic], [strong]

This property sets the shadow or edge color.

If this value isnil, the shadow or edge style of the caption text will be rendered in default content defined value or transparent if it is not defined.

> **Note** To ensure that the chosen edge styles are displayed, set `shadowColor` to the desired color value, taking into account the colors of the font/background and font/shadow color opacity (`fontColor` and `backgroundColor`, `fontColorOpacity`, `shadowColorOpacity`).

**See Also**

The `edgeStyle` property

#### - (CGFloat) shadowColorOpacity [read], [write], [nonatomic], [assign]
This property sets the shadow color opacity.

If the value is NAN, shadow color opacity will be rendered in the default content defined value or Opaque(100) if it is not defined.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

#### - (NXVerticalAlignment) verticalAlignment [read], [write], [nonatomic], [assign]
Sets the vertical alignment for captions.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

Default value is `NXVerticalAlignment_Default`

**See Also**

NXCaptionAttribute::NXVerticalAlignment

#### - (UIColor∗) windowColor [read], [write], [nonatomic], [strong]

This property sets the window color.

If the value isnil, the window color will be rendered in the default content defined value or transparent if it is not defined.

> **Note** In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

#### - (CGFloat) windowColorOpacity [read], [write], [nonatomic], [assign]
This property sets the window color opacity.

If the value is NAN, window color opacity will be rendered in the default content defined value or Opaque(100) if it is not defined.

> **Note**In case of CEA608 caption, NXCaptionView::use CEA608CustomView should be set to YES to use this property.

### NXCaptionRenderController Class Reference

#### - (void) clearCaptionView

This property clears all the captions currently rendered on the screen.

#### - (NXCaptionAttribute∗) captionAttribute [read], [write], [nonatomic], [copy]

This property changes caption attributes (including font color, background color, and edge style) to user-defined settings.

While caption attributes are often defined in content specifications, this property can be used to allow users to change the way CEA 608 closed caption and WebVTT text track text are displayed in content (similar support for other caption specifications is currently being developed).

Users can be allowed to set the colors of caption text and background and the edge style to use on text (dropshadow, raised, depressed, or uniform), as well as setting the window color and font size on WebVTT text track captions (not available for CEA 608).

#### - (BOOL) captionHidden [read], [write], [nonatomic], [assign]
This property sets visibility state of captions available in content.

Assigning `NO` hides captions (CEA 608 and CEA 708 closed captions, 3GPP and TTML timed text, and WebVTT
text tracks) in the current NXPlayerView.

Default value is NO.

### NXCEA608Caption Class Reference

Represents a complete CEA 608 caption display.

CEA 608 closed captions, unlike other subtitle formats, do not merely include text captions associated with the playing content but also support numerous other attributes including caption color (text and background), text effects (italics, flashing characters, and underlining), and text positioning on the screen as well as supporting an animated "rolling up" display of the captions.

While NexPlayer handles and displays these closed captions according to the specification in `NXCEA608CaptionView` if they are turned on using NXPlayer::selected CEA608Channel, this interface can also be used to handle and display the captions independently if another view is provided.

#### - (void) drawCaptionsInRect: (CGRect) rect inContext:(CGContextRef) cgx redrawTime:(unsigned int ∗) redrawTime

Draws the captions represented by this object in the specified rectangle.

This generally should be called from within drawRect method of aUIView subclass.

**Parameters**

| Name  | Description  | 
|---|---|
| rect | What area to draw in within the context.|
| cgx | The context in which to draw on.|
| redrawTime | The maximum number of milliseconds to wait before the caption display should be redrawn, even if there are no updates. The two cases where the caption display may need to be redrawn are if there are flashing items to display or if there is a roll-up animation in progress. If this value is zero, it means no redraw is necessary until new subtitle data is received.|

#### - (void) getCellInfo: (NXCEA608CellInfo ∗) cellInfo size:(int) size atRow:(int) row andCol:(int) col

Gets information on the character and attributes of a caption cell.

This method gets the caption cell information for CEA 608 close captions for display. These captions are generally displayed by NexPlayer in the NXCEA608CaptionView, and the captions to display are chosen by setting the channel to receive captions with NXPlayer::selected CEA608Channel.

**Parameters**

| Name  | Description  | 
|---|---|
| cellInfo | The CEA 608 closed caption information to be displayed.|
| size | The size of the caption cell, namely size of (NXCEA608CellInfo)|
| row | The row position of the caption cell. This will be an integer from 0 to 14, or -1 for a row that has "rolled-off" the screen.|
| col | The column position of the caption cell. This will be an integer from 0 to 31.|

#### + (UIColor∗) recommendedUIColorForBG: (NXCEA608Color) color

Gets the recommended UIColor to use for the specified NXCEA608Color, in a background color context.

Based on the color specified by NXCEA608Color, this determines the UIColor to use to display the background
of captions in the cell.

**Parameters**


| Name  | Description  | 
|---|---|
| color | The background color to use for the given caption cell.|

**Returns**

The recommended UIColor for the specified caption color.

**See Also**

NXCEA608Color for supported colors.


#### + (UIColor∗) recommendedUIColorForFG: (NXCEA608Color) color

Gets the recommended UIColor to use for the specified NXCEA608Color, in a foreground color context.

Based on the color specified by NXCEA608Color, this determines the UIColor to use to display the text of captions in the cell. Note that text colors do not include transparency, unlike the background colors of captions.

**Parameters**

| Name  | Description  | 
|---|---|
| color | The text color to use for the given caption cell.|

**Returns**

The recommended UIColor for the specified text caption color.

#### - (NXCEA608Channel) channel [read], [nonatomic], [assign]

The channel (1∼4) to which this CEA 608 caption pertains.

While CEA 608 closed captions can be received from one of four channels, since channels 1 and 2 share field 1 in the NTSC line 21 data, and channels 3 and 4 share field 2, the most commonly used channels are channel 1 and channel 3. These channels also often represent different language captions which may be best selected from the user interface.

Note that if this property is set to ZERO, no channel is selected and the captions are effectively disabled or turned off.

#### - (BOOL) isEmpty [read], [nonatomic], [assign]

YES if this caption is empty (contains no data).

This is a property that can be used for convenience if a CEA 608 closed caption cell is empty. Instead of drawing an entire caption object of empty values, if this is true, it’s possible to merely erase the captions currently displayed on the screen.


#### - (int) rollupBaseRow [read], [nonatomic], [assign]

The base row (0-14) for roll-up captioning in CEA 608 closed captions.

When closed captions are to be displayed "rolling up" on the screen, this value sets the horizontal position of the lowest "base" row in the roll up display. Captions to first be displayed in this base row, and then will be "rolled up" as new rows of captions are added.


####  - (int) rollupRows [read], [nonatomic], [assign]

The number of rows (2-4) of roll-up captioning, or zero if not in roll-up captioning mode.

For CEA 608 closed captions, a roll-up display of captions is supported. If these captions are to roll up on the screen, captions will always begin by appearing in the base row indicated by rollupBaseRow, and will then roll up for the number of row set here.

This property indicates the number of rows to be rolled up and is a number between 2 and 4.

This property as well as rollupBaseRow can be used to position the rows rolling up, and the property `timeSinceRollupStart` should be used to help animate the roll-up display, if animated independently.

#### - (unsigned long) timeSinceRollupStart [read], [nonatomic], [assign]

The time (milliseconds) that has passed since the start of the most recent rollup operation.

In order to animate the rolling up of captions when they are to be displayed in "roll up" mode, this value can be used to determine where to display the rows of text being rolled-up (including the the row of text being "rolled out" of view into row -1).

Based on this number and the amount of time to be taken to roll the rows up to the next position, the rows of captions can be displayed in progressively higher positions until the animation is finished and the new caption can begin to be displayed in the base row.

### NXCEA608CaptionView Class Reference

This view receives and displays CEA 608 closed captions.

This interface must be implemented in order for CEA 608 closed captions to be displayed.

Please see NXCEA608Caption and NXPlayerView for more information.

**Properties**

- NXOnOffDefault bold

#### - (void) setCaption: (NXCEA608Caption ∗) caption

This method displays CEA 608 closed captions on the screen.

Once a view has been created to display CEA 608 closed captions, this method sets and displays the captions as new caption data becomes available.

**Parameters**

| Name  | Description  | 
|---|---|
| caption | The captions to be displayed.|

Please see NXCEA608Caption for more information about CEA 608 closed captions.

### NXCEA608CellInfo Struct Reference

CEA-608 caption cell information.

This structure is used by to store CEA 608 closed caption cell information and is passed to `NXCEA608CaptionView` to be displayed.

**Public Attributes**

- `unsigned short characterCode` The character code of the cell.
- `NXCEA608Charset characterSet` The character set to use to encode the cell.
- `NXCEA608Color backgroundColor` The background color of the character.
- `NXCEA608Color foregroundColor` The foreground color of the character.
- `BOOL large` (ignored by NexPlayer) Whether or not the cell is to be displayed "large".
- `BOOL italic` Whether or not the cell is displayed in italics.
- `BOOL underline` Whether or not the cell is underlined.
- `BOOL flash` Whether or not to display the cell flashing.

### NXClosedCaption Class Reference

**Properties**

- `NXCaptionType type` Type of the caption.
- `NSString∗ text` Caption text that may contain HTML formatting depending on the value of type property.
- `NSString∗ plainText` Caption text without formatting.
- `NSDictionary∗ extraInfo`

### NXContentInfo Class Reference

Information about specific multimedia content.

Information about the currently loaded content is available as an NXContentInfo object via NXPlayer::contentInfo.

**Class Methods**

- `(NSString∗) + stringFromAudioCodecID:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for audio codec IDs.
- `(NSString∗) + stringFromVideoCodecID:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for video codec IDs.
- `(NSString∗) + stringFromFileFormat:` Convenience method that returns a string representation of an NXFileFormat, useful for diagnostic and log output, and for displaying to the user.
- `(NSString∗) + stringFromCaptionType:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for caption types.

#### - (NSString∗) infoAsMultiLineString
Formats the content information as a multi-line string that can be displayed to the user or logged for diagnostic information.

The string includes all of the details included in NXContentInfo, as well as details on all of the streams available within.

The string should be displayed in a fixed-pitch font for best results.

**Returns**

the content information formatted as astring.

#### - (NSArray∗) streamsOfType: (NXMediaType) type

Returns a filtered list of streams containing only streams of a single specific type.

**Parameters**

| Name  | Description  | 
|---|---|
| type | The type of stream (NXMediaTypeAudio, NXMediaTypeVideo) to return.|


**Returns**

An array of NXMediaStreamInfo objects, containing only the elements of NXContentInfo::streams that match
the specified media type.

####  - (unsigned int) audioChannels [read], [write], [nonatomic], [assign]

The number of audio channels in the current content.

This is 1 for mono, 2 for stereo. Some formats may support additional channels. If the content doesn’t include audio, this will be zero.

#### - (NXCodecID) audioCodec [read], [write], [nonatomic], [assign]

The audio codec in use for decoding the content.

If the content doesn’t include audio, or the audio format is not recognized or not supported, this will be zero.

#### - (NXCodecID) captionType [read], [write], [nonatomic], [assign]

The types of captions available in the current content.

In the current version, only the types listed above will be recognized and if captions in another format exist, this will be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN`.

Furthermore, if an external subtitle file is included in addition to another format, this member will be set to the external subtitle type (SMI or SRT).

Since CEA 608 and CEA 708 closed captions cannot be identified until decoding begins, caption Type will also
be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN` when they are included in content.

#### - (NXMediaStreamInfo∗) currentAudioStream [read], [write], [nonatomic], [strong]

The currently selected audio stream within the content.

This applies to content with multiple audio streams. This is one of the streams from the NXContentInfo::streams array.

#### - (NXMediaStreamInfo∗) currentTextStream [read], [write], [nonatomic], [strong]

The currently selected text stream within the content.

This applies to content with multiple text streams. This is one of the streams from the `NXContentInfo::streams` array.

#### - (NXMediaStreamInfo∗) currentVideoStream [read], [write], [nonatomic], [strong]

The currently selected video stream within the content.

This applies to content with multiple video streams. This is one of the streams from the `NXContentInfo::streams` array.

#### - (NSDictionary∗) DRMInfo [read], [write], [nonatomic], [strong]

Information about DRM protection associated with the content.

The exact contents of this dictionary depend on the type of DRM, and whether it is being handled by NexPlayer directly. For DRM handled using custom application-provided descramblers, this dictionary will be empty.

#### - (NXFileFormat) fileFormat [read], [write], [nonatomic], [assign]

The format of the file from which the content was loaded, if applicable.

In cases where there isn’t an applicable file format (such as during some kinds of streaming playback) this will have the value `NXFileFormatNONE`.

**See Also**

NXFileFormat for a list of possible values.

#### - (BOOL) hasAudio [read], [write], [nonatomic], [assign]

YES if the content includes audio.

In some cases, where the content includes audio in a format that NexPlayer doesn’t recognize, this may be NO
even for content with audio. If this is YES, the content includes audio, and NexPlayer is capable of playing back that audio.

#### - (BOOL) hasVideo [read], [write], [nonatomic], [assign]

YES if the content includes video.

In some cases, where the content includes video in a format that NexPlayer doesn’t recognize, this may be NO
even for content with video. If this is YES, the content includes video, and NexPlayer is capable of playing back that video.

#### - (BOOL) junkContent [read], [write], [nonatomic], [assign]

YES if the index table is damaged and operations such as seeking may be problematic.

This allows UI components to alert the user of the problem.

#### - (NSDictionary∗) metaData [read], [write], [nonatomic], [strong]

Additional metadata associated with the content.

The exact contents of this dictionary depend on the content and may change from version to version. ID3 tag values are an example of one kind of metadata that may be associated with content.

#### - (unsigned int) pitch [read], [write], [nonatomic], [assign]

Pitch of the original video frames, in pixels.

The pitch is the actual pixel width of the video frame, including any hidden margin required by the decoder, and any padding needed to byte-align each row. Since NexPlayer handles the display of the video image automatically on iOS, this value is really only useful for diagnostic purposes.

#### - (NSArray∗) streams [read], [write], [nonatomic], [strong]

An array of all audio, video and text streams associated with the content.

Most content has only one video stream and one audio stream, but some file formats and some streaming formats support multiple streams of the same type (for example, to provide audio tracks in multiple languages).

In addition, it is possible for some content that this array may be empty, even though there is audio and video associated with the content. In this case, there is no additional information available about the audio or video beyond the basic information in NXContentInfo, and it is not possible to switch to other tracks.

Each element in this array is an NXMediaStreamInfo object.

To get a list of only one type of media, call streamsOfType: instead of using this property.

#### - (NXDuration) totalPlayTime [read], [write], [nonatomic], [assign]

Total playing time of the media, if applicable.

For some streaming formats (in particular, live streams) there may not be a duration available. In this case, the total play time will be `NXDuration_Unknown`.

#### - (NXCodecID) videoCodec [read], [write], [nonatomic], [assign]

The video codec in use for decoding the content.

If the content doesn’t include video, or the video format is not recognized or not supported, this will be zero.

#### - (unsigned int) videoFrameRate [read], [write], [nonatomic], [assign]

Frame rate of the video, in frames per second.

This is the frame rate specified in the content.

If the device isn’t powerful enough to decode and display the video stream in real-time, the actual number of displayed frames may be lower than this value.

For the actual number of displayed frames, see NXPlayer::video PerformanceStats

### NXDashDRMSessionDelegate Protocol Reference

For internal use only. Please do not use.

#### - (int) DashDRMSessionClose: (NXPlayer ∗) player drmSessionHandle:(long long) hSH

For internal use only. Please do not use.

#### - (int) DashDRMSessionDecryptIsobmffFrame: (NXPlayer ∗) player drmSessionHandle:(long long) hSH initialVector:(char ∗) pIV initialVectorLen:(unsigned int) dwIVLen encFrame:(char ∗) pEncFrame encFrameLen:(unsigned int) dwEncFrameLen decFrame:(char ∗) pDecFrame decFrameLen:(unsigned int ∗) pdwDecFrameLen

For internal use only. Please do not use.

#### - (int) DashDRMSessionOpen: (NXPlayer ∗) player drmSessionHandle:(long long ∗) pSH drmInfo:(char ∗) pDRMInfo pDRMInfoLen:(unsigned int) dwDrmInfoSize

For internal use only. Please do not use.

#### - (int) DashDRMSessionSetCencBox: (NXPlayer ∗) player drmSessionHandle:(long long) hSH boxName:(char ∗) pBoxName boxData:(char ∗) pBoxData boxLen:(unsigned int) dwBoxDataSize

For internal use only. Please do not use.

### NXDeceUVDescrambler Protocol Reference

A protocol to implement if DECE Ultra Violet descrambling should be implemented.

**See Also**

NXPlayer::deceUVDescrambler for additional information.

#### - (int) descrambleDeceUVForPlayer: (NXPlayer ∗) player inputBuffer:(unsigned char ∗) pInputBuffer inputBufferSize:(unsigned int) uiInputBufferSize outputBuffer:(unsigned char ∗) pOutputBuffer outputBufferSize:(unsigned int ∗) puiOutputBufferSize sampleEncryptionBox:(unsigned char ∗) pSampleEncBox sampleEncBoxLen:(unsigned int) dwSampleEncBoxLen sampleIDX:(unsigned int) dwSampleIDX trackID:(unsigned int) dwTrackID

Called by the player when there is DECE Ultra Violet data available for descrambling.

Note that the descramble method will be called for all data of the requested type (specified by NXDRMType) even if the data is not encrypted. This is because the player has no way to determine if the data is clear text or encrypted.

This method must make that determination separately.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance that this descrambler has been assigned to.|
| pInputBuffer | The original (possibly scrambled) input data.|
| uiInputBufferSize | The size (in bytes) of the input buffer.|
| pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location.|
| puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller than `uiInputBufferSize`, but not larger.|
| pSampleEncBox | The `SampleEncryptionBox`, as detailed in [UV] Ultra Violet Protocol Specification.|
| dwSampleEncBoxLen | The length, in bytes, of the data in pSampleEncBox.|
| dwSampleIDX | The index of the media object (frame or sample, depending on the media for- mat) being descrambled.|
| dwTrackID | The Media Track ID, from TfhdBox, as defined in [UV] Ultra Violet Protocol Specification.|

**Returns**

0 if successful, -1 if there was an error.

### NXDeviceInfo Class Reference

This class provides information about the current device.

#### - (NXDeviceInfoConnectionType) dataConnectionType

The type of current data connection of a device.


#### - (NSString∗) deviceId

The ID of a device.


#### - (NSString∗) deviceType

The device type name.

#### - (NSString∗) ipAddress

The IP address of a device.


#### - (NSString∗) platformVersion

The current iOS version of a device.

### NXDRMDescrambler Protocol Reference

The `NXDRMDescrambler` protocol must be adopted and implemented by objects that provide general DRM
descrambling services.

Any object can adopt this protocol, but it is typically adopted by either the NXPlayerDelegate, or by a dedicated. DRM descrambling object.

When assigned to NXPlayer::DRMDescrambler, an object that adopts this protocol will be called for each frame of audio or video data before that frame is decoded. This provides a general opportunity for descrambling the frame.

For types of DRM where descrambling must occur at a different point in the playback process or where additional information is needed, more specific descrambling protocols are provided, and should be used instead of this one where necessary.

This protocol comprises only one method, which is called to perform the descrambling.

#### - (int) descrambleDRMForPlayer: (NXPlayer ∗) player dataType:(NXDRMDataType) type inputBuffer:(unsigned char ∗) pInputBuffer inputBufferSize:(unsigned int) uiInputBufferSize outputBuffer:(unsigned char ∗) pOutputBuffer outputBufferSize:(unsigned int ∗) puiOutputBufferSize

General method for descrambling DRM encrypted content.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance|
| type | The type of frame to be descrambled: `NXDRMDataTypeVideo`,`NXDRMDataTypeAudio`|
| pInputBuffer | The encrypted data to be descrambled|
| uiInputBufferSize | The size of the encrypted data, in bytes|
| pOutputBuffer | The location at which to place the descrambled output data. This may point
to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
| puiOutputBufferSize | The size of the decrypted data. The callback must set this value. This may be equal to or smaller than `uiInputBufferSize`, but not larger.|

**Returns**

The method should return zero if the data was successfully descrambled. In the case of an error, it should return -1.

### NXDynamicThumbnailDelegate Protocol Reference

This protocol defines a delegate protocol for the application to receive Dynamic Thumbnail events from NexPlayer.

NexPlayer will call the methods provided in this interface automatically during playback to notify the application when various Dynamic Thumbnail events have occurred.

In most cases, the handling of these events is optional; NexPlayer will continue play content back normally without the application doing anything special in response to the events received.

#### - (void) onDynamicThumbnailData: (NXPlayer ∗) player width:(NSInteger) width height:(NSInteger) height cts:(NSInteger) cts thumbImage:(UIImage ∗) thumbImage

This method will be called by the NexPlayer when thumbnail data is created.

If the `enableDynamicThumbnail (NXPlayer):` method is called before HLS & Smooth Streaming content
is in the open state, then this method will be called and gets the thumbnail information associated with the content.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NexPlayer object generating the event.|
| width | The width of the thumbnail image.|
| height | The height of the thumbnail image.|
| cts | The current timestamp of the thumbnail image.|
| thumbImage | UIImage instance of the thumbnail image.|

#### - (void) onDynamicThumbnailRecvEnd: (NXPlayer ∗) player

This method will be called by the NexPlayer when the end of thumbnail data is received.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NexPlayer object generating the event.|


### NXHLSAES128Descrambler Protocol Reference

A protocol you can implement if you wish to implement decrypting AES128 an encrypted HTTP Live Streaming content. When registered to NXPlayer::hlsAESDescrambler property, the method defined in this protocol called every time AES128 encrypted HLS content is received.

#### - (int) HLSAES128Descrambler: (NXPlayer ∗) player inputBuffer:(unsigned char ∗) pInBuf inputBufferSize:(unsigned int) dwInBufSize outputBuffer:(unsigned char ∗) pOutBuf outputBufferSize:(unsigned int ∗) pdwOutBufSize segmentURL:(char ∗) pSegmentUrl MpdUrl:(char ∗) pMpdUrl KeyAttribute:(char ∗) pKeyAttr segmentSeq:(unsigned int) dwSegmentSeq key:(unsigned char ∗) pKey keySize:(unsigned int) dwKeySize

Called every time an AES128 encrypted HLS content is received.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance.|
| pInBuf | The encrypted data to be descrambled.|
| dwInBufSize | The size of the encrypted data, in bytes.|
| pOutBuf | The location at which to place the decrypted output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
| pdwOutBufSize | The size of the decrypted data. The callback must set this value. This may be equal to or smaller than dwInBufSize, but not larger.|
| pSegmentUrl | A pointer to the URL of the segment of content.|
| pMpdUrl | A pointer to the original URL of the content playlist.|
| pKeyAttr | A pointer to the decryption Key information.|
| dwSegmentSeq | The sequence number of the TS segment file.|
| pKey | A pointer to the decryption Key. This parameter is only meaningful when dw- KeySize is greater than 0 (i.e. a key has been downloaded).|
| dwKeySize | The size of the decryption Key. This parameter will be zero if no key has been downloaded.|

**Returns**

```
1 if successful; 0 if there was an error.
```

**See Also**

`NXPlayer::hlsAESDescrambler`

### NXHLSTSDescrambler Protocol Reference

A protocol you can implement if you wish to implement HTTP Live Streaming TS segment descrambling.

#### - (NexHLSTSDescrambleResult) descrambleHLSTS: (NXPlayer ∗) player inputBuffer:(unsigned char ∗) pInputBuffer inputBufferSize:(unsigned int) uiInputBufferSize outputBuffer:(unsigned char ∗) pOutputBuffer outputBufferSize:(unsigned int ∗) puiOutputBufferSize [optional]

Called by the player when there is data available for descrambling.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance.|
| pInputBuffer | The encrypted data to be descrambled.|
| uiInputBufferSize | The size of the encrypted data, in bytes|
| pOutputBuffer | The location at which to place the descrambled output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
| puiOutputBufferSize | The size of the decrypted data. The callback must set this value. This may be equal to or smaller than uiInputBufferSize, but not larger.|

**Returns**

`NexHLSTSDescrambleResultSucceed` if successful, `NexHLSTSDescrambleResultError` if there was an error, or `NexHLSTSDescrambleResultNeedMoreBuffer` if `uiInputBufferSize` is smaller than the output data in bytes.

**See Also**

NexHLSTSDescrambleResult

#### - (NexHLSTSDescrambleResult) descrambleHLSTS: (NXPlayer ∗) player inputBuffer:(unsigned char ∗) pInputBuffer inputBufferSize:(unsigned int) uiInputBufferSize outputBuffer:(unsigned char ∗) pOutputBuffer outputBufferSize:(unsigned int ∗) puiOutputBufferSize mediaFileURL:(char ∗) pMediaFileURL playlistURL:(char ∗) pPlaylistURL [optional]

Called by the player when there is data available for descrambling.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance.|
| pInputBuffer | The encrypted data to be descrambled.|
| uiInputBufferSize | The size of the encrypted data, in bytes.|
| pOutputBuffer | The location at which to place the descrambled output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the decrypted data may be smaller than the encrypted data, but not larger.|
| pOutputBufferSize | The size of the decrypted data. The callback must set this value. This may be equal to or smaller than uiInputBufferSize, but not larger.|
| pMediaFileURL | The URL of the media file.|
| pPlaylistURL | The URL of the playlist.|

**Returns**

NexHLSTSDescrambleResultSucceed if successful, NexHLSTSDescrambleResultError if there was an error,
or NexHLSTSDescrambleResultNeedMoreBuffer if uiInputBufferSize is smaller than the output data in bytes.

**See Also**

NexHLSTSDescrambleResult


### NXHTTPCredentialsProvider Protocol Reference

Classes that will handle requests for HTTP credentials during streaming playback should implement this protocol.

See `NXPlayer::HTTPCredentialsProvider` for details.

#### - (NSDictionary∗) HTTPCredentialHeaders [optional]

Called whenever NexPlayer receives an HTTP 401 response during streaming play.

> **Deprecated** This only handled the HTTP 401 case; please use HTTPCredentialHeadersForHTTPStatusCode:responseData: instead.

See NXPlayer::HTTPCredentialsProvider for more information.

#### - (NSDictionary∗) HTTPCredentialHeadersForHTTPStatusCode: (unsigned int) statusCode responseData:(NSData ∗) responseData [optional]

Called whenever NexPlayer receives an authentication failure response (HTTP 401 or HTTP 407) during streaming play.

If this is implemented, it takes precedence over the older HTTPCredentialHeaders method (and HTTPCredentialHeaders will not be called);

**Parameters**

| Name  | Description  | 
|---|---|
| statusCode | The status code received from the HTTP server (401 or 407)|
| responseData | The actual response sent by the server. This is backed by a buffer internal to the SDK, so it should not be retained and must not be accessed after this function returns. If it is necessary to access this data later, make a copy in a new NSData object.|

**Returns**

A dictionary containing the HTTP headers to add when retrying the request (the header field names are in the dictionary keys; the header field values are the dictionary values).

See NXPlayer::HTTPCredentialsProvider for more information.

### NXHTTPRetrieveDelegate Protocol Reference

This protocol defines a delegate protocol for the retrieval and offline playback of HLS content stored with NexPlayer.

Any application that will handle retrieval of HLS content stored for offline playback must implement this protocol.

Refer to the `NXHTTPStoreDelegate` protocol for details on how HLS content can be stored so that it can be retrieved with this delegate protocol.

Once HLS content has been stored by NexPlayer, to retrieve and play that content offline:

1. Set the bitrate using setVideoBitrates:len:withOption:to the same bitrate used to store the HLS content.
2. Implement the `NXHTTPRetrieveDelegate` protocol and call the `HTTPRetrieve:url:retrieve    Offset:receivedLength:outputBuffer:retrievedSize:` function to retrieve offline content.
3. Open, start, and stop the player normally as with any HLS content (except that the previously stored content will be played).

**See Also**

NXHTTPStoreDelegate

#### - (int) HTTPRetrieve: (NXPlayer ∗) player url:(char ∗) pURL retrieveOffset:(unsigned long long) dwOffset receivedLength:(unsigned long long) dwLength outputBuffer:(char ∗∗) ppOutputBuffer retrievedSize:(unsigned long long ∗) pdwSize

This function retrieves HLS content previously stored so that it can be played when a device is offline.

Once stored content is retrieved by calling this function, the offline content can be opened, started, and stopped normally with the player.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance that this delegate has been assigned to.|
| pURL | The pointer to the URL of the HLS content stored.|
| dwOffset | The stored offset from the beginning of the content to be played offline.|
| ppOutputBuffer | A pointer to the output buffer for the HLS content previously stored.|
| pdwSize | The size of the stored content retrieved to be played offline.|

### NXHttpStateDelegate Protocol Reference

A delegate method for `NXStatisticsAPI`. Implement this to receive HTTP state information. These methods are optional; implement the methods if you wish to receive the HTTP state information.


#### - (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDataReceived:(NXHttpStateInfoDataReceived ∗) dataReceived [optional]

This event occurs when NexPlayer is downloading a file which is one of NXHttpStateInfoFileType.

**Parameters**

| Name  | Description  | 
|---|---|
| dataReceived | The detailed dataReceived information (see `NXHttpStateInfoDataReceived`).|

#### - (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDownEnd:(NXHttpStateInfo- DownEnd ∗) downEnd [optional]

This event occurs when NexPlayer finished downloading a file which is one of NXHttpStateInfoFileType.

**Parameters**

| Name  | Description  | 
|---|---|
| downEnd | The detailed downEnd information (see `NXHttpStateInfoDownEnd`).|


#### - (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDownStart:(NXHttpStateInfo- DownStart ∗) downStart [optional]

This event occurs when NexPlayer started downloading a file which is one of the NXHttpStateInfoFileType.

**Parameters**

| Name  | Description  | 
|---|---|
| downStart | The detailed downStart information (see `NXHttpStateInfoDownStart`).|


#### - (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoHttpError:(NXHttpStateInfo- HttpError ∗) httpError [optional]

This event occurs when NexPlayer encountered an error during download.


**Parameters**

| Name  | Description  | 
|---|---|
| httpError | The detailed error information(see NXHttpStateInfoHttpError).|


### NXHttpStateInfoDataReceived Class Reference

#### - (NSInteger) bytesReceived [read], [nonatomic], [assign]

The current number of bytes received, as aninteger.

#### - (NSInteger) totalSize [read], [nonatomic], [assign]

The total bytes of the content to be downloaded. -1 represents unknown.

### NXHttpStateInfoDownEnd Class Reference

#### - (NSInteger) bytesReceived** [read] **,** [nonatomic] **,** [assign]

The current number of bytes received, as aninteger.

### NXHttpStateInfoDownStart Class Reference

#### - (NXHttpStateInfoFileType) fileType [read], [nonatomic], [assign]

The file type to be downloaded.

**See Also**

NXHttpStateInfoFileTypefor more details.

#### - (NXHttpStateInfoMediaType) mediaType [read], [nonatomic], [assign]
The media type of the current content.

**See Also**

NXHttpStateInfoMediaType for more details.

#### - (NSUInteger) segmentDuration [read], [nonatomic], [assign]

The duration of the current segment, as an integer.

#### - (NSUInteger) segmentNumber [read], [nonatomic], [assign]

The current segment number, as an integer.

#### - (NSUInteger) trackBW [read], [nonatomic], [assign]

The bandwidth of the current track, as an integer.

### NXHttpStateInfoHttpError Class Reference

#### - (NXError) errorCode [read], [nonatomic], [assign]

The error code.

**See Also**

`NXError` for more details.

### NXHTTPStoreDelegate Protocol Reference

This protocol defines a delegate protocol for the HLS offline storage feature in NexPlayer.

Any application that will handle HLS offline storage must implement this protocol.

In order to store content for offline playback:

1. NXPlayer should set a desired bitrate using the setVideoBitrates:len:withOption.
2. The NXHTTPStoreDelegateshould be implemented. The `HTTPStore:url:storeOffset:receivedLength:storeBuffer:retrievedSize:` method will be called when HLS contents need to be stored.
3. The player should be opened with a call to mode: NXOpenModeStoreStream.
4. Then the player should be started with a call to `nexPlayer:completedAsyncCmdOpenWithResult:playbackType:` from the NXPlayer delegate.
5. After contents are stored, stop: should be called once the event `nexPlayerDidReachEndOFContent` is received by `NXPlayerDelegate`.

Once content is stored for offline playback, an application can implement NXHTTPRetrieveDelegate to retrieve the stored HLS content and play it back.

**See Also**

NXHTTPRetrieveDelegate

#### - (int) HTTPStore: (NXPlayer ∗) player url:(char ∗) pURL storeOffset:(unsigned long long) dwOffset receivedLength:(unsigned long long) dwLength storeBuffer:(char ∗) pBuffer retrievedSize:(unsigned long long) dwSize

This function stores HLS content for playback offline.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance that this delegate has been assigned to.|
| pURL | A pointer to the URL of the HLS content to be stored for offline playback|
| dwOffset | The offset from the beginning of content at which the delegate should start storing for offline playback|
| dwLength | The received length of the content to be stored.|
| pBuffer | A pointer to the buffer where content downloaded for offline playback will be stored.|
| dwSize | The size of the stored content to be retrieved for offline playback.|

### NXManifestAndPlaylistDescrambler Protocol Reference

The `NXManifestAndPlaylistDescrambler` protocol must be adopted and implemented by objects that
provide manifest/playlist descrambling services.

Any object can adopt this protocol, but it is typically adopted by either the NXPlayerDelegate, or by a dedicated descrambling object.

When assigned to NXPlayer::manifestAndPlaylistDescrambler, an object that adopts this protocol will be called whenever a top-level playlist or manifest is obtained, and at that point can perform any descrambling that is necessary.

This protocol comprises only one method, which is called to perform the descrambling.

#### - (int) descrambleForPlayer: (NXPlayer ∗) player URL:(NSURL ∗) url manifestOrPlaylistData:(char ∗) pData length:(unsigned int ∗) pdwDataLen

Method for descrambling top-level playlists and manifests.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance.|
| url | The URL from which this top-level playlist or manifest was retrieved (in the case of redirection, this will be the URL before redirection).|
| pData | The contents of the playlist. Descrambling should be done in-place, so on input this is the scrambled playlist, and on output it is the descrambled playlist.|
| pdwDataLen | On input, the size of the original (scrambled) playlist; on output, the size of the descrambled playlist. Note that the output size must be equal to or smaller than the input size.|

**Returns**

The method should return zero if the data was successfully descrambled. In the case of an error, it should
return -1.

### NXMediaStreamInfo Class Reference

Information about a media stream.

For some local formats, and some streaming formats, multiple alternate media streams may be available. For
example, audio may be available in multiple languages.

Media streams are described by `NXMediaStreamInfo` objects. The list of streams available can be found in `NXContentInfo::streams`, and the currently selected audio and video streams can be found in `NXContentInfo::currentVideoStream` and `NXContentInfo::currentAudioStream`, respectively.

Streams may contain multiple tracking comprising the same media encoded at different quality levels. This allows the player to automatically switch between tracks based on the quality of the network connection and the available bandwidth.

The full list of tracks available for a stream is in the array `NXMediaStreamInfo::tracks`; the current track that has been automatically selected by the player is in `NXMediaStreamInfo::currentTrack`

Some streaming formats support variations on the content (not merely the encoding). Tracks that contain different content are marked with custom attributes to distinguish them from tracks that are merely variations in quality.

#### - (NSString∗) infoAsMultiLineString

Formats the media stream information as a multi-line string that can be displayed to the user or logged for diagnostic information.

The string includes all of the details included in NXMediaStreamInfo.

The string should be displayed in a fixed-pitch font for best results.

**Returns**

The media stream information formatted as a string.

#### - (NSArray∗) customAttrSetIDs [read], [write], [nonatomic], [strong]

Numeric IDs for each supported combination of custom attributes as an array of NSNumber objects.

These are internal identifiers and their use is discouraged except for debugging and diagnostic purposes.

#### - (NSString∗) inStreamID [read], [write], [nonatomic], [strong]

This is the INSTREAM-ID TAG of the media stream.

This is an arbitrary value set by the author, and is intended for user display (to allow users to select among different alternative streams).

#### - (unsigned int) internalId [read], [write], [nonatomic], [assign]

An internal numeric ID that uniquely identifies a stream.

This can be used to determine if two different `NXMediaStreamInfo` objects refer to the same stream:

```objc
if( [mediaStreamInfoA internalId] == [mediaStreamInfoB internalId] ) {
// mediaStreamInfoA and mediaStreamInfoB refer to the same stream
}
```

However, since a given `NXContentInfo` object can only refer to one set of `NXMediaStreamInfo` objects (one per stream), it is generally safe to simply test for identity:

```objc
if( [contentInfo.streams objectAtIndex:i] == contentInfo.currentAudioStream )
{
// The object at index i is the current audio stream
}
```

The actual integer value that appears here is arbitrary and may be any 32-bit value. The method for assigning the internal ID may change in future versions.

#### - (NSString∗) language [read], [write], [nonatomic], [strong]

The language of the stream.

Some stream formats may not include language information. The exact format of the language string depends on
the format of the content and the options chosen by the author of the stream.

#### - (NSString∗) name [read], [write], [nonatomic], [strong]

The name of the stream.

Not all streaming formats include stream names, so it is possible for the stream name to be empty.

#### - (NXCodecID) representCodecType [read], [write], [nonatomic], [assign]

The type of codec available in the stream.

it will be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN` until the stream is downloaded. If this is for CEA
608/708 captions embedded in the content, it will be represented as `NXTypes::(NXCodecID)NXCodecID_TEXT_CC_CEA`

### NXPDBlockDescrambler Protocol Reference

The `NXPDBlockDescrambler` protocol must be adopted and implemented by objects that provide descrambling services for individual blocks of data received during progressive download and playback.

Any object can adopt this protocol, but it is typically adopted by either the NXPlayerDelegate, or by a dedicated DRM descrambling object.

When assigned to NXPlayer::PDBlockDescrambler, an object that adopts this protocol will be called for each block of a file received via progressive download.

This protocol comprises only one method, which is called to perform the descrambling.

#### - (void) descramblePDBlockForPlayer: (NXPlayer ∗) player data:(char ∗) data size:(int) size offset:(long long) offset

Method for descrambling encrypted blocks of data received via progressive download.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The calling NXPlayer instance.|
| data |The block of data received via progressive download. This should be descrambled in-place and the revised data should be written to the same location.|
| size | The size of the block, in bytes. The output size and the input size must be the same, so this value cannot be changed.|
| offset | Offset into the original file at which this block begins.|

### NXPicTiming_ClockTSInfo Struct Reference

This class allows NXPlayer to handle SEI picture timing information in H.264 content.

In summary, this class passes timing information about each video frame in H.264 content if the content provides SEI picture timing information. NXPlayer passes an instance of this class.

In most cases, this information will include `full_timestamp_flag`, `seconds_value`, `minutes_value`,
and `hours_value`. But also note that `seconds_value`, `minutes_value`, and `hours_value` are valid **only** if `full_timestamp_flag` is 1.

For more in depth information about SEI picture timing information, please see the H.264 specifications.

#### unsigned char NXPicTiming_ClockTSInfo::clock_timestamp_flag

This is the clock timestamp flag of SEI picture timing information in H.264 content.

**Values:**

- 1 : Indicates that several clock timestamp syntax elements are present and follow immediately.
- 0 : Indicates that the related clock timestamp elements are **present**.

#### unsigned char NXPicTiming_ClockTSInfo::cnt_dropped_flag

This is the `cnt_dropped_flag` value in SEI picture timing information in H.264 content.

Based on the counting method set by `mCountingType`, this value specifies that one or more values of `mNFrames` should be skipped.

#### unsigned int NXPicTiming_ClockTSInfo::counting_type

This is the counting_type value in SEI picture timing information in H.264 content.

It indicates the method of dropping values of then_framesin SEI picture timing information.

**Values:**

- 0 : no dropping of n_frames count values and no use of time_offset
- 1 : no dropping of n_frames count values
- 2 : dropping of individual zero values of n_frames count
- 3 : dropping of individual MaxFPS - 1 values of n_frames count
- 4 : dropping of the two lowest (value 0 and 1) n_frames counts when seconds_value is equal to 0 and minutes_value is not an integer multiple of 10
- 5 : dropping of unspecified individual n_frames count values
- 6 : dropping of unspecified numbers of unspecified n_frames count values
- 7..31 : Reserved.

#### unsigned int NXPicTiming_ClockTSInfo::ct_type

This is the scan type of the source material from SEI picture timing information in H.264 content.

**Values:**

- 0 : Original picture scan was progressive.
- 1 : Original picture scan was interlaced.
- 2 : Original picture scan is unknown.
- 3 : Reserved.

#### unsigned char NXPicTiming_ClockTSInfo::discontinuity_flag

This is the discontinuity_flag value in SEI picture timing information in H.264 content.

Please see the H.264 specifications for details in how to interpret the values here.

**Values:**

- 0 : Continuous clock timestamps.
- 1 : Discontinuity in clock timestamps.

#### unsigned char NXPicTiming_ClockTSInfo::full_timestamp_flag

This is the full_timestamp_flag value in SEI picture timing information in H.264 content.

**Values:**

- 0 : Indicates that then_frames element is followed only by the seconds_flag
- 1 : Indicates that a full timestamp is included and that then_frames element is followed by seconds_value, minutes_value, and hours_value.

#### unsigned int NXPicTiming_ClockTSInfo::hours_value

This is the hours_value in SEI picture timing information in H.264 content.

**Values:** 

0 to 23 (inclusive)

#### unsigned int NXPicTiming_ClockTSInfo::minutes_value

This is the minutes_value in SEI picture timing information in H.264 content.

**Values:** 

0 to 59 (inclusive)

#### unsigned int NXPicTiming_ClockTSInfo::n_frames

This is the seconds_value in SEI picture timing information in H.264 content.

**Values:** 

0 to 59 (inclusive)

#### unsigned char NXPicTiming_ClockTSInfo::nuit_field_based_flag

This is the nuit_field_based_flag in SEI picture timing information in H.264 content.

This value can be used to calculate the clock timestamp of H.264 video frames.

####  unsigned int NXPicTiming_ClockTSInfo::seconds_value

This is the minutes_value in SEI picture timing information in H.264 content.

**Values:** 

0 to 59 (inclusive)

#### int NXPicTiming_ClockTSInfo::time_offset

This is the time_offset value in SEI picture timing information in H.264 content.

It can be used to determine the clock timestamp.

### NXPicTimingInfo Struct Reference

**Public Attributes**

- unsigned int **cpb_removal_delay**
- unsigned int **dpb_output_delay**
- unsigned int **pic_struct**
- unsigned int **NumClockTS**
- NXPicTiming_ClockTSInfo **TSInfo** [3]
- unsigned int **uiPTS**
- unsigned int **uiDTS**

### NXPiffPlayReadyDescrambler Protocol Reference

A protocol you can implement if you wish to implement Piff PlayReady descrambling.

See `NXPlayer::piffPlayReadyDescrambler` for additional information.

#### - (NSInteger) descramblePiffPlayReadyForPlayer: (NXPlayer ∗ )playerinputBuffer:(unsigned char ∗ )pInputBufferinputBufferSize:(unsigned int)uiInputBufferSizeoutputBuffer:(unsigned char ∗ )pOutputBufferoutputBufferSize:(unsigned int ∗ )puiOutputBufferSizesampleEncBox:(unsigned char ∗ )pSampleEncBoxsampleEncBoxLen:(unsigned int)dwSampleEncBoxLensampleIndex:(unsigned int)dwSampleIDXtrackID:(unsigned int)dwTrackID

Called by the player when there is Piff PlayReady data available for descrambling.

This is called every time Piff PlayReady data is received, regardless of whether or not the content is encrypted. It is the responsibility of this callback to determine whether or not the data is encrypted and descramble the data if necessary.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| | player | The `NXPlayer` instance that this descrambler has been assigned to. |
| in | pInputBuffer | The original (possibly scrambled) input data. |
| | uiInputBufferSize | The size (in bytes) of the input buffer. |
| out | pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location. |
| out | puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller than `uiInputBufferSize`, but not larger. |
| out | pSampleEncBox | The `SampleEncryptionBox`, as detailed in the *[MS-SSTR]* Smooth Streaming Protocol Specification. |
| | dwSampleEncBoxLen | The length, in bytes, of the data at `pSampleEncBox`
| | dwSampleIDX | The index of the media object (frame or sample, depending on media format) being descrambled. |
| | dwTrackID | Media Track ID, from `TfhdBox`, as defined in the *[MS-SSTR]* Smooth Streaming Protocol Specification. |

### NXPlayer Class Reference

This class represents a player instance, and provides for opening, playing and controlling both local and streaming content.

If the content includes video, this class requires a CAEAGLLayer in which to display the video.

The `NXPlayerView` class provides a CAEAGLLayer for video output, and even handles the creation of an associated `NXPlayer` instance automatically (this instance can be accessed through `NXPlayerView::player`).

Alternatively, you can create your own UIView subclass with CAEAGLLayer support, and assign the layer from that class to `NXPlayer::renderLayer`. If you do this, you should also have the layout Subviews method of the custom UIView subclass call `prepareVideoBuffers (NXPlayer)` to adjust the size of the OpenGL buffers to match the new size of the layer.

If your content does not include video, or if you do not care about displaying that video, you may safely create an`NXPlayer` instance without an associated render layer.

#### - (void) addEventReceiver: (id < NXPlayerDelegate > )receiver

This method adds an event receiver.

> **Note** If the developer wants to register several delegates, they can register receivers with this method.

Events will be forwarded in sequence from receivers to delegate.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | receiver | The object that implements `NXPlayerDelegate` to which methods will be called when events occur. |

**See Also**

`NXPlayerDelegate`

#### - (NXError) addHTTPHeaderFields: (NSString ∗ )headerFieldString

This function adds additional header fields to be sent along with the HTTP headers when sending streaming requests for HLS and Smooth Streaming content.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | headerFieldString | The field to add; this should include both the field name and the value for the field, separated by a colon character, in the normal HTTP header field format. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) addRTSPHeaderField: (NSString ∗ )headerFieldStringforMethods:(NXRTSPMethod)methodCombination

Specifies additional fields to be sent along with the normal headers in RTSP requests.

RTSP requests are very similar to HTTP requests, and include a header consisting of a set of required fields. This method adds additional fields that will be sent as part of future RTSP requests.

One possible use of this, for example, is to set a user agent identifier to be used in RTSP requests.

Each call to this method adds one field. To add multiple fields, call this method multiple times. There is currently no way to delete a field once it has been added, although the value could be set to an empty string.

If the specified field already exists, the current value of that field and the set of RTSP methods to which it applies will be over written. That is, if this method is called more than once with the same header field specified, only the most recent call will be used for the value and RTSP method set of that header field.

There are several request types that are part of the RTSP protocol, and when a header is added, you must specify with which request types it will be included. This is done by performing a bitwise OR on one or more of the following values, and specifying the result in the `methodCombination` parameter:

- NXRTSPMethodNone
- NXRTSPMethodDescribe
- NXRTSPMethodSetup
- NXRTSPMethodPlay
- NXRTSPMethodPause
- NXRTSPMethodTeardown
- NXRTSPMethodOptions
- NXRTSPMethodRedirect
- NXRTSPMethodSetParameter
- NXRTSPMethodGetParameter
- NXRTSPMethodAnnounce
- NXRTSPMethodPlaylist
- NXRTSPMethodAll

For example:

```objc
[hNexPlayer addRTSPHeaderField:@"User-Agent: NexStreaming Android Player"
				forMethods:NXRTSPMethodSetup|
		NXRTSPMethodPlay];
```

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | headerFieldString | The field to add; this should include both the field name and the value for the field, separated by a colon character, in the normal RTSP header field format. |
| in | methodCombination | The combination of methods for which this header will be sent. This is one or more of the possible values for NXRTSPMethod combined using a bitwise OR operation. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) clearToBlack

Clears the render layer to black.

When the player is paused, stopped, or even closed, the last frame that was displayed will remain visible on the render layer. This is done in case an application wishes to play additional content on the same layer without it flashing to black in between. However, in many applications, it is desirable to clear the render layer to black when playback is stopped. In this case, simply call this method in response to the `nexPlayer:completedAsyncCmdStopWithResult:` callback of the delegate.

This should not be called while video is actually playing, because the next frame will immediately be drawn, and the
black frame will merely be shown for a fraction of a second, causing the video to flicker.

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) close

Closes any currently open content.

If the content is currently playing or paused, the content will be stopped first before it is closed (this behavior differs from the old API, where the content must be stopped before closing it to avoid unpredictable behavior).

Note that in some cases (such as when this is called while content is already playing, or if an open method is called while there is already open content) the content we automatically be closed when the nexPlayer:completedAsyncCmdStopWithResult: (NXPlayerDelegate-p) even occurs. In this very particular case, an additional (redundant) call to the close method inside the nexPlayer:completedAsyncCmdStopWithResult: (NXPlayerDelegate-p) handler will be ignored.

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) disableDynamicThumbnail

This method disables the Dynamic Thumbnail feature, if enabled.

> **Warning** The Dynamic Thumbnail feature must be disabled by calling this method before calling close when a player is being closed.

**Returns**

Zero for success, or a non-zero NexPlayer error code in the event of a failure.

#### - (NXError) enableDynamicThumbnail

This method is used to enable and apply the Dynamic Thumbnail feature for HLS & Smooth Streaming content.

Refer to the following steps to use this method accurately:

1. The `enableDynamicThumbnail:` method should be called before `open:`.
2. When `open:` is successful, use the `NXPlayer::contentInfo` to get the total playtime of the content.
    By dividing the extracted total playtime value by the number of the thumbnail buffer array from the UI (the number of available thumbnails), the interval time is determined. The interval time can then be used with the `setOptionDynamicThumbnail:` method to get thumbnail information.
3. If the setting above works normally, NexPlayer will use the `onDynamicThumbnailData()` method to
    send thumbnail data to the UI.
4. The `disableDynamicThumbnail:` method should be called before `close:` when closing content.
5. If a video track is changed while content is playing, these methods should be called in the following order:
    - FIRST, `disableDynamicThumbnail:`
    - SECOND, `enableDynamicThumbnail:` to enable Dynamic Thumbnails for the new content, and
    - LASTLY, `setOptionDynamicThumbnailwithOption:` NexDynamicThumbnailOption::NexDynamicThumbnailOptionInterval andParam1:interval_time andParam2:0 to set the appropriate interval for the new thumbnails.

**Returns**

Zero for success, or a non-zero NexPlayer error code in the event of a failure.

#### - (float) getAirPlayRate

Return current play rate of AirPlay.

This value is to check current AirPlay player’s status.

**Returns**

- `-111.0`: invalid not activated AirPlay
- `0.0`: pause state of AirPlay
- `above0.1` : playing of AirPlay

#### - (NSInteger) getEffectiveProperty: (NXProperty)property

Gets the effective value of a NexPlayer property.

In the event of an error (for example, an invalid property identifier), an exception is raised.

This is usually the value as set with setProperty:toValue: but it may be different for properties with defaults that
change automatically.

See Properties for details.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | property | Identifies the property to be retrieved. |

**Returns**

The effective value of the property.

#### - (float) getPlaybackRate

Return current playback rate.

This value is to check current the playback rate.

**Returns**

- `0.1∼5.0` : The value of current playback rate.

#### - (NSInteger) getProgramDateTime: (NSInteger ∗ )dwOffsetbuffer:(char ∗ )pValue

This method gets the date and time information in HLS content when the HLS tag, #EXT-X-PROGRAM-DATE-TIME,
is included.

It can be used to determine the current time of the frame and help when syncing content and text or when determining when to play text.

**Parameters**

| Name  | Description  | 
|---|---|
| dwOffset | The time offset of the currently decoding frame’s timestamp with respect to the #EXT-X-PROGRAM-DATE-TIME tag time, in milliseconds. |
| pValue | The playtime of the playlist. |

**Returns**

Always zero.

#### - (NSInteger) getProperty: (NXProperty)property

Gets the value of a NexPlayer property.

In the event of an error (for example, an invalid property identifier), an exception is raised.

This is the value as set with `setProperty:toValue:`

For a few properties, the actual value in effect may be different (for example, it a property is set to a default that varies based on the protocol or device). If the actual value is needed, `getEffectiveProperty:` can be called.

See Properties for details.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | property | Identifies the property to be retrieved. |

**Returns**

The value of the property.

#### - (NXError)getProperty: (NXProperty)propertyvalue:(NSInteger ∗ )pValue

Gets the value of a NexPlayer property.

See Properties for details.

This returns an NXError value to indicate success or failure, and returns the property value at the location pointed to by the `value` argument.

Since the only error that can occur is an invalid property identifier, in many cases it is simpler to just use `getProperty:` instead, which directly returns the property value and indicates an error by raising an exception.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | property | Identifies the property to be retrieved |
| out | value | Points to a location to receive the value of the property |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXSARInfo) getSARInfo

This method retrieves the SAR (Sample Aspect Ratio) of H.264 content when specified.

The sample aspect ratio (SAR) returned by this method is expressed as a ratio of the width of the sample size to the height of the sample size.

It can be used to appropriately display content to the user.

This sample aspect ratio will be one of the following ratios: 1:1, 4:3, 3:2, 2:1, 12:11, 10:11, 40:33, 24:11, 20:11, 32:11, 80:33, 18:11, 15:11, 64:33, or 160:99.

Note that if SAR information is not specified for given H.264 content, the returned ratio will also be 1:1.

For more information about the SAR information included in H.264 content, please consult Table E-1 - Meaning of Sample Aspect Ratio Indicator on page 374 of the H.264 specifications (Rec. ITU-T H.264 (03/2010).

**Parameters**

| Name  | Description  | 
|---|---|
| strSAR | Returns the sample aspect ratio, as a string. |

#### - (void) getSeekableRange: (int32_t ∗ )startTimeendTime:(int32_t ∗ )endTime

This method returns the range of the current content that is seekable.

This method is used to allow NexPlayer to support timeshifting playback within HLS Live and Smooth Streaming content. Based on the amount of content available from the server at a particular time, it determines the seekable range within the playing content which also indicates the range where playback may be timeshifted. This range will be constantly shifting as the live streaming content available from the server changes in real time, so this method will need to be repeatedly called to ensure accurate shifting of playback.

For local content this method will always return the same two values, and the second value indicating the end of the seekable range will continuously change in progressive download (PD) content, but this method is most relevant when playing live streaming content, as with HLS and Smooth Streaming.

For more information about how this method may be used to timeshift playback in live content, please also refer to the introductory section on time shift support.

**Parameters**

| Name  | Description  | 
|---|---|
| startTime[in,out] | A pointer to a `long` that is the timestamp indicating the start of the seekable range. |
| endTime[in,out] | A pointer to a `long` that is the timestamp indicating the end of the seekable range. |

#### - (NXError) goToCurrentLivePosition: (BOOL)exact

Moves to the current live position after the actual playback position.

Normally, when playing live content, previously recorded data (for example, a few seconds earlier than the actual live position) to avoid buffering. This method however ignores this concept and moves directly to the latest loaded playback position (where the server is currently being encoded).

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | exact | If exactis YES, the player will seek exactly to the time specified by msec. Otherwise, the playhead will seek to the nearest approximate position for faster seeking performance |

**Returns**

Zero for success, or a non-zero NexPlayer error code in the event of a failure.

#### - (BOOL) isMediaOnOff: (NXMediaType)mediaType

This returns the current enable state of media for Audio, Video, and Text.

**See Also**

- `setMediaOnOff:mediaType:` This is related to the method and returns the current On/Off state of the mediaType.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | mediaType | The mediaType to disable or enable. The method uses NXMediaType and only values below are valid. NXMediaTypeAudio NXMediaTypeVideo NXMediaTypeText |

**Returns**

**YES** if media of mediaType is enabled; **NO** if not. For invalid mediaType, it also returns **YES**, which is default value for the type.

#### + (BOOL) logging

Returns the current logging state for NexPlayer.

The current logging state is set with `setLogging:`.

**Deprecated** This has been replaced with `logLevel:`. Please use that instead.

**Returns**

**YES** if logging is enabled; **NO** if logging is disabled.

#### + (NXLogLevel) logLevel

Returns the current logging level for NexPlayer.

The logging level is set with `setLogLevel:`.

If logging is turned off, the log level will be `NXLogLevelDisabled`.

**Returns**

The current log level if logging is enabled, `NXLogLevelDisabled` if logging is disabled.

#### - (NXError) open: (NSString ∗ )path

Opens the specified content.

This is a convenience function, and is equivalent to calling NXPlayer::open:mode:subtitles:transport:startAtTime:autoPlay: with a mode of NXOpenModeAuto, a transport of NXTransportTypeTCP, no subtitle path, and `autoPlay` set to **NO**

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path or local or remote URL to the content to be opened. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError)open: (NSString ∗ )pathmode:(NXOpenMode)modesubtitles:(NSString ∗ )subtitlePathtransport:(NXTransportType)transportautoPlay:(BOOL)autoPlay

Opens the specified content.

This is a convenience function, and is equivalent to calling NXPlayer::open:mode:subtitles:transport:startAtTime:autoPlay: with a startAtTime of zero.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path or local or remote URL to the content to be opened. |
| in | mode | Controls how the content is opened. See `NXOpenMode` for details. |
| in | subtitlePath | Local path to a subtitle file containing subtitles or captions to display with the content. Supported formats include SMI, SRT and SUB. |
| in | transport | Specifies the transport type for streaming protocols such as RTSP that support multiple transports. For local content or streaming content that doesn’t support multiple transports, this is ignored. If unsure, set this to `NXTransportTypeTCP`. See `NXTransportType` for details. |
| in | autoPlay | If this is set to YES, NexPlayer automatically manages playback as follows: <br> - Upon successfully opening content, automatically call **start** to begin playback. <br> - Upon reaching the end of content, automatically call **stop** to stop playback. <br> - Upon successfully stopping playback, automatically call close to **close** the player instance.

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicates success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError)open: (NSString ∗ )pathmode:(NXOpenMode)modesubtitles:(NSString ∗ )subtitlePathtransport:(NXTransportType)transportstartAt:(NXDuration)startAtTimeautoPlay:(BOOL)autoPlay

Opens the specified content.

This is an asynchronous operation that completes in the background. When it is finished, the `nexPlayer:completedAsyncCmdOpenWithResult:playbackType: (NXPlayerDelegate-p)` method of the delegate will be called (and the result argument will indicate success or failure).

After content has successfully been opened, you may call **start** to begin playback, or specify `autoPlay:YES`
when opening the content to begin playback automatically when opening is successful.

```objc
// Open the file "test.wmv" that has been added directly to the
// application’s project in Xcode (that is, it will appear in the
// bundle)
NXError result = [hNexPlayer open:@"test.wmv"
mode:NXOpenModeLocalBundle
subtitlePath:nil
transport:NXTransportTypeTCP
startAtTime:0
autoPlay:YES];
```

> **Note** There are several convenience methods that simplify the opening of content by using default values for most of the arguments. You may use these instead of `open:mode:subtitles:transport:autoPlay` if they suit your requirements:
> 
> - open:
> - openFromBundle:
> - openAndPlay:
> - openAndPlayFromBundle:

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path or local or remote URL to the content to be opened. |
| in | mode | Controls how the content is opened. See NXOpenMode for details. |
| in | subtitlePath | Local path to a subtitle file containing subtitles or captions to display with the content. Supported formats include SMI, SRT and SUB |
| in | transport | Specifies the transport type for streaming protocols such as RTSP that support multiple transports. For local content or streaming content that doesn’t support multiple transports, this is ignored. If unsure, set this to `NXTransportTypeTCP`. See `NXTransportType` for details. |
| in | startAtTime | The offset (in milliseconds) from the beginning of the content at which to begin playback, if autoPlay is true. Has no effect if autoPlay is false. |
| in | autoPlay | If this is set to YES, NexPlayer automatically manages playback as follows: <br> - Upon successfully opening content, automatically call **start** to begin playback. <br> - Upon reaching the end of content, automatically call stop to **stop** playback. <br> - Upon successfully stopping playback, automatically call close to **close** the player instance.

**Returns**
 
NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) openAndPlay: (NSString ∗ )path

Opens and begins playing content.

This is a convenience function, and is equivalent to calling NXPlayer::open:mode:subtitles:transport:startAtTime:autoPlay: with a mode of NXOpenModeAuto, a transport of NXTransportTypeTCP, no subtitle path, and autoPlay set to YES

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path or local or remote URL to the content to be opened. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) openAndPlayFromBundle: (NSString ∗ )path

Opens the specified local content from the application bundle and begins playing it.

This is a convenience function, and is equivalent to calling NXPlayer::open:mode:subtitles:transport:startAtTime:autoPlay: with a mode of NXOpenModeLocalBundle, a transport of NXTransportTypeTCP, no subtitle path, and autoPlay set to YES

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path relative to application bundle (usually, just a filename). |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

####  - (NXError) openFromBundle: (NSString ∗ )path

Opens the specified local content from the application bundle.

This is a convenience function, and is equivalent to calling NXPlayer::open:mode:subtitles:transport:startAtTime:autoPlay: with a mode of NXOpenModeLocalBundle, a transport of NXTransportTypeTCP, no subtitle path, and
autoPlayset to NO.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | path | Local path relative to application bundle (usually, just a filename). |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) pause

Pauses playback of content.

Content must be in a playing state or this has no effect.

Playback can be resumed by calling **resume**.

This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::nexPlayer:completedAsyncCmdPause: method of the delegate will be called (and the result argument will
indicate success or failure).

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) prepareVideoBuffers

Creates or adjusts the buffers used for rendering video to match the current dimensions of the render layer.

> **Note** 
> It is not necessary to call this if you are using `NXPlayerView`, because that class automatically manages the render layer.

If you provide your own UIView subclass and set up NXPlayer::renderLayer manually, you must call this function
once after render Layer has been set up, and again any time the dimensions of the layer change. This is usually
done in the layout Subviews method of the UIView subclass, as follows:

```objc
- (void) layoutSubviews { 
    [player prepareVideoBuffers];
}
```

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

**See Also**

`NXPlayer::renderLayer`

####  - (NXError) reconnectNetwork

This method allows NexPlayer to reconnect to the media server in the case of streaming content.

It allows NexPlayer to reconnect to a media server when network conditions may have closed a connection.

> **Warning** This is only supported in HLS, DASH, SmoothStreaming and PD streaming content.

**Returns**

NXErrorNone if successful.

####  - (void) removeEventReceiver: (id < NXPlayerDelegate > )receiver

This removes a receiver which was added with addEventReceiver.

**Parameters**

| i/o  | Name | Description | 
|---|---|---|
| in | receiver | The object that implements NXPlayerDelegate to which methods won’t be called anymore. |

**See Also**

NXPlayer::addEventReceiver

#### - (NXError) resume

Resumes playback of content that was paused with pause.

This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::nexPlayer:completedAsyncCmdResume: method of the delegate will be called (and the result argument will indicate success or failure).

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

####  - (NXError) seekTo: (NXDuration)timestamp

Seeks to the specified time in the content.

If the content is currently playing, it will continue playing after the seek; if it is paused, it will be paused after the seek
operation.

This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::nexPlayer:completedAsyncCmdSeek: method of the delegate will be called (and the result argument will indicate success or failure).

Note that seeking is not possible on all types of content. For live content, seeking may or may not be available. To determine if seeking is possible, check the `isSeekable` member of `NXPlayer::contentInfo`.

In the case of live content that is seekable, the seek timestamp is relative to the seek base, seekBase and the window within which seek can be performed in the content can be determined with the property `seekableLength`.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | timestamp | The offset in milliseconds from the beginning of the content to which to seek. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### + (void) setAVPlayerForAirPlay: (BOOL)bUse

Set to use native AV player for AirPlay internally.

> **Note** set to use native iOS’s AVPlayer for airplay.

AV Player is only activated when using AirPlay. If you use this option, it means that you couldn’t use NexPlayer’s advantages (DASH, MSS, 3rd party package...etc) This is a class method. It’s good to be set before NXPlayer init. The default value for this is NO.

**Parameters**

in bUse use it or not.

- YES: use airplay internally
- NO: don’t use airplay internally (default)

**Returns**

The result value.

#### - (NXError) setCustomID3Tags: (NSArray ∗ )tags

Registers custom ID3 metadata tags to NexPlayer.

To set custom tags, custom ID3 tags should be registered to NexPlayer.

In prior versions of the NexPlayer SDK, it was only possible to input values of the address where the required custom tag data was stored (to set any custom tags) but this method makes it possible to register the custom metadata tags with the custom tag IDs passed as an array.

**Parameters**

| Name  | Description  | 
|---|---|
| tags | Custom ID3 tags as an array. |

**Returns**

Always zero.

####  - (void) setExternalSubtitle: (NSString ∗ )path

This method allows the subtitles for particular content to be switched during playback.

A new subtitle file can be loaded from the device’s storage or from a given URL as passed in the parameter `path`. For example, the user can switch the subtitles to a different language while playing particular content.

**Parameters**

| Name  | Description  | 
|---|---|
| path | The path or the URL to the new subtitle file to use. |

#### + (NXError) setLicenseKeyBuffer: (NSString ∗ )strKeyBuffer

This method inputs the license file information into a NexPlayer buffer.

This should be called before `NXPlayer::init`.

**Parameters**

| Name  | Description  | 
|---|---|
| strBuffer | Information in the license file, as aString. |

**See Also**

NXPlayer::setLicenseKeyFile for more information.

#### + (NXError) setLicenseKeyFile: (NSString ∗ )strKeyPath

This method sets the path to the specific license file included with the NexPlayer SDK.

This should be called before NXPlayer::init. The license file will be included with the NexPlayer SDK files and when called with this API, an application will be able to input the license file information to run NexPlayer.

> **Warning** The license file will be updated regularly, so please always check for updates and be sure to replace and use the latest license file in applications built with the NexPlayer SDK.

**Parameters**

| Name  | Description  | 
|---|---|
| strKeyPath | Path to the license file, as aString. |

**See Also**

NXPlayer::setLicenseKeyBuffer

#### + (void) setLogging: (BOOL)logging

Enables or disables log output of diagnostic information by NexPlayer.

Disabling logging is the same as setting the log level to -1, and enabling logging is the same as setting the log level
to zero. Since other log levels are possible, it is better to set the log level directly rather than use this method.

**Deprecated** This has been replaced with setLogLevel:. Please use that instead.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | logging | Specify YES to enable log output, NO to disable log output. |

####  + (void) setLogLevel: (NXLogLevel)logLevel

Controls the amount of diagnostic information output by NexPlayer.

This should be set before creating the NXPlayer instance. Log data is output as part of initialization, so if this is set after creating the instance, some log data may be lost.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | logLevel | The logging level to set. This determines the amount of diagnostic information the SDK sends to the log. Refer to NXTypes::NXLogLevel: <br> - **NXLogLevelDisabled** : Disables logging. Does not output any log messages. <br> - **NXLogLevelError** : Output basic log messages only (recommended). <br> - **NXLogLevelWarning** ∼ **NXLogLevelExtraVerbose** : Outputs detailed log messages; higher numbers result in more verbose log entries, but may cause performance issues in some cases and are not recommended for general release code. |

#### + (BOOL)setLogLevel:(NXLogLevel)logLevelforced:(BOOL)bForced

This method sets setLogLevel regardless of performance.

From version 5.28 and up, legacy setLogLevel API only sets settings that do not affect the performance. If the user needs a debugging log regardless of performance, set the forced parameter toTRUEand call setLogLevel:forced: to set.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | logLevel | The logging level to set. This determines the amount of diagnostic information the SDK sends to the log. Refer to NXTypes::NXLogLevel: <br> - **NXLogLevelDisabled** : Disables logging. Does not output any log messages. <br> - **NXLogLevelError** : Output basic log messages only (recommended). <br> - **NXLogLevelWarning** ∼ **NXLogLevelExtraVerbose** : Outputs detailed log messages; higher numbers result in more verbose log entries, but may cause performance issues in some cases and are not recommended for general release code. |
| in | bForced | Whether or not to force set logLevel regardless of device performance. |

**Returns**

YES if it is set according to the logLevel parameter, NO if it is force down-set due to performance issues.

#### + (void) setLogLevelToDefault

Resets the logging level to the default.

If used, it is best to call this before creating the NXPlayer instance. Log data is output as part of initialization, so if
this is called after creating the instance, some log data may be lost.

#### - (NXError) setMediaOnOff: (BOOL)bOnOffmediaType:(NXMediaType)mediaType

This method "turns" On/Off media of each Audio, Video, or Text.

This method is only valid when the state of content is between Open and Close. If you wish to apply it after play
begins, call from completedAsyncCmdOpenWithResult:.

> **Note** This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::completedAsyncCmdMediaOnOffWithResult:mediaType:bOnOff method of the delegate will be
> called (and the result argument will indicate success or failure).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | bOnOff | if you want to disable the media, set to NO. if you want to enable the media, set to YES. |
| in | mediaType | The mediaType to disable or enable. The method uses NXMediaType and values below only are valid. NXMediaTypeAudio NXMediaTypeVideo NXMediaTypeText NXMediaTypeAV => not recommended. Return value is not guaranteed. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) setOptionDynamicThumbnailwithOption: (NexDynamicThumbnailOption)optionandParam1:(NSUInteger)param1andParam2:(NSUInteger)param2

This method sets option parameters related to the Dynamic Thumbnail feature in HLS & Smooth Streaming when
handling thumbnail data

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | option | The **option** property to set thumbnail data. |
| in | param1 | The first parameter of the **option** property. |
| in | param2 | The second parameter of the **option** property. If the option being set only needs one parameter, **param2** will be 0.

**Returns**

Zero for success, or a non-zero NexPlayer error code in the event of a failure.

#### - (NXError) setPlaybackRate: (float)playRate

This method is used to change the playback rate.

> **Note** Speed Control is an optional feature. This method makes it possible to allow users to adjust the playback rate, from 0.1 of the original speed to 4x speed, by changing the value of the parameter play Rate. For example, to play content at half-speed, play Rate should be set to 0.5

This method doesn’t work if it is called when NexPlayer is stopped.

**Parameters**

| Name  | Description  | 
|---|---|
| playRate | This float represents the rate by which to change the playback rate. It must be in the range of 0.1 to 4.0, which adjusts the playback speed from 0.1x to 4x the original speed of the content with HW decoder. It must be in the range of 0.1 to 2.0, which adjusts the playback speed from 0.1x to 2x the original speed of the content with SW decoder. It must be in the range of 0.5 to 2.0, when you use AirPlay mode. (isAirPlayActive is YES) |

> **Warning** When using this method with HLS or Smooth Streaming content, playing multitrack content may cause unstable performance. Therefore, playing content as a single track is encouraged. When using this method with Live content, beffering may occur more frequently.

#### - (NXError) setProperty: (NXProperty)propertytoValue:(NSInteger)value

Sets the value of a NexPlayer property.

See Properties for details.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | property | Identifies the property to be changed. |
| in | value | The new value for the property.

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) setProperty: (NXProperty)propertyvalue:(NSObject ∗ )value

Sets the value of a NexPlayer property.

See Properties for details.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | property | Identifies the property to be changed. |
|in | value | The new value for the property. |

**Returns**

NXErrorNone if successful, or another value in case of failure.

#### - (NXError) setUserCookie: (NSString ∗ )strCookie

This method sets a user cookie to be used while playing content.

In prior versions of the NexPlayer SDK, it was only possible to set a user cookie before content was opened in the player but this method makes it possible to set a cookie while content is playing. The cookie set with this method may also be different than an initial cookie set.

**Parameters**

| Name  | Description  | 
|---|---|
| strCookie | The user cookie to set, as a String. |

**Returns**

Zero if successful, non-zero if there was an error.

####  - (NXError) setVideoBitrates: (NSUInteger ∗ )bitrateslen:(NSInteger)lenwithOption:(NexAvailableBitrate)option

This method allows specific subtracks to be selected and played based on the bitrates of the tracks in HLS content.

Only the tracks with the bitrates passed on this method with the parameter bitrates will be played by NexPlayer. However, choosing a different option with the parameter option allows NexPlayer to choose and play the selected subtracks based on the passed bitrates differently.


**Parameters**

| Name  | Description  | 
|---|---|
| bitrates | The bitrates of the HLS content subtracks to play, as an integer array. |
| option | How HLS subtracks should be played based on the bitrates selected in bitrates. This will be one of: <br> - **NexAvailableBitrateNone:** No restriction on subtracks other than the bitrates selected in bitrates. <br> - **NexAvailableBitrateMatch** Only use subtracks which have exact same bitrate as the selected bitrates passed in bitrates. <br> - **NexAvailableBitrateNearest:** Only use subtracks which have the nearest bitrates to the target bitrates described in the list passed in bitrates. For example, if the target bitrates passed are [300K, 600K] and the HLS playlist includes 100K, 200K, 500K, 700K tracks, only the 200K (close to 300K) and 500K (close to 600K) tracks will be used. <br> - **NexAvailableBitrateHigh:** Only use subtracks which have bitrates equal to or higher than the target bitrate. The first bitrate in the list passed in bitrates is the target bitrate, the rest will be ignored. <br> - **NexAvailableBitrateLow:** Only use subtracks which have bitrates equal to or lower than the target bitrate. The first bitrate in the list passed in bitrates is the target bitrate, the rest will be ignored. <br> - **NexAvailableBitrateInsideRange:** Only use subtracks which have bitrates inside the range defined by the bitrates passed in bitrates. The first bitrate in the list is taken as the lower boundary, the second as the upper boundary, and the rest of the list will be ignored. Subtracks with bitrates between the lower and upper boundaries will be used.

**Returns**

Zero if successful, non-zero if there was an error.


#### - (NXError) setVideoStream: (NXMediaStreamInfo ∗)videoStreamaudioStream:(NXMediaStreamInfo ∗)audioStreamtextStream:(NXMediaStreamInfo ∗)textStreamtrackAttributes:(NSDictionary ∗)trackAttr

For media with multiple streams, selects the streams that will be presented to the user.
The full list of available streams (if any) can be found in the `NXContentInfo::streams` member in `NXPlayer::contentInfo`.
Each stream listed in the array in content information is either an audio stream or a video stream. One stream of
each type may be selected for presentation to the user.
There can be multiple tracks associated with each stream, providing different levels of quality. The player switches
among these strings as necessary to provide the best possibly quality for the available bandwidth.

**Custom Attributes**

In addition to providing different levels of quality, the tracks associated with a video stream can also provide different types of content (for example, different camera angles). These tracks are labeled with custom attributes.

Custom attributes consist of key/value pairs, and zero or more may be associated with any given track. Each unique combination of custom attributes makes up one attribute set. The list of possible attribute sets available for a given stream can be found in `NXMediaStreamInfo::customAttrSets`.

You may limit the selection of tracks to only those that share a particular set of custom attributes by specifying the set of key/value pairs as an NSDictionary in the track Attr argument.

> **Note** This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::completedAsyncCmdSetMediaStreamWithResult: method of the delegate will be called (and the result argument will indicate success or failure).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | videoStream | The video stream to select. This may be any one of the elements of `NXContentInfo::streams` where `NXMediaStreamInfo::type` is NXMediaTypeVideo. Specify nil to leave the video stream unchanged. |
| in | audioStream | The audio stream to select. This may be any one of the elements of `NXContentInfo::streams` where `NXMediaStreamInfo::type` is NXMediaTypeAudio. Specify nil to leave the audio stream unchanged. |
| in | textStream | The text stream to select. This may be any one of the elements of NXContentInfo::streams where NXMediaStreamInfo::type is NXMediaTypeText. Specify nil to leave the text stream unchanged. |
| in | trackAttr | A dictionary specifying the custom attributes by which to select a video track within the stream. Only video tracks that match ALL specified attributes (both name and value) will be used. Names and values must all be given asNSString instances. Specify nil to use the first available combination of custom attributes (the first available attribute set) in the selected video stream. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicates success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) setVideoStream: (NXMediaStreamInfo ∗ )videoStreamaudioStream:(NXMediaStreamInfo ∗ )audioStreamtrackAttributes:(NSDictionary ∗ )trackAttr

Convenience function for setting audio and video streams.

This is a convenience function, and is equivalent to calling `setVideoStream:audioStream:textStream:trackAttributes:`
with text Stream specified as nil.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | videoStream | The video stream to select. |
| in | audioStream | The audio stream to select. |
| in | trackAttr | A dictionary specifying the custom attributes by which to select a video track within the stream. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure.

#### - (NXError) start

Begins playback of content from the beginning.

Content must have been opened with `open:mode:subtitles:transport:startAt:autoPlay:` (or one of the related convenience functions) and the open operation must have completed `(nexPlayer:completedAsyncCmdOpenWithResult:playbackType: (NXPlayerDelegate-p)` method of delegate called) before playback can be started.

If autoPlay was YES when the content was opened, playback will start automatically, and it is not necessary to call this method.

This is an asynchronous operation that completes in the background. When it is finished, the `nexPlayer:completedAsyncCmdStartWithResult:playbackType: (NXPlayerDelegate-p)` method of the delegate will be called (and the result argument will indicate success or failure).

Do not use this to resume paused content; use `resume` for that, instead.

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) startFromTime: (NXDuration)startTime

Begins playback of content from the specified time.

Content must have been opened with `open:mode:subtitles:transport:startAt:autoPlay:` (or one of the related convenience functions) and the open operation must have completed (`nexPlayer:completedAsyncCmdOpenWithResult:playbackType: (NXPlayerDelegate-p)` method of delegate called) before playback can be started.

If autoPlay was YES when the content was opened, playback will start automatically, and it is not necessary to call this method.

This is an asynchronous operation that completes in the background. When it is finished, the `nexPlayer:completedAsyncCmdStartWithResult:playbackType: (NXPlayerDelegate-p)` method of the delegate will be called (and the resultargument will indicate success or failure).

Do not use this to resume paused content; use `resume` for that, instead.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | startTime | The offset in milliseconds from the beginning of the content from which to start playing. |

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### - (NXError) stop

Stops playback of content.

Content must be in either the playing or paused state. If autoPlay was specified when the content was opened,
stopping the content will also cause it to automatically be closed.

This is an asynchronous operation that completes in the background. When it is finished, the `nexPlayer:completedAsyncCmdStopWithResult: (NXPlayerDelegate-p)` method of the delegate will be called (and the result argument will indicate success or failure).

**Returns**

NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicate success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.

#### + (BOOL) useAVPlayerForAirPlay

Get the value for using native AV player for AirPlay internally.

**Returns**

The result value.

- YES: use airplay internally
- NO: don’t use airplay internally (default)

#### - (id < NXAsfPlayReadyDescrambler > ) asfPlayReadyDescrambler [read] , [write] , [nonatomic] ,[weak]

An object that conforms to `NXAsfPlayReadyDescrambler` that will handle PlayReady ASF descrambling.

> **Note** Like a delegate, this isnot retained.

If your application needs to descramble PlayReady encrypted ASF content before NexPlayer decodes and plays
that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXAsfPlayReadyDescrambler` for more information on how to implement a descrambler object of this type.
* `NXWMDRMDescrambler`
* `NXDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* NXRemoteFileIOInterface

#### - (BOOL) backgroundMode [read] , [write] , [nonatomic] , [assign]

Set Enable/Disable playback in background. It is strongly recommended for audio only channel.

> **Note** If you want to use this option, you should set the capability of your Application as follows: App target -> capabilities ->Background Modes (On) ->Audio, AirPlay and Picture in Picture (check)

**Values**

- YES: The player plays current content continuously although App is running in background.
- NO: The player stops or pauses when App is running in background.

#### - (float) brightnessAdjustment [read] , [write] , [nonatomic] , [assign]

Adjusts the brightness of video being played.

This property may be set to a value between -1.0 and +1.0, where -1.0 represents the darkest the video can be displayed, and +1.0 represents the brightest the video can be displayed. This may property may be provided in an application UI to allow users to adjust this setting directly.

The default value for this property is 0.0 which is the original brightness of the video.

> **Note** Setting value to this property has no effect when the video toolbox hardware accelerated decoding service is used.

#### - (id < NXPlayerCEA608CaptionUpdateReceiver > ) CEA608CaptionUpdateReceiver [read] , [write] ,[nonatomic] , [weak]

Specifies a receiver to be notified of changes to the current CEA 608 closed caption information.

> **CAUTION:** This is automatically set by `NXPlayerView`, and should not be changed for `NXPlayer` instances that are connected to `NXPlayerView` instances.

Normally, the `nexPlayer:updatedCaption:forCEA608Channel:` method of the delegate should be
used instead. This is useful for cases such as `NXPlayerView`, where the size of the player view (and matching `NXCEA608CaptionView`) is being managed by something other than the delegate.

#### - (NXContentInfo ∗ ) contentInfo [read] , [nonatomic] , [assign]

Contains information on the content that is currently playing.

See the `NXContentInfo` class for details on the information that is available.

The first time that content information becomes available, and any time there after that the content information has been updated, the `nexPlayerDidUpdateContentInfo: (NXPlayerDelegate-p)` method will be called on the delegate.

In addition, when the asynchronous open command has completed and the `nexPlayer:completedAsyncCmdOpenWithResult:playbackType: (NXPlayerDelegate-p)` method on the delegate is called, content information will be available (unless the open command failed).

The content info object is re-created any time that the content information is updated (the object is never updated in-place). If the application has retained a previous content information object, that older object will remain valid (albeit obsolete) until the application releases it.

#### - (id < NXPlayerContentInfoUpdateReceiver > ) contentInfoUpdateReceiver [read] , [write] ,[nonatomic] , [weak]

Specifies a receiver to be notified of changes to the current content information.

> **CAUTION:** This is automatically set by NXPlayerView, and should not be changed for NXPlayer instances that are connected to NXPlayerView instances.

Normally, the `nexPlayerDidUpdateContentInfo:` method of the delegate should be used instead. This
is useful for cases such as `NXPlayerView`, where the size of the player view is being managed by something other than the delegate.

#### - (float) contrastAdjustment [read] , [write] , [nonatomic] , [assign]

Adjusts the contrast of video being displayed.

This property may be set to a value between -1.0 and +1.0, where -1.0 represents the lowest contrast at which the video can be displayed, (essentially a grey screen) and +1.0 represents the highest contrast at which the video can be displayed. This may property may be provided in an application UI to allow users to adjust this setting directly.

The default value for this property is 0.0 which is the original contrast of the video.

> **Note** Setting value to this property has no effect when the video toolbox hardware accelerated decoding service is used.

#### - (NXDuration) currentTimeStamp [read] , [nonatomic] , [assign]

The current playback position, in milliseconds.

For local and streaming on-demand content, this is the number of milliseconds from the beginning of the content.

For live streaming content, this is the number of milliseconds from the seek base.

#### - (id < NXDashDRMSessionDelegate > ) dashDRMSessionDelegate [read] , [write] , [nonatomic] , [weak]

For internal use only. Please do not use.

#### - (id < NXDeceUVDescrambler > ) deceUVDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to NXDeceUVDescrambler that will handle DECE UV(Ultra Violet) descrambling.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble DECE UV encrypted content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXDeceUVDescrambler` for more information on how to implement a descrambler object of this type.
* `NXWMDRMDescrambler`
* `NXDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXAsfPlayReadyDescrambler`
* `NXRemoteFileIOInterface`


#### - (id < NXPlayerDelegate > ) delegate [read] , [write] , [nonatomic] , [weak]

The delegate for the NXPlayer instance.

The delegate receives all of the notifications about events that occur during playback. For example, if you wish to perform an action when the content has finished playing, you would do that by setting a delegate.

Any object may serve as a delegate, as long as it implements the NXPlayerDelegate protocol. Generally, the view controller that owns the player view also serves as the delegate. The delegate should provide a method for any event it wishes to handle.

**See Also**

`NXPlayerDelegate` for details on events that can be captured

#### - (id < NXDRMDescrambler > ) DRMDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to NXDRMDescrambler that will handle DRM descrambling.

**Note**

Like a delegate, this is not retained.

If your application needs to descramble DRM encrypted content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXDRMDescrambler` for more information on how to implement a descrambler object of this type.
* `NXWMDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`

#### - (id < NXDynamicThumbnailDelegate > ) dynamicThumbnailDelegate [read] , [write] , [nonatomic] , [assign]

The delegate for the Dynamic Thumbnail feature in NexPlayer.

Any application that will handle Dynamic Thumbnail must implement this property.

#### - (float) gain [read] , [write] , [nonatomic] , [assign]

NexPlayer’s output volume (gain).

This property can be adjusted to modify the output volume of the player. This affects the output of the player before it is mixed with other sounds. Normally, this should be left at the default setting of 1.0, and the volume should be controlled by the user via the hardware buttons on the device. However, if the application contains multiple audio sources (or if there is other audio being played on the device), this property can be used to reduce the NexPlayer volume in relation to other sounds.

The valid range for this property is 0.0∼1.0. A value of 0.0 will silence the output of the player, and a value of 1.0 (the default) plays the audio at the original level, affected only by the device master volume setting (controlled by the hardware buttons).

Do not use this setting for volume controlled by the user. Instead, use the MPVolumeView class provided by iOS, in order to conform to the iOS Human Interface Guidelines. The MPVolumeView provides a volume slider that controls the device master volume (the same volume adjusted by the hardware volume buttons) and allows the user to select the output destination for the audio (the audio route) if multiple output devices are available.

#### - (id < NXHLSAES128Descrambler > ) hlsAESDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXHLSAES128Descrambler` that will handle descrambling of HLS AES128 encrypted content.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble HLS AES128 encrypted content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXHLSAES128Descrambler` for more information on how to implement a descrambler object of this type.
* `NXDeceUVDescrambler`
* `NXWMDRMDescrambler`
* `NXDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXAsfPlayReadyDescrambler`
* `NXRemoteFileIOInterface`


#### - (id < NXHLSTSDescrambler > ) HLSTSDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXHLSTSDescrambler` that will handle descrambling of HTTP Live Streaming TS segments.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble HTTP Live Streaming TS segments before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXHLSTSDescrambler` for more information on how to implement a descrambler object of this type.
* `NXDRMDescrambler`
* `NXWMDRMDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`

#### - (id < NXHTTPCredentialsProvider > ) HTTPCredentialsProvider [read] , [write] , [nonatomic] , [weak]

An object that will handle requests for HTTP credentials.

Whenever NexPlayer receives an HTTP 401 or 407 response during streaming play, it calls the appropriate method of `NXHTTPCredentialsProvider` to get additional HTTP headers to use when retrying the failed request.

This is an opportunity to add, for example, authentication credentials such as a user name or password.

#### - (id < NXHTTPRetrieveDelegate > ) httpRetrieveDelegate [read] , [write] , [nonatomic] , [weak]

The delegate for the retrieval and offline playback of HLS content stored with NexPlayer.

Any application that will handle retrieval of HLS content stored for offline playback must implement this property.

#### - (id < NXHTTPStoreDelegate > ) httpStoreDelegate [read] , [write] , [nonatomic] , [weak]

The delegate for the HLS offline storage feature in NexPlayer.

Any application that will handle HLS offline storage must implement this property.

#### - (BOOL) isAirPlayActive** [read] ,[nonatomic] , [assign]

Check whether AirPlay is active.

> **Note** This SDK use AVPlayer internally for AirPlay. Return Value is AVPlayer.isExternalPlaybackActive.

#### - (id < NXManifestAndPlaylistDescrambler > ) manifestAndPlaylistDescrambler [read] , [write] ,[nonatomic] , [weak]

An object that conforms to NXManifestAndPlaylistDescrambler that will handle manifest and playlist descrambling.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble manifests and/or playlists before NexPlayer processes them, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to process playlist or manifest contents.

**See Also**

`NXManifestAndPlaylistDescrambler` for more information on how to implement a descrambler object of this
type.


#### - (id < NXPDBlockDescrambler > ) PDBlockDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXPDBlockDescrambler` that will handle descrambling of Progressive Download content.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble blocks of Progressive Download before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXPDBlockDescrambler` for more information on how to implement a descrambler object of this type.
* `NXWMDRMDescrambler`
* `NXDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`

#### - (id < NXPiffPlayReadyDescrambler > ) piffPlayReadyDescrambler [read] , [write] , [nonatomic] ,[weak]

An object that conforms to `NXPiffPlayReadyDescrambler` that will handle descrambling of Piff PlayReady content.

**Note**

Like a delegate, this is not retained.

If your application needs to descramble Piff PlayReady content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXPiffPlayReadyDescrambler` for more information on how to implement a descrambler object of this type.
* `NXDRMDescrambler`
* `NXWMDRMDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`
* `NXSmoothStreamFragmentDescrambler`

#### - (id < NXRemoteFileIOInterface > ) remoteFileIOInterface [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXRemoteFileIOInterface` that will handle file input and output.

> **Note** Like a delegate, this is not retained.

If your are playing back local content that is not available via the standard operating system file APIs, you can provide your own replacement functions which NexPlayer will use for opening and reading your file.

These replacement functions are provided as methods of a class that the application provides.

**See Also**

* `NXRemoteFileIOInterface` for more information on how to implement a class that replaces that standard file input and output functions.
* `NXDRMDescrambler`
* `NXWMDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXAsfPlayReadyDescrambler`

#### - (CAEAGLLayer ∗ ) renderLayer [read] , [write] , [nonatomic] , [weak]

This is the CAEAGLLayer (a layer supporting OpenGLES rendering) that the player will render video into.

> **Note** If you are using NXPlayerView, this will have been automatically set, and should not be changed.

If you are using your own UIView subclass, the CAEAGLLayer from that subclass must be assigned here so that the player can access it to render video output.

This should be set when NXPlayer is initially created, and before opening any content. This may be changed later as long as no content is currently playing at the time.

You must call prepareVideoBuffers once after assigning the render layer, and again any time the dimensions of the render layer have changed.

> **Warning** Changing this during playback will have unpredictable results.

**See Also**

- `prepareVideoBuffers`

#### (NSString ∗ ) SDKName [read], [nonatomic], [assign]

The name of the current SDK.

This property provides the current name of the SDK in use, which may be helpful in debugging or if multiple versions of the SDK have be used.


#### - (NSUInteger) seekableLength [read] , [nonatomic] , [assign]

The current seekable length.

If content is seekable, this property provides the length of the portion of the content that is seekable. While this will be the entire length of a local seekable file, or the downloaded portion of a progressively downloaded file, this value may also be used with seekBaseto determine which portion of a live stream is within the seekable window.

For more information, please see the introductory section on server-side timeshifting.

#### - (uint64_t) seekBase [read] , [nonatomic] , [assign]

The current seek base.

If content is seekable, this indicates the beginning of the portion of content where seek can be performed. For local and progressive download content, this will be zero, but in the case of live content, this will be a constantly shifting value that indicates the start of the "seekable window" within the live content. The end of the seekable window can be determined using the property seekable Length.

These two properties allow live content to be timeshifted based on the amount of content available on the server.

See `nexPlayer:seekableStateChangedTo:seekBase:seekableLength: (NXPlayerDelegate-p)` for additional information.

#### - (BOOL) seeking [read] , [nonatomic] , [assign]

Indicates if the player is currently in a seek operation.

Note that during seek operations, the player is automatically placed in a paused state.

**Values**

- YES if the player is seeking.
- NO if the player is not seeking.

#### - (NXCEA608Channel) selectedCEA608Channel [read] , [write] , [nonatomic] , [assign]

Selects the channel to use to receive CEA 608 closed captions.

The default setting is `NXCEA608Channel_None` which indicates no channel is selected and the captions are turned off or disabled.

These channels offer different caption information for the same content, often different language captions which could be selected by the user of the application if desired.

Other values are `NXCEA608Channel_Ch1`, `NXCEA608Channel_Ch2`, `NXCEA608Channel_Ch3`, and `NXCEA608Channel_Ch4`, but channels 1 and 3 are the most commonly used.

**See Also**

`NXCEA608Caption`

#### - (id < NXSmoothStreamFragmentDescrambler > ) smoothStreamFragmentDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXSmoothStreamFragmentDescrambler` that will handle descrambling of Smooth Streaming fragments.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble fragments of encrypted Smooth Streaming content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* NXSmoothStreamFragmentDescrambler for more information on how to implement a descrambler object of this type.
* NXDRMDescrambler
* NXWMDRMDescrambler
* NXRemoteFileIOInterface
* NXAsfPlayReadyDescrambler

#### - (id < NXSmoothStreamPlayReadyDescrambler > ) smoothStreamPlayReadyDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXSmoothStreamPlayReadyDescrambler` that will handle descrambling of Smooth
Streaming PlayReady content.

> **Note** Like a delegate, this is not retained.

If your application needs to descramble Smooth Streaming PlayReady content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXSmoothStreamPlayReadyDescrambler` for more information on how to implement a descrambler object of this type.
* `NXDRMDescrambler`
* `NXWMDRMDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`

####  - (NXPlayerState) state [read] , [nonatomic] , [assign]

The current state of the player (paused, stopped, etc.)

**See Also**

`NXPlayerState` for possible values.

####  - (NXPlayerState) stateBeforeSeek [read] , [nonatomic] , [assign]

Indicates the player status before seeking.

When seeking, NXPlayerState will be set (NXPlayerStatePause ->seek action ->NXPlayerStatePlay) internally.
So, this property keeps the original (before seek action) NXPlayerState.

This property is only valid when (BOOL)seeking is TRUE. ex) In the `nexPlayer:completedAsyncCmdSeekWithResult:`

#### - (NXStatsInfo ∗ ) statsInfo [read] , [nonatomic] , [assign]

Retrieves statistical information about how content is currently being handled by NexPlayer.

If statistics like the rate of video frames being dropped or of frames being rendered are desired, this property can be used to retrieve the FPS (frames per second) for short intervals (about 2 seconds) of content, as well as the total number of decoded video frames and the number of frames rendered during that interval of content.

**See Also**

NXStatsInfo

#### - (NSArray ∗ ) subtitleTracks [read] , [nonatomic] , [assign]

Available subtitle tracks.

This is an array of NXSubtitleTrack instances listing all of the available caption languages for the currently open content.

Note that this is not the same as the text track associated with streaming content. Although the two have a similar end result, functionally they are different and are implemented with different mechanisms. For streaming content, the text track is selected with setVideoStream:audioStream:textStream:trackAttributes:

At present, the only way to make caption languages available is to specify a subtitle file when opening the content.

Subtitle tracks may be turned on and off individually; it is possible to turn on multiple subtitle tracks at the same time.

For example, to turn on all subtitle tracks:

```
for( NXSubtitleTrack *track in hNexPlayer.subtitleTracks ) {
	track.enabled = YES;
}
```

To turn off all subtitle tracks:

```
for( NXSubtitleTrack *track in hNexPlayer.subtitleTracks ) {
	track.enabled = NO;
}
```

Each track has a variety of additional data associated with it, including a track name, language, and dictionary of metadata. It is important to note that track name and language are not available for all subtitle formats; in some cases, the track number (as an index in the subtitleTracks array) is the only identification available, especially for formats that only support one track.

For SMI subtitle files, the SMI class name is provided in the metadata for each track.

The default behavior, if an `NXSubtitleTrack` is displayed as a string (using `[NSString stringWithFormat:@"%@", subtitleTrack]`) is to display the name, and if the name is not available, the language. If neither are available, the SMI class name
is used. If none of those are available "Subtitle Track N" is used, where N is the 1-based index of the track.

Since SMI class names may be purely arbitrary, the best approach for an SMI file is to read the file itself and parse the header to determine the actual language information for each class name.

However, if this is not an option, another method is to heuristically check the string. Many SMI files follow an ad-hoc standard of naming classes using the format:

- (language)(country)(type)

where each of these fields is a two-character uppercase code, and country may be omitted. For example:

- ENUSCC English, United State, Closed Caption
- KRCC Korean, Closed Caption
- FRFRCCFrench, France, Closed Caption

Therefore, it is possible to check if the language string is a 4- or 6-letter uppercase code, and if so, to parse it for language and country. The language generally an ISO 639 short (two-character) language code, and the country is generally an ISO 3166-1 two-character country code.

Since the exact heuristics that will be suitable for a given application depend on the needs of the application, NexPlayer simply provides the raw language string and does not attempt to interpret it in any way.

If a given string is not recognized by the application, it is generally best to fall back to displaying the raw string.

#### - (id < NXWMDRMDescrambler > ) WMDRMDescrambler [read] , [write] , [nonatomic] , [weak]

An object that conforms to `NXWMDRMDescrambler` that will handle WM-DRM descrambling.

> **Note** Like a delegate, this isnot retained.

If your application needs to descramble WM-DRM encrypted content before NexPlayer decodes and plays that content, you should define a class that handles the descrambling operation and assign an instance of that class to this property.

If there is an object assigned to this property, the player will call methods of that object to perform descrambling prior to attempting to decode the content for playback.

**See Also**

* `NXWMDRMDescrambler` for more information on how to implement a descrambler object of this type.
* `NXDRMDescrambler`
* `NXSmoothStreamFragmentDescrambler`
* `NXRemoteFileIOInterface`
* `NXAsfPlayReadyDescrambler`

### NXPlayerABRController Class Reference

This interface must be implemented in order for the application to set a minimum or maximum allowable bandwidth, or both, for playing streaming content.

#### - (NXError) changeBandwidthMin: (NSUInteger)minMax:(NSUInteger)max

This method sets the minimum and maximum bandwidth for streaming content in NexPlayer, dynamically during
playback.

**Warning**

To dynamically change the minimum and maximum bandwidth in the middle of playback, please use this
method. To take effect, this method should be called after calling open. Note that the minimum, and maximum bandwith can also be set before play begins by setting the properties, NXPropertyMinBW, with changeMinBandwidth. and NXPropertyMaxBW, with changeMaxBandwidth.

This applies in cases where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the minimum, and over the maximum bandwidth when determining whether a track change is appropriate, even if it detects less, and more bandwidth available.

Note that to remove a minimum and maximum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set both of min, and max to 0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| min | Minimum bandwidth in kbps (kilobits per second). To reset to no minimum bandwidth,min = 0x00000000.  |
| max | Maximum bandwidth in kbps (kilobits per second). To reset to no maximum bandwidth,max = 0x00000000. |

**Returns**

NXErrorNone for success, or a non-zero NexPlayer error code in the event of a failure.

#### - (NXError) changeMaxBandwidth: (NSUInteger)max

This method sets the maximum bandwidth for streaming content in NexPlayer, dynamically during playback.

> **Warning** To dynamically change the maximum bandwidth in the middle of playback, please use this method. To take effect, this method should be called after calling open. Note that the maximum bandwith can also be set before play begins by setting the `NXProperty,NXPropertyMaxBW`, with `changeMaxBandwidth`.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track over the maximum bandwidth when determining whether a track change is appropriate, even if it detects more bandwidth available.

Note that to remove a maximum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set max to 0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| max | Maximum bandwidth in kbps (kilo bits per second). To reset to no maximum bandwidth, set max= 0x00000000. |

**Returns**

NXErrorNone for success, or a non-zero NexPlayer error code in the event of a failure.

####  - (NXError) changeMinBandwidth: (NSUInteger)min

This method sets the minimum bandwidth for streaming content in NexPlayer, dynamically during playback.

**Warning**

To dynamically change the minimum bandwidth in the middle of playback, please use this method. To take effect, this method should be called after callin gopen. Note that the minimum bandwith can also be set before play begins by setting the `NXProperty,NXPropertyMinBW`, with `changeMinBandwidth`.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the minimum bandwidth when determining whether a track change is appropriate, even if it detects less bandwidth available.

Note that to remove a minimum that has been set with this method (so that NexPlayer will again consider all tracks regardless of bandwidth), set min to0x00000000.

**Parameters**

| Name  | Description  | 
|---|---|
| min | Minimum bandwidth in kbps (kilo bits per second). To reset to no minimum bandwidth, set min= 0x00000000.|

**Returns**

NXErrorNone if successful, otherwise nil if there was an error.

#### - (NXError) setABREnabled: (BOOL)enabled

This method sets whether or not ABR methods should be used.

In general, NexPlayer plays streaming content, including content with multiple tracks at different bandwidths such as HLS, by choosing the optimal track according to network conditions and device performance. This is the default behavior of NexPlayer and this occurs when ABR is enabled (or calling `NXPlayerABRController::setABREnabled` with the parameter enabled set to YES).

However, there may be instances when an application may want to set limits on which tracks should be selected and played by NexPlayer in order to provide a specific user experience, and to force NexPlayer to stay on a particular bandwidth track, regardless of network conditions. In cases like this, in order to keep playing a track at a target bandwidth (set with `NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption:`) this method must be called to disable NexPlayer’s ABR behavior (with the parameter enabled set to NO).

> **Warning** This method must be called with enabled set to NO before calling NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption: if the application should continue playing the target bandwidth regardless of network conditions.

**Parameters**

| Name  | Description  | 
|---|---|
| enabled |- **YES** : ABR enabled. NexPlayer will handle track changes automatically. <br>- **NO** : ABR disabled. NexPlayer will continue playing the target bandwidth track set, regardless of network conditions.

**Returns**

NXErrorNone if successful, otherwise non-zero if there was an error.

**See Also**

`NXPlayerABRController::setTargetBandWidth:withSegmentOption:withTargetOption:`


#### - (NXError) setTargetBandwidth: (NSUInteger)targetBwBpssegmentOption:(NexBandwidthSegmentOption)segOptiontargetOption:(NexBandwidthTargetOption)targetOption

This method sets the target bandwidth for streaming playback dynamically during playback.

This applies in cases with content where there are multiple tracks at different bandwidths (such as in the case of HLS). The player will not consider any track under the target bandwidth and over the target bandwidth when determining whether a track change is appropriate, even if it detects less and more bandwidth available.

**Parameters**

| Name  | Description  | 
|---|---|
| targetBwBps | Target bandwidth in bps (bits per second). |
| segOption | One of the following NexBandwidthSegmentOption values, indicating how to handle buffered content when the track changes: <br> - **NexBandwidthSegmentOptionDefault = 0** : Default (NexPlayer will decide between NexBandwidthSegmentOptionQuickMix (changing tracks quickly) and NexBandwidthSegmentOptionLateMix (playing buffered content and changing tracks more slowly)). <br> -**NexBandwidthSegmentOptionQuickMix = 1** : NexPlayer will clear the buffer as much as possible and will start to download new track so user can see a new track faster. <br>- **NexBandwidthSegmentOptionLateMix = 2** : NexPlayer will preserve and play the content segments already buffered and will download a new track.
| targetOption | How to use the target bandwidth value set. One of the following NexBandwidthTargetOption options: <br>- **NexBandwidthTargetOptionDefault = 0** : Default target option (NexBandwidthTargetOptionBelow). <br>- **NexBandwidthTargetOptionBelow = 1** : Select a track with a bandwidth below the target bandwidth. <br>- **NexBandwidthTargetOptionAbove = 2** : Select a track with a bandwidth above the target bandwidth. <br>- **NexBandwidthTargetOptionMatch = 3** : Select the track that has a bandwidth that matches the target set; otherwise send an error and no new target bandwidth is selected.

> **Warning** This method should be called after open: (NXPlayer).

**Returns**

NXErrorNone if successful, otherwise non-zero if there was an error.

**See Also**

- `setABREnabled:`

### NXPlayerABRControllerTrackChangeParams Struct Reference

Bandwidth information for ABRControl.

This structure is used by `NXABRDelegate` protocol to control ABR track switch and it includes bandwidth information.

**Public Attributes**

- NSUInteger `netBW`
    The current network bandwidth.
- NSUInteger `curTrackBW`
    The current track bandwidth.
- NSUInteger `nextTrackBW`
    The target track bandwidth.


### NXPlayerCallbackDelegate Protocol Reference

Inheritance diagram for<NXPlayerCallbackDelegate>:

`<NXPlayerGetKeyExtDelegate>` -> `<NXPlayerCallbackDelegate>` -> `<NSObject>` 

### NXPlayerCEA608CaptionUpdateReceiver Protocol Reference

This protocol must be adopted and implemented to support and display CEA 608 closed captions in content.

Whenever CEA 608 closed caption information is updated and new caption information is ready, this protocol will be used to receive the updated information event.

For more information about CEA 608 closed captions, please see `NXCEA608Caption`.

#### (void) nexPlayer: (NXPlayer ∗)nxplayerupdatedCaption:(NXCEA608Caption ∗ )caption forCEA608Channel:(NXCEA608Channel)channel

This method receives the updated caption information for content with CEA 608 closed captions.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The calling NexPlayer instance. |
| in | caption | The new caption information to display (see `NXCEA608Caption` for details).
| | channel | The channel from which the caption information was received. (see NXTypes::NXCEA608Channel and NXPlayer::selectedCEA608Channel for more information).


### NXPlayerContentInfoUpdateReceiver Protocol Reference

This protocol must be adopted and implemented by the player to receive updates to content information as content is played back.

It will be used each time information about the playing content changes, for example when a track or stream changes.

For more details about the recorded information of the current content, please see NXContentInfo.

#### (void) nexPlayerDidUpdateContentInfo: (id)nxplayer

Sent when content information is updated.

This event is sent whenever content information changes and is updated for the associated instance of NexPlayer.

**Parameters**

| Name  | Description  | 
|---|---|
| nxplayer | The instance of NexPlayer where content information changed. |

### NXPlayerDelegate Protocol Reference

Delegate protocol for `NXPlayer`.

Any class that will receive events from a `NXPlayer` instance as a delegate should implement this protocol.

All methods are optional; implement the methods for events which you wish the delegate to handle.

NXPlayerDelegate::nexPlayer:willBeSentEvent:withArgs: is a special method that can be used to trap all events, and which can filter events before they are passed to other event handling methods.

Use specific event handling methods if you need to respond to a specific event. For example, if you wish to issue a play command when the content has been successfully opened, you might implement `nexPlayer:completedAsyncCmdOpenWithResult:playbackType: (NXPlayerDelegate-p)` as follows:

```objc
- (void) nexPlayer:(NXPlayer*)nxplayer completedAsyncCmdOpenWithResult:(
    	NXError)result playbackType:(NXPlaybackType)type {
	[m_playerView.player start];
}
```

Use the general event handling method if you need to respond to a large group of events (or all events) in an identical way. For example, if you wish to note every event that occurs in the log, you might implement NXPlayerDelegate::nexPlayer:willBeSentEvent:withArgs:.

```objc
- (BOOL) nexPlayer:(NXPlayer*)nxplayer willBeSentEvent:(NSString*)selectorName withArgs:(NSArray
    *)args {
	NSArray*el = [selectorName componentsSeparatedByString:@":"];
	NSMutableString*output = [NSMutableString string];
	for( int i=0; i<[el count]; i++ ) {
		if( [[el objectAtIndex:i] length] < 1 )
			continue;
		if( i>=[args count] )
			[output appendFormat:@"%@:? ", [el objectAtIndex:i], nil ];
		else
			[output appendFormat:@"%@:%@ ", [el objectAtIndex:i], [args objectAtIndex:i], nil ];
	}
	NSLog(@"NEXPLAYER EVENT: %@\n", output);
	return YES;
}
```

#### (void) nexPlayer: (NXPlayer ∗ )nxplayerbufferingProgress:(NSInteger)percent

Buffering has progressed and the percentage complete has changed.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | percent | The percentage (an integer from 0 to 100) of the required amount of data that has been buffered. |

**See Also**

- `nexPlayerDidBeginBuffering:` for more information

#### (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdMediaOnOffWithResult:(NXError)result mediaType:(NXMediaType)mediaTypebOnOff:(BOOL)bOnOff

An asynchronous media on/off operation has completed.

This method is called when the media on/off operation initiated by `setMediaOnOff:mediaType: (NXPlayer)` has
completed.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | result | The result of the asynchronous operation (NXErrorNone for success, or a nonzero NXError code in the event of a failure). |
| in | mediaType | The mediaType to disable or enable. The method uses NXMediaType and values below only are valid. NXMediaTypeAudio NXMediaTypeVideo NXMediaTypeText |
| in | bOnOff | if you want to disable the media, set to NO. if you want to enable the media, set to YES. | 

**See Also**

- `setMediaOnOff:mediaType: (NXPlayer)`

#### (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdOpenWithResult:(NXError)result playbackType:(NXPlaybackType)type

An asynchronous open operation has completed.

This method is called when an open operation started by `open:mode:subtitles:transport:autoPlay: (NXPlayer)` (or one of the related convenience functions) has completed.

If autoPlay was set to YES when the open command was issued, the player will automatically call `start (NXPlayer)` to begin playback; otherwise, the delegate will need to start playback explicitly by calling that same method.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |
| in | type | The type of content; one of: <br> - NXPlaybackTypeLocal <br> - NXPlaybackTypeStreaming |

**See Also**

- `open:mode:subtitles:transport:autoPlay: (NXPlayer)`, the method starting the open operations that calls this method when they complete.

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdPauseWithResult:(NXError)result

An asynchronous *pause* operation has completed.

This method is called when the pause operation initiated by `pause (NXPlayer)` has completed.

> **Note** If you call `pause (NXPlayer)` during a seek operation, no pause command is actually issued. Rather, the seek operation that is in progress is modified to leave the player in a paused state upon completion. In this case, because the pause command is not actually issued, no completion event will occur. You can detect this case by checking the value of `NXPlayer::seeking` just before calling `pause (NXPlayer)`.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdResumeWithResult:(NXError)result

An asynchronous *resume* operation has completed.

This method is called when the resume operation initiated by `resume (NXPlayer)` has completed.

**Note** If you call `resume (NXPlayer)` during a seek operation, no resume command actually issued. Rather, the seek operation that is in progress is modified to leave the player in a playing state upon completion. In this case, because the resume command is not actually issued, no completion event will occur. You can detect this case by checking the value of `NXPlayer::seeking` just before calling `resume (NXPlayer)`.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdSeekWithResult:(NXError)result

An asynchronous *seek* operation has completed.

This method is called when the seek operation initiated by NXPlayer::seek has completed.

> **Note** If you call seekTo: (NXPlayer) while a seek operation is already in progress, it just modifies the target of the current seek operation. No new seek operation is started, and therefore, only one single completion event will be generated.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |

####  - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdSetExternalSubtitleWithResult:(NXError)result

An asynchronous *forward* operation has completed.

> **Deprecated** There is currently no API in the NexPlayer iOS SDK that implements theforwardcommand, and this event can therefore never occur. It may be supported in future versions, so you should not write code
> that processes this event at present (otherwise that code may break in the future).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). An asynchronous backwards operation has completed. |

> **Deprecated** There is currently no API in the NexPlayer iOS SDK that implements thebackwardscommand, and this event can therefore never occur. It may be supported in future versions, so you should not write code that processes this event at present (otherwise that code may break in the future).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). An asynchronous `setExternalSubtitle` operation has completed.

This method is called when the pause operation initiated by NXPlayer::setExternalSubtitle has completed.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | result | The result of the asynchronous operation (NXErrorNone for success, or a nonzero NXError code in the event of a failure). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdSetMediaStreamWithResult:(NXError)result streamInfo:(NXMediaStreamInfo ∗ )stream

An asynchronous media stream switching operation has completed.

This method is called when the media stream switching operation initiated by setVideoStream:audioStream:textStream:trackAttributes: (NXPlayer) or setVideoStream:audioStream:trackAttributes: (NXPlayer) has completed.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | result | The result of the asynchronous operation (NXErrorNone for success, or a non-zero NXError code in the event of a failure). |
| in | stream | The new stream of NXContentInfo.

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdStartWithResult:(NXError)result playbackType:(NXPlaybackType)type

An asynchronous *start* operation has completed.

This method is called when playback has started (or failed irrecoverably) after a call to start (NXPlayer).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |
| in | type | The type of content; one of: <br> - NXPlaybackTypeLocal <br> - NXPlaybackTypeStreaming |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayercompletedAsyncCmdStopWithResult:(NXError)result

An asynchronous *stop* operation has completed.

This method is called when the stop operation initiated by stop (NXPlayer) has completed.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | result | The result of the asynchronous operation (zero if the operation succeeded, or a non-zero NXError code if the operation failed due to an error). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdebugMessage:(NSString ∗ )messagecategory:(NXDebugMsgCat) category

Provides debugging and diagnostic information during playback.

The information provided here is for debugging purposes only; the contents of the strings provided may change in future versions, so do not attempt to parse them or make programmatic decisions based on their contents. Also, do not make assumptions about line length or number of lines.

At present, the debugging messages generated relate to the RTSP/RTCP connection. Additional categories may
be added in the future.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | message | Debugging message |
| in | category | Message category; currently, one of: <br> - NXDebugMsgCat_RTSP <br> - NXDebugMsgCat_RTCP_RR_SEND <br> - NXDebugMsgCat_RTCP_BYE_RECV <br> - NXDebugMsgCat_ContentInfo

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdidChangeFromState:(NXPlayerState)oldState toState:(NXPlayerState)newState [optional]

General event handling method that is called before any specific method.

This can be used to filter events (return NO to prevent further processing of an event), to handle all events (for example, to log debugging information about events as they occur), or to handle a large group of events (in cases where it might be inconvenient to implement event-specific functions).

**Deprecated** This API will be removed from the next SDK version.(5.30.x) Please implement the methods for events which you wish the delegate to handle since all the methods are optional in NXPlayerDelegate.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | selectorName | The Objective-C selector for the event-specific method for this event (this is specified as a string rather than an actual selector; you can use NSSelectorFromString(selectorName). |
| in | args | An array of the arguments that would be passed to the event-specific method, in the same order as they appear in the selector. These are in the same format as the method arguments, except that numeric values such as integers have been replaced with NSNumber instances.

**Returns**

YES to continue processing normally (event will be sent to the event-specific method of the delegate) or NO to stop processing this event (event-specific method will not be called). General method called in addition to (and before) other event-specific methods if the state of the player (play, pause, stop) has changed.

This can be used to update the user interface to reflect the new state, such as by enabling or disabling pause and play buttons.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | oldState | The previous player state (see NXPlayerState for details). |
| in | newState | The new player state (see NXPlayerState for details). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdidDownloadSoFar (NSUInteger)downloadedBytestotalSize:(NSUInteger) totalSize

The player is downloading content, and the download has progressed.

This event provides status updates on the number of bytes downloaded so that applications can display that information in the user interface.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | downloadedBytes | The number of bytes downloaded so far. |
| in | totalSize | The total number of bytes in the file to be downloaded. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdidReceiveInformativeEvent:(NexInformativeEvent)event details:(NSDictionary ∗ )details

This method delivers an informative event such as NexInformativeEventDownloadBegan.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | TheNXPlayerinstance that generated the event. |
| in | event | The informative event. |
| in | details | Dictionary contains parameters for the event, if available. See NexInformativeEventfor details. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdidReceiveSessionData:(NSMutableArray ∗ )sessionDataArr

This method reports the arbitrary session data of the HLS master playlist.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | TheNXPlayerinstance that generated the event. |
| in | sessionDataArr | The array of NexSessionData object that includes the arbitrary session data of the HLS master playlist. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerdidUpdateDownloadProgressWithFileCount:(NSUInteger)current totalFileCount:(NSUInteger)total

This method provides the download progress for Offline Playback.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | TheNXPlayerinstance that generated the event. |
| in | current | Current file count. |
| in | total | Total File count. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerencounteredError:(NXError)errorCode

An error has occurred during playback.

If the delegate implements this method, it should respond to the error by stopping and closing the currently playing content (it can do this by simply calling `close (NXPlayer)`, which will automatically stop the content first).

An error message should also be displayed to the user.

If this method is not implemented by the delegate, the default behavior is to display a pop-up message with the error (using UIAlertView) and stop and close the current content.

> **Note** The pop-up error provided by default is very simple and is not localized. It is strongly recommended that you override this function and provide your own error display that is suited to your application.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event.
| in | errorCode | The error that has occurred. (See NXError for details). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayermediaTypeChangedTo:(NXMediaType)newType

The stream being played back has changed and the new stream has a different media type.

This event happens whenever the state changes between video-only, audio-only and audio-video.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | newType | The new media type (see NXMediaType). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayeronHTTPRequest:(NSString ∗ )strRequest

This method allows NexPlayer to pass HTTP request messages to an application.

While NexPlayer normally handles HTTP requests and responses internally, in cases where additional information is required from the server (for example user cookies), this method can be used in conjunction with onHTTPResponse to allow an application to handle that information directly.

This should be called before a request is sent to an HTTP server. To handle the response received, call `onHTTPResponse`.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | strRequest | The HTTP request to be sent to the server, as a String.

**See Also**

- `nexPlayer:onHTTPResponse:statusCode:`

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayeronHTTPResponse:(NSString ∗ )strResponsestatusCode:(NSUInteger)statusCode

This method allows responses from an HTTP server to be received and handled in a more customized way.

While NexPlayer normally handles HTTP requests and responses internally, in cases where additional information is required from the server (for example user cookies), this method can be used in conjunction with onHTTPRequest to handle that information directly.

This should be called after a response has been received from the server.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | strResponse | The response from the HTTP server, as a String. |
| in | statusCode | The status code from the HTTP server, as an Integer. |

**See Also**

- `nexPlayer:onHTTPRequest:`

#### - (NSString ∗ ) nexPlayer: (NXPlayer ∗ )nxplayeronModifyHttpRequest:(NSString ∗ )requestString

This method allows the HTTP request that will be used by NexPlayer to be switched when an HTTP request should be modified.

This method will be called if NXPropertyEnableModifyHTTPRequest is set to TRUE or enabled.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | requestString | The HTTP Request data. |

**Returns**

A String with the modified HTTP request. This value will be used by NexPlayer instead of the previous
HTTP request.

**See Also**

`NXProperty::NXPropertyEnableModifyHTTPRequest`

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayeronStatusHTTPInvalidResponse:(NSUInteger)statusCode

This method is called when an HTTP error response was received from the server.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. 
| in | statusCode | contains the error code (this is a normal HTTP response code, such as 404,
500, etc.) |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerplayheadAdvancedTo:(NXDuration)newPosition

Playback has progressed to a certain position.

This event occurs every second during playback, and can be used to update the user interface to reflex the current play position.

The current playback position is also available through `NXPlayer::currentTimeStamp`, and that can be polled on a timer if more frequent updates are necessary.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | newPosition | The new playback position (in milliseconds from start of content) |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerplaylistReceived:(NSString ∗ )newPlaylistforURL:(NSString ∗ )URL

Called whenever a new playlist is received.

This is called every time that the player receives an HLS playlist. This can happen in several cases:

- When the initial (master) playlist is received.
- When the player switches to a new track and loads the playlist for that track.
- Whenever the server updates the playlist while playing live content.

Whenever NXPlayer::HLSTSDescrambler is called with a TS or audio file to be descrambled, that TS or audio file
will always be from the playlist most recently received by this callback.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | URL | The URL of the playlist. |
| in | newPlaylist | The playlist that was just received. Playlists can be very large, so the memory backing this string is managed by the engine. Do not retain this string. If you must use it after this method returns, make a copy of the playlist string or relevant portions. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerseekableStateChangedTo:(BOOL)isSeekableseekBase:(uint64_t) seekBaseseekableLength:(NSUInteger)seekableLen

The seekable state of the content has changed.

Any time the seekable state of the content changes, this event will be sent. This event should be used to update the seek bar and is used to support server-side timeshifting in live content.

If the content is not seekable, `seekBase` and `seekableLen` will both be zero and `isSeekable` will be NO.

If the content is seekable, `isSeekable` will be YES and `seekableLen` will be greater than zero.

For most content, `seekBase` will be zero. However, in the case of seekable live content, there is a sliding window within which seeking is possible. In this case, seekBase will be non-zero and indicates the beginning of that window. The end of the seekable window can be determined using `seekableLen`.

The actual values that can appear in `seekBase` for live content are arbitrary and depend on the server.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | isSeekable | YES if the current contents support seeking, otherwise NO. |
| in | seekBase | The earliest possible time that the player can seek to. |
| in | seekableLen | The length of the seekable region starting atseekBase. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerstreamChangedTo:(NXMediaStreamInfo ∗ )stream

The stream has changed.

This happens for protocols such as Smooth Streaming that support multiple streams. A stream change is usually the result of an API call, such as `setVideoStream:audioStream:trackAttributes: (NXPlayer)`. When this event occurs, a NXPlayerDelegate::nexPlayerDidUpdateContentInfo event will also occur.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | stream | The new stream of NXContentInfo. |

####  - (void) nexPlayer: (NXPlayer ∗ )nxplayersubTitleChange:(NSString ∗ )subtitleTextoriginalBytes:(NSData ∗ )subtitleBytes**

Subtitle (caption) text has changed, and the application should update the display with the new text.

> **Deprecated** This doesn’t include subtitle source information, but is retained for compatibility with existing code. nexPlayer:subTitleChange:originalBytes:subtitleSource: should be used instead, in new code.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | subtitleText | The string as decoded using the detected encoding. |
| in | subtitleBytes | The original bytes of the string prior to decoding. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayersubTitleChange:(NSString ∗ )subtitleTextoriginalBytes:(NSData ∗ )subtitleBytessubtitleSource:(NSString ∗ )source

Subtitle (caption) text has changed, and the application should update the display with the new text.

NexPlayer handles the parsing, decoding and timing of subtitle text, but not the display of that text. When subtitle text is ready for display, this method is called, and the delegate must display the text in an appropriate manner. Often, this is simply done by setting the text attribute of a UITextView that is positioned on top of the video.

For local subtitles, the subtitle text from multiple tracks may be combined in a single string in the `subtitleText` and `subtitleBytes` parameters, depending on the setting of NXPlayer::captionLanguages.

There are multiple sources for subtitles. For example, subtitles may come from a local subtitle file (such as SMI, SUB, or SRT file) specified when the content was opened, or they may be included as part of the data streamed from the server. When the delegate is called, the source parameter identifies the source of the subtitle text. This text replaces any previous text from the same source. Most applications only play subtitles from a single source, so this parameter can usually be ignored. The source may be any string, but in the current version of the SDK it will always be one of:

- LOCAL
- STREAM

To handle subtitles from an arbitrary number of sources simultaneously, use thesourcevalue as a dictionary key and keep a dictionary of the current subtitles for each source. Then concatenate these when updating the display.

> **A note about Encoding**

> Many subtitle formats do not actually specify an encoding for the subtitle text. NexPlayer uses a heuristic algorithm to attempt to determine the encoding.
> 
> Since it is not possible to make an absolutely certain determination about the encoding in use automatically, alternative algorithms may be better suited to some applications, or there may be applications where it is desirable to let the user select the encoding.
> 
> 
> For these reasons, in addition to a text string (decoded using the detected encoding), NexPlayer also provides the raw bytes prior to decoding, so the application may handle them differently if necessary.
> 
> Currently, the following encodings are detected automatically:
> 
> - ASCII (low ASCII only)
> - UTF-8 (Unicode)
> - EUC-KR (Korean)
> - EUC-JP (Japanese)

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | subtitleText | The string as decoded using the detected encoding. |
| in | subtitleBytes The original bytes of the string prior to decoding. |
| in | source | The source of the subtitles. See above. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayertrackChangedTo:(NXTrackInfo ∗ )track

The track has changed.

This happens for protocols such as HLS that provide the content in multiple formats or at multiple resolutions or bitrates. The ID of the new track can be found in NXMediaStreamInfo::currentTrack and also as an argument to this method. When this event occurs, a NXPlayerDelegate::nexPlayerDidUpdateContentInfo event will also occur.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |
| in | track | The new track. |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerupdatedCaption:(NXClosedCaption ∗ )caption

This method receives updated closed captions for contents such as WebVTT or TTML.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | caption | New captions to be displayed on the contents. (see `NXClosedCaption` for more details). |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerupdatedCaption:(NXCEA608Caption ∗ )caption forCEA608Channel:(NXCEA608Channel)channel

CEA 608 closed caption text has changed.

Whenever new CEA 608 closed caption data is updated, this event will be sent.

NexPlayer can handle and display CEA 608 closed captions fully but an application may also choose to handle the display of these captions differently in another independent view.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | caption | The caption to display (see `NXCEA608Caption` for details). This should replace ALL existing displayed caption text. |
| in | channel | The channel that closed caption data relates to (may be 0 if captions were just turned off, and this event is to erase the caption display).

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerupdatedMetaData:(NSDictionary ∗ )metaData

The metadata associated with the current content has changed.

Whenever any metadata changes for the current content, this method will be called and will provide only the updated fields of the metadata. These can be used to update the UI view for the relevant fields if desired, without calling the entire `NXContentInfo::metaData` object.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | metaData | A dictionary containing only the updated metadata fields. Field names are the same as `NXContentInfo::metaData` |

#### - (void) nexPlayer: (NXPlayer ∗ )nxplayerupdatedSEIPicTiming:(NXPicTimingInfo ∗ )timing

This method provides SEI picture timing information about video frames of H.264 content when it is available and changes.

While SEI may include a variety of attributes, this method specifically receives SEI picture timing information when available.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | timing | The `NXPicTimingInfo` object that includes the new SEI picture timing information for the content. |

#### - (void) nexPlayerBeganDownloadBuffering: (NXPlayer ∗ )nxplayer

The player does not have enough data to play back content.

This event occurs during a progressive download when there is not enough data to continue playing. The download will continue, but playback will be temporarily suspended until additional data is available. Once enough data is available, the nexPlayerFinishedDownloadBuffering: event will occur.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDataInactivityTimeout: (NXPlayer ∗ )nxplayer

NexPlayer hasn’t received any data from the streaming server for the period specified by NXPropertyData-
InactivityTimeout.

The value of NXPropertyDataInactivityTimeout can be set by calling setProperty:toValue: (NXPlayer), and it indicates the maximum time to wait for packets from the server before timing out and generating this event.

The delegate should take appropriate action in response to this event. In most cases, the correct response is to notify the user and to stop playback and close the content.

If this method is not implemented by the delegate, the default behavior is to forward this to nexPlayer:encounteredError: with the error code NXErrorDataInactivityTimeout (which, in most cases, will display a message to the user, stop playback, and close the content).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event.

#### - (void) nexPlayerDidBeginBuffering: (NXPlayer ∗ )nxplayer

The player has begun buffering.

This happens when the player doesn’t have enough data to ensure seamless playback, and is waiting for more data before continuing playback.

Buffering happens in two cases:

1. When beginning playback, the player buffers enough data to play back several seconds of content. The exact amount of initial buffering can be adjusting by changing the property `NXPropertyInitialBufferingDuration`.
2. If the player runs out of data during playback (if there is not enough data to decode and play back any
    additional frames), playback will temporarily stop until the player buffers enough data to play back several seconds of content. The exact amount of this additional buffering can be adjusted by changing the property `NXPropertyReBufferingDuration`.

In any case, when buffering begins, this event is sent. Throughout the buffering process, `nexPlayer:bufferingProgress:` events will be sent to indicate the percentage of required data that has been buffered so far. When enough data has been buffered to resume playback, the `nexPlayerDidFinishBuffering:` event will be sent.

In general, the application should handle these events as follows:

- `nexPlayerDidBeginBuffering`: Display a *"buffering..."* message
- `nexPlayer:bufferingProgress`: Update the message to reflect the current buffering percentage.
- `nexPlayerDidFinishBuffering`: Remove the buffering message

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidBeginDownloading: (NXPlayer ∗ )nxplayer

The player has begun to download the content.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidChangeCodec: (NXPlayer ∗ )nxplayer

One or more of the codecs in use has changed.

There was a change in the audio codec in use, the video codec in use, or both. The new codecs are in `NXContentInfo::audioCodec` and `NXContentInfo::videoCodec`.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidChangeDSI: (NXPlayer ∗ )nxplayer

An attribute relating to the video or audio format (such as the resolution, bitrate, etc.) has changed.

See `NXPlayer::contentInfo` for the updated information.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidConnectForDownload: (NXPlayer∗ )nxplayertotalSize:(NSInteger)sizeInBytes

The player connected to the HTTP server and got the HEAD information successfully.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |
| in | sizeInBytes | The total size, in bytes, of the file to be downloaded. |

#### - (void) nexPlayerDidConnectToServer: (NXPlayer ∗ )nxplayer

The RTSP connection has been successfully established with the streaming server.

This is a one-time event and applies only to RTSP streaming, not to other forms of streaming.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidFailToGetAudioCodec: (NXPlayer ∗ )nxplayer

Failed to determine the audio codec.

This notification can happen at the beginning of playback, or during playback if there is an audio codec change. This can happen because of a switch to a new codec that NexPlayer does not support, or can be due to an error in the format of the content or corrupted data in the content.

The player doesn’t take any special automatic action when this event occurs. Playback is allowed to continue because the track may change again in future to one that contains a supported codec. However, it may be desirable for the application to indicate the state temporarily in the user interface.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidFailToGetVideoCodec: (NXPlayer ∗ )nxplayer

Failed to determine the video codec.

This notification can happen at the beginning of playback, or during playback if there is a video codec change. This can happen because of a switch to a new codec that NexPlayer does not support, or due to an error in the format of the content or corrupted data in the content.

The player doesn’t take any special automatic action when this event occurs. Playback is allowed to continue because the track may change again in future to one that contains a supported codec. However, it may be desirable for the application to indicate the state temporarily in the user interface.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidFailToInitAudioCodec: (NXPlayer ∗ )nxplayer

The audio codec failed to initialize.

This can happen for several reasons. The container may indicate the wrong audio codec, or the audio stream may be incorrect or corrupted, or the audio stream may use a codec version or features that NexPlayer doesn’t support.

The player doesn’t take any special automatic action when this event occurs. Playback is allowed to continue because the track may change again in future to one that contains a supported codec. However, it may be desirable for the application to indicate the state temporarily in the user interface.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidFailToInitVideoCodec: (NXPlayer ∗ )nxplayer

The video codec failed to initialize.

This can happen for several reasons. The container may indicate the wrong video codec, or the video stream may be incorrect or corrupted, or the video stream may use a codec version or features that NexPlayer doesn’t support.

The player doesn’t take any special automatic action when this event occurs. Playback is allowed to continue because the track may change again in future to one that contains a supported codec. However, it may be desirable for the application to indicate the state temporarily in the user interface.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidFinishBuffering: (NXPlayer ∗ )nxplayer

The player has finished buffering.

This happens when the player has buffered the requested amount of data and is about to resume playback.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |

**See Also**

- `nexPlayerDidBeginBuffering:` for more information

#### - (void) nexPlayerDidFinishDownloading: (NXPlayer ∗ )nxplayer

The player has finished downloading the content.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidReachEndOfContent: (NXPlayer ∗ )nxplayer

Playback has completed successfully up to the end of content.

If playback was started with autoPlay:YES, the player will automatically be stopped when this event occurs. Otherwise, it is necessary to stop playback by calling

`[nxplayer stop];`

in response to this event.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |

#### - (void) nexPlayerDidStartAudioTask: (NXPlayer ∗ )nxplayer

The player’s audio task has been activated.

Generally, applications can ignore this event except for debugging purposes.

It is not reliable to use this to detect which content has audio, because the audio task may be reused for playing other content, or there may temporarily be no audio due to bandwidth limitations during streaming. Instead, to determine if the content includes audio, check NXContentInfo::hasAudio.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |

#### - (void) nexPlayerDidStartVideoTask: (NXPlayer ∗ )nxplayer

The player’s video task has been activated.

Generally, applications can ignore this event except for debugging purposes.

It is not reliable to use this to detect which content has video, because the video task may be reused for playing other content, or there may temporarily be no video due to bandwidth limitations during streaming. Instead, to determine if the content includes video, check NXContentInfo::hasVideo.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerDidUpdateContentInfo: (NXPlayer ∗ )nxplayer

The content information has changed.

There are many reasons why a content information change can happen. One example is changing streams or
tracks when playing streaming content.

There are several more specific events that can occur in addition to this one, such as `nexPlayerDidChangeCodec:`. If there is a more specific event suitable to your need, you should consider using that instead.

The new content information can be found in `NXPlayer::contentInfo`.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

#### - (void) nexPlayerFinishedDownloadBuffering: (NXPlayer ∗ )nxplayer

This event occurs when there is enough data downloaded to resume playback.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The `NXPlayer` instance that generated the event. |

**See Also**

- nexPlayerBeganDownloadBuffering: for details.

#### - (void) nexPlayerPauseSupervisionTimeout: (NXPlayer ∗ )nxplayer

NexPlayer has been in the `NXPlayerStatePause` state for the period specified by NXPropertyPauseSupervisionTimeout.

The value of NXPropertyPauseSupervisionTimeout can be set by calling `setProperty:toValue: (NXPlayer)` for NXPropertyPauseSupervision, and it indicates that the maximum time in the paused state has passed.

The delegate may ignore this event (in which case, nothing will happen) or it may take an appropriate action in response to this event, such as to resume playback or to stop streaming altogether.

If this method is not implemented by the delegate, the default behavior is to forward this to `nexPlayer:encounteredError`: with the error code `NXErrorPauseSupervisionTimeout` (which, in most cases, will display a message to the user, stop playback, and close the content).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event.

#### - (void) nexPlayerReadyForControl: (NXPlayer ∗ )nxplayer

The player is now ready to accept control commands (pause and seek) if appropriate for the open content.

There are several stages that the player must go through (opening the content, starting the content, waiting for initial buffering to complete) before it is legal to issue seek and pause commands to the player. Once these stages have completed, this event is sent. Note that just because the player is ready to accept commands doesn’t mean that all commands are valid (for example, live content may still not be seekable).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event. |

#### - (void) nexPlayerRTSPCommandTimeout: (NXPlayer ∗ )nxplayer

NexPlayer made an RTSP request, but has not received a response from the streaming server within the period specified by NXPropertyRTSPCommandTimeout.

The value of NXPropertyRTSPCommandTimeout can be set by calling setProperty:toValue: (NXPlayer) and controls the maximum time that the player will wait for a response before generating this event.

If the delegate implements this method, it should respond by stopping and closing the currently playing content (it can do this by simply calling close (NXPlayer), which will automatically stop the content first).

A message should also be displayed to the user.

If this method is not implemented by the delegate, the default behavior is to forward this to nexPlayer:encounteredError: with the error code NXErrorRTSPCommandTimeout (which, in most cases, will display a message to the user, stop playback, and close the content).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | nxplayer | The NXPlayer instance that generated the event.

### NXPlayerDRMDelegateProvider Class Reference

A class dedicated to provide DRM delegates to the associatedNXPlayerinstance.

Example code :

```objc
@interface PlayerViewController <NXPlayerGetKeyExtDelegate> : ...
...
@end

@implementation PlayerViewController
...

- (void) initializePlayer
{
    ...
    NXPlayer*player = self.player;
    NXPlayerDRMDelegateProvider*drmDelegateProvider = [
       NXPlayerDRMDelegateProvider providerWithNXPlayer:player];
    drmDelegateProvider.getKeyExtDelegate = self;
    self.drmDelegateProvider = drmDelegateProvider;
    ...
}
- (NSData*) nexPlayer:(NXPlayer*) nxplayer getKeyExtForURLString:(NSString*) URLString result:(
    BOOL*) pResult
{
    ...
}
```
#### + (id) providerWithNXPlayer: (NXPlayer ∗ )nxplayer

This method creates an instance of this class associated with the parameternxplayer.

#### - (id < NXPlayerGetKeyExtDelegate > ) getKeyExtDelegate [read] , [write] , [nonatomic] , [weak]

Delegate object that will be called with it’s nexPlayer:getKeyExtForURLString:result: (NXPlayerGetKeyExtDelegatep) method when an encryption key retrieval is required from a HLS playlist to be passed to NexPlayer for descrambling.

**See Also**

NXPlayerGetKeyExtDelegate

### NXPlayerGetKeyExtDelegate Protocol Reference

Delegate interface that defines the methods that will be called when an encryption key retrieval is required from a HLS playlist to be passed to NexPlayer for descrambling.

#### - (NSData ∗ ) nexPlayer: (NXPlayer ∗ )nxplayergetKeyExtForURLString:(NSString ∗ )URLStringresult:(BOOL ∗ ) pResult

This method is called for encryption key retrieval from the NexPlayer for descrambling.

**Parameters**

| Name  | Description  | 
|---|---|
| nxplayer | The NXPlayer instance that generated the event. |
| URLString |  The URL of the encryption key. |
| pResult |  [out] YES if encryption key was successful. NO, otherwise. |

**Returns**

NSData object that contains encryption key information if successful .nil otherwise

### NXPlayerRenderView Class Reference

Provides a view in which NexPlayer video output can be displayed, creates an associated NXPlayer object, and binds it to the view.

This is similar to NXPlayerView, except that NXPlayerView scales the video to maintain the aspect ratio, and handles resizing and rotation, whereas NXPlayerRenderView simply stretches the video to fill the view.

This is the recommended way to render video with NexPlayer if you wish to calculate scaling values yourself.

The layer associated with this class is a CAEAGLLayer, suitable for use with NXPlayer. Each NXPlayerLayer creates and manages an associated NXPlayer object, including assigning the view’s layer to the render Layer of the player, and updating the NXPlayer video render buffers if the size of the view changes.

This provides all of the usual UIView methods and properties.

In addition, you can use the NXPlayerRenderView::player property to access the NXPlayer object and control the player. For example, to play a local video file named "test.wmv" in a NXPlayerRenderView, you could simply write:

```objc
[hPlayerView.player openAndPlayFromBundle: @"test.wmv"];
```

#### - (NXPlayer ∗ ) player [read] , [nonatomic] , [strong]

The NXPlayer instance associated with this view.

This can be used to control playback within this view.

### NXPlayerView Class Reference

Provides a view in which NexPlayer video output can be displayed, and creates an associated NXPlayer object and binds it to the view.

This is the recommended way to render video with NexPlayer.

Each NXPlayerView creates and manages an associated NXPlayer object, including assigning the view’s layer to the renderLayer of the player, and updating the NXPlayer video render buffers if the size of the view changes.

Each NXPlayerView also creates and maintains an NXPlayerRenderView in which the actual player output is displayed. The NXPlayerRenderView is managed automatically to maintain the correct scaling. In the case of content with CEA 608 closed captions, if the captions are turned on, the NXPlayerView also creates and maintains a NXCEA608CaptionView to receive and display caption information as it is received.

This provides all of the usual UIView methods and properties.

In addition, you can use the NXPlayerView::player property to access the NXPlayer object and control the player. For example, to play a local video file named "test.wmv" in an NXPlayerView, you could simply write:

```
[hPlayerView.player openAndPlayFromBundle: @"test.wmv"];
```

#### - (NXScale) autoScaling** [read] , [write] , [nonatomic] , [assign]

Controls automatic scaling of the video image when the view is resized.

Set this to NXScale_None to disable auto scaling (the video image will remain in its original size and position
regardless of layout or rotation changes).

Set this to any other legal value (listed below) to automatically rescale the video whenever the view size changes.
The video is also rescaled to the appropriate size as soon as this value is changed.

Changes to the scale can be animated using the usual UIView animation technqiues (begin and commit).

Possible values:

- `NXScale_None` The video size will not be changed; the size and location can be set by assigning values to thevideoRectproperty.
- `NXScale_OriginalSize` The video will be displayed at its original size, centered in the view. The original video dimensions are calculated using regular (normal resolution) pixels in order to maintain consistency between normal and retina displays.
- `NXScale_FitInView` Fit video to container (as large as possible without cropping). The aspect ratio of the video is maintained. There may be black bars if the aspect ratio of the video doesn’t precisely match the aspect ratio of the view.
- `NXScale_FillView` NexPlayer will fill the parent container. If the video dimensions don’t match the view dimensions, the video will be cropped to avoid black bars. The aspect ratio is maintained.
- `NXScale_Stretch` Stretch the video to match the dimensions of the view (does not maintain the aspect ratio) of the original video.

The default for this is NXScale_Stretch.

> **Warning** Changing this should be done while the NXPlayerView instance is visible on the screen.

#### - (BOOL) captionHidden** [read] , [write] , [nonatomic] , [assign]

Sets visibility state of captions available in content.

Assigning NO hides captions (CEA 608 and CEA 708 closed captions, 3GPP and TTML timed text, and WebVTT text tracks) in the current NXPlayerView.

Default value is NO.

**See Also**

- CEA608CaptionView

#### - (NXCaptionRenderController** ∗) captionRenderController** [read] , [nonatomic] , [strong]

TheNXCaptionRenderControllerobject returned by this property allows the rendering options set for captions to be rendered on the screen.

#### - (NXCEA608CaptionView** ∗ ) CEA608CaptionView [read] , [nonatomic] , [strong]

The `NXCEA608CaptionView` contained within this view.

If closed captions are turned on, and the current captions are CEA 608 closed caption standard, they will be displayed in this view whenever caption data is updated by NexPlayer.

If a developer wishes to handle and display CEA 608 closed captions independently, the captionHidden property must be setNOand a separate view should be implemented to receive and display captions in the application.

**Deprecated** If a developer wishes to handle and display CEA 608 closed captions independently,captionHidden property must be set toNOinstead of using `CEA608CaptionView.hidden`.

**See Also**

- captionHidden

#### - (NXPlayer** ∗ ) player [read] , [nonatomic] , [weak]

The NXPlayer instance associated with this view.

This can be used to control playback within this view.

#### - (NXPlayerRenderView** ∗ ) renderView** [read] , [nonatomic] , [strong]

The NXPlayerRenderView contained within this view.

There is generally not much reason to access this directly.

#### - (BOOL) useCEA608CustomView** [read] , [write] , [nonatomic] , [assign]

This property allows the rendering mode of the CEA 608 closed captions.

NO means basic CEA 608 rendering, meeting the specifications of the CEA 608 standard, and YES means an enhanced rendering mode that makes possible for CEA 608 closed captions to be rendered with additional display settings. (including the changing of the foreground and background colors, the font size, the font type, etc).

Default value is NO.

####= - (CGRect) videoRect** [read] , [write] , [nonatomic] , [assign]

Sets the rectangle in which the video image will be drawn.

Dimensions are in pixels, and coordinates are relative to the NXPlayerView.

Changing this property automatically forcesautoScalingto be set toNXScale_None.

Enabling automatic scaling (settingautoScalingto a value other thanNXScale_None) causes the value of
videoRectto change automatically when the layout or rotation of a parentFrame changes.

### NXRemoteFileIOInterface Protocol Reference

Provides replacements for standard operating system file I/O functions.

If you are playing back local content that is not available via the standard operating system file APIs, you can provide your own replacement functions which NexPlayer will use for opening and reading your file.

To provide your own replacement funtions, create a class that implements this protocol, and assign an instance of that class to NXPlayer::remoteFileIOInterface

#### - (int) remoteFileClose: (NXFileHandle)hFile

Replacement for `close()`

This should close the requested file and invalidate the handle.

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file to be closed (as returned by remoteFileOpen:mode:) |
| buffer | A buffer ro receive the bytes read from the file. |
| length | The number of bytes to read. |

**Returns**

- 0 for success  
- -1 if an error occurred.

#### - (NXFileHandle) remoteFileOpen: (char ∗ )filenamemode:(NXFileMode)mode

Replacement for `open()`

This should open the requested file in the requested mode, and return a handle to the file. The handle may be any
value that this instance of NXRemoteFileIOInterface can use to identify the open file.

**Parameters**

| Name  | Description  | 
|---|---|
| filename | The path and filename of the file to open. |
| mode | NXFileModeRead, NXFileModeWrite, NXFileModeReadWrite or NXFileModeCreate. |

**Returns**

The handle to the file.

#### - (ssize_t) remoteFileRead: (NXFileHandle)hFilebuffer:(void ∗ )bufferlength:(NSUInteger)length

Replacement for `read()`

This should read the specified number of bytes from the file. Unless the end of the file has been reached, at least one byte must be read (to avoid confusion with an end-of-file condition).

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file to read from (as returned by remoteFileOpen:mode:) |
| buffer | A buffer to receive the bytes read from the file. |
| length | The number of bytes to read. |

**Returns**

The actual number of bytes read; 0 if the end of the file was reached; -1 if an error occurred.

#### - (long long) remoteFileSeek64: (NXFileHandle)hFileoffset:(long long)offsetorigin:(NXFileSeekOrigin)origin

Same as remoteFileSeek:offset:origin: except that 64-bit values are used for the offset and return value, allowing
support of files greater than 2GB in size.

This should move the current read/write offset to the specified position.

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file for which to adjust the read/write offset (as returned by remoteFile-Open:mode:) |
| offset | The offset (from origin) by which to move the current read/write offset. |
| origin | The position which theoffsetparameter is measured relative to. May be NXFileSeek-OriginBeginning, NXFileSeekOriginCurrent or NXFileSeekOriginEnd. |

**Returns**

The new position within the file.

#### - (int) remoteFileSeek: (NXFileHandle)hFileoffset:(int)offsetorigin:(NXFileSeekOrigin)origin

Replacement for `lseek()`

This should move the current read/write offset to the specified position.

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file for which to adjust the read/write offset (as returned by remoteFile-Open:mode:) |
| offset | The offset (from origin) by which to move the current read/write offset. |
| origin | The position which theoffsetparameter is measured relative to. May be NXFileSeek-OriginBeginning, NXFileSeekOriginCurrent or NXFileSeekOriginEnd. |

**Returns**

The new position within the file.

#### - (long long) remoteFileSize: (NXFileHandle)hFile

Replacement for getting the size of a file.

This should return the size of the filewithoutmodifying the position to which the file has been seeked (if the seek
location must be moved to determine the size, this function should move it back afterwards).

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file (as returned by remoteFileOpen:mode:) |

**Returns**

The actual number ofbytesof file, or -1 if an error occurred.

#### - (ssize_t) remoteFileWrite: (NXFileHandle)hFilebuffer:(void ∗ )bufferlength:(NSUInteger)length

Replacement for `write()`

This should write the specified number ofbytesto the file.

**Parameters**

| Name  | Description  | 
|---|---|
| hFile | The handle of the file to write to (as returned by remoteFileOpen:mode:) |
| buffer | A buffer ofbytesto write to the file. |
| length | The number ofbytesto write to file. |

**Returns**

The actual number of bytes written, or -1 if an error occurred.

### NXRTStreamingInfo Class Reference

This class manages information about the current streaming content.

#### - (NSUInteger) curNetworkBw** [read] , [nonatomic] , [assign]

The actual bitrate, inbps, of the read segments. The read bitrate is the average speed at which the streaming
segments are read from the network server.

#### - (NSUInteger) curTrackBw** [read] , [nonatomic] , [assign]

The bitrate, inbps, as specified in the segment profile.

#### - (NSString ∗ ) initialMpd [read] , [nonatomic] , [strong]

Full content of an initial manifest file.

#### - (NSString ∗ ) initialMpdUrl [read] , [nonatomic] , [strong]

The actual URI (after all the redirects) for the request of a manifest file.

#### - (NSString ∗ ) masterMpd [read] , [nonatomic] , [strong]

Full content of a master manifest file.

#### - (NSString ∗ ) masterMpdUrl [read] , [nonatomic] , [strong]

Master manifest URL.

#### - (uint64_t) numOfBytesRecv [read] , [nonatomic] , [assign]

The number of bytes received from the server by the player.

#### - (NSUInteger) numOfRedirect [read] , [nonatomic] , [assign]

The total number of redirects. This includes redirects for both the manifest file and the individual segments.

#### - (NSUInteger) numOfSegmentDownRate [read] , [nonatomic] , [assign]

The number of the segments with a lower read bitrate than the bitrate specified on the profile. The read bitrate is the average speed at which the streaming segments are read from the network server.

#### - (NSUInteger) numOfSegmentFailToParse [read] , [nonatomic] , [assign]

The number of segments failed to receive during the streaming.

#### - (NSUInteger) numOfSegmentFailToRecv [read] , [nonatomic] , [assign]

The number of segments failed to receive from the server.

#### - (NSUInteger) numOfSegmentInBuf [read] , [nonatomic] , [assign]

The total number of segments in the buffer.

#### - (NSUInteger) numOfSegmentRecv [read] , [nonatomic] , [assign]

The number of received segments from the server by the player.

#### - (NSUInteger) numOfSegmentRequest [read] , [nonatomic] , [assign]

The number of requested segments from the server by the player.

#### - (NSUInteger) numOfSegmentTimeout [read] , [nonatomic] , [assign]

The number of segments that resulting a timeout.

#### - (NSUInteger) numOfTrackSwitchDown [read] , [nonatomic] , [assign]

The number of times that a content profile has changed to a profile with a lower bitrate.

#### - (NSUInteger) numOfTrackSwitchUp [read] , [nonatomic] , [assign]

The number of times that a content profile has changed to a profile with a higher bitrate.

#### - (NSString ∗ ) startSegUrl [read] , [nonatomic] , [strong]

The description of an initially selected profile.

### NXSARInfo Struct Reference

SAR (Sample Aspect Ratio) of H.264 contents.

**Public Attributes**

- `NSUInteger width`  
    The width of the content.
- `NSUInteger height`  
    The height of the content.

### NXSDKVersion Class Reference

A singleton class containing version information about the NexPlayer SDK.

There is only one object of this class, and it is accessed using:

```objc
NXSDKVersion *version = [NXSDKVersion sharedInstance];
```

Attempts to call alloc on this class oriniton instances of it will fail.

The NXSDKVersion instance has properties describing the current version. The recommended method of displaying the current version at build time is as follows:

```objc
NXSDKVersion*version = [NXSDKVersion sharedInstance];
NSString*buildTimeAndVersion =
	[NSString stringWithFormat: @"%@ %@ %@ %@",
	version.versionString,
	version.buildDate,
	version.buildTime,
	version.buildTimeZone];
NSLog( @"Version: %@", buildTimeAndVersion );
```

#### + (NXSDKVersion ∗ ) sharedInstance

Returns the single shared instance of this class.

This can be used to access the current SDK version information.

**Returns**

The shared singleton instance of this class.

**See Also**

NXSDKVersion for more information.

#### - (NSString ∗ ) SDKName [read] , [nonatomic] , [weak]

The name of the current SDK. This is a string the same as NXPlayer::SDKName.

### NXSessionData Class Reference

This class manages information about the arbitrary session data of the HLS master playlist.

**Properties**

- `NSUInteger uId` unique ID for internal use.
- `NSString∗dataID` This is a unique string used to identify the session data.
- `NSString∗value` It is identified by a string, DATA-ID. If a LANGUAGE is specified, this attribute must be included in a human-readable form in the specified language.
- `NSString∗uri` A string containing a URI, the resource identified by this URI must be formatted using JSON (JavaScript Standard Object Notation, one of the notations, RFC 7159).
- `NSString∗language` Language of the VALUE, using the RFC5646 value.
- `NSString∗abstractUrl` Absolute requested URI.
- `NSData∗dataFromUrl` data from URI

### NXSmoothStreamFragmentDescrambler Protocol Reference

A protocol you can implement if you wish to implement Smooth Streaming fragment descrambling.

See NXPlayer::smoothStreamFragmentDescrambler for additional information.

#### - (unsigned long) descrambleSmoothStreamingFragmentForPlayer: (NXPlayer ∗ )playerinputBuffer:(unsigned char ∗ )pInputBufferinputBufferSize:(unsigned int)uiInputBufferSizeoutputBuffer:(unsigned char ∗ )pOutputBuffer outputBufferSize:(unsigned int ∗ )puiOutputBufferSize [optional]

Called by the player when there is data available for descrambling.

**Deprecated** Please use `descrambleSmoothStreamingFragmentForPlayer:inputBuffer:inputBufferSize:output
Buffer:outputBufferSize:mediaFileURL:parentPlaylistURL:` instead.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
|  | player | The NXPlayer instance that this descrambler has been assigned to. |
| in | pInputBuffer | The original (possibly scrambled) input data. |
|  | uiInputBufferSize | The size (in bytes) of the input buffer. |
| out | pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location. |
| out | puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller thanuiInputBufferSize, but not larger. |

#### - (unsigned long) descrambleSmoothStreamingFragmentForPlayer: (NXPlayer ∗ )playerinputBuffer:(unsigned char ∗ )pInputBufferinputBufferSize:(unsigned int)uiInputBufferSizeoutputBuffer:(unsigned char ∗ )pOutputBufferoutputBufferSize:(unsigned int ∗ )puiOutputBufferSizemediaFileURL:(char ∗ )mediaFileURLparentPlaylistURL:(char ∗ )parentPlaylistURL [optional]

Called by the player when there is data available for descrambling.

This function is called every time a Smooth Streaming fragment is received, regardless of whether or not the
fragment is encrypted. It is the responsibility of this callback to determine whether or not the fragemnt is encrypted
and descramble the fragment if necessary.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | player | The NXPlayer instance that this descrambler has been assigned to. |
| in | pInputBuffer | The original (possibly scrambled) input data. |
| in | uiInputBufferSize | The size (in bytes) of the input buffer. |
| out | pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location. |
| out | puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller thanuiInputBufferSize, but not larger. |
| in | mediaFileURL | The URL of the media file that this fragment belongs to. | 
| in | parentPlaylistURL | The URL of the parent playlist thatmediaFileURLbelongs to. |


### NXSmoothStreamPlayReadyDescrambler Protocol Reference

A protocol you can implement if you wish to implement Smooth Streaming PlayReady descrambling.

See NXPlayer::smoothStreamPlayReadyDescrambler for additional information.

#### - (NSInteger) descrambleSmoothStreamPlayReadyForPlayer: (NXPlayer ∗ )playerinputBuffer:(unsigned char ∗ )pInputBufferinputBufferSize:(unsigned int)uiInputBufferSize outputBuffer:(unsigned char ∗ )pOutputBuffer outputBufferSize:(unsigned int ∗ )puiOutputBufferSize sampleEncBox:(unsigned char ∗ )pSampleEncBox sampleEncBoxLen:(unsigned int)dwSampleEncBoxLen sampleIndex:(unsigned int)dwSampleIDXtrackID:(unsigned int)dwTrackID

Called by the player when there is data available for descrambling.

This function is called every time a Smooth Streaming fragment is received, regardless of whether or not the fragment is encrypted. That must be determined separately.

**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| | player | The NXPlayer instance that this descrambler has been assigned to. |
| in | pInputBuffer | The original (possibly scrambled) input data. |
| | uiInputBufferSize | The size (in bytes) of the input buffer. |
| out | pOutputBuffer | The location at which to write the descrambled output data. Note that this may overlap or be the same as the input buffer location. |
| out | puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller than uiInputBufferSize, but not larger. |
| out | pSampleEncBox | The SampleEncryptionBox, as detailed in the[MS-SSTR] Smooth Streaming Protocol Specification. |
| | dwSampleEncBoxLen | The length, in bytes, of the data atpSampleEncBox |
| | dwSampleIDX | The index of the media object (frame or sample, depending on media format) being descrambled. |
|| dwTrackID | Media Track ID, fromTfhdBox, as defined in the[MS-SSTR] Smooth Streaming Protocol Specification. |

### NXStatisticsAPI Class Reference

This class manages the playback statistics of the content.

#### - (id) initWithPlayer: (NXPlayer ∗ )player

Designated initializer.

**Parameters**

| Name  | Description  | 
|---|---|
| player | TheNXPlayerinstance. |

**Returns**

An instance ofNXStatisticsAPIclass.

#### - (NXBufferInfo ∗ ) bufferInfo [read] , [nonatomic] , [strong]

Instance ofNXBufferInfoclass to access buffer information related methods such asNSUInteger.

**See Also**

NXBufferInfo

#### - (NXDeviceInfo ∗ ) deviceInfo [read] , [nonatomic] , [strong]

The information about the current device streaming a HLS content.

**See Also**

NXDeviceInfo

#### - (id < NXHttpStateDelegate > ) httpStateDelegate [read] , [write] , [nonatomic] , [weak]

An object that conforms to NXHttpStateDelegate which delivers HTTP state information.

**See Also**

NXHttpStateDelegate


#### - (NXRTStreamingInfo ∗ ) RTStreamingInfo [read] , [nonatomic] , [strong]

Information about the current HLS content.

**See Also**

NXRTStreamingInfo

### NXStatsInfo Class Reference

This interface provides playback statistics about the current content in NexPlayer.

This interface can be used to retrieve playback statistics such as the decoded frame rate and the rate of frames being rendered in the player over a short interval of content playback, which may be useful in monitoring player performance and user experience.

**See Also**

NXPlayer.h/statsInfo

#### - (NSUInteger) avgAudioBitrate [read] , [nonatomic] , [assign]

The average bitrate of the audio content currently playing.

#### - (NSUInteger) avgTimeDecodingVideoFrames [read] , [nonatomic] , [assign]

The average time took to decode a video frame.

#### - (NSUInteger) avgTimeRenderingVideoFrames [read] , [nonatomic] , [assign]

The average time took to render a video frame.

#### - (NSUInteger) avgVideoBitrate [read] , [nonatomic] , [assign]

The average bitrate of the video currently playing.

#### - (NSUInteger) decodedVideoFramesLastInterval [read] , [nonatomic] , [assign]

Number of video frames decoded by NexPlayer during the last interval of content.

The default interval of content is 2seconds.

#### - (double) decodedVideoFramesPerSec [read] , [nonatomic] , [assign]

The average number of video frames decoded per second.

#### - (NSUInteger) numDecodingVideoFrames [read] , [nonatomic] , [assign]

Number of video frames decoded by NexPlayer during the last interval of content.

The default interval of content is 2 seconds.

> **Deprecated** Use `decodedVideoFramesLastInterval` Instead.

#### - (NSUInteger) numRenderingVideoFrames [read] , [nonatomic] , [assign]

Number of video frames rendered and displayed by NexPlayer over the last interval of content.

Even though data for more frames of current content may be decoded during an interval, it may be necessary at times for some frames to be skipped in certain circumstances, and this value provides clearer information about what is actually displayed by NexPlayer.

> **Deprecated** Use `renderedVideoFramesLastInterval` Instead.

#### - (NSUInteger) renderedVideoFramesLastInterval [read] , [nonatomic] , [assign]

Number of video frames rendered and displayed by NexPlayer over the last interval of content.

Even though data for more frames of current content may be decoded during an interval, it may be necessary at times for some frames to be skipped in certain circumstances, and this value provides clearer information about what is actually displayed by the NexPlayer.

#### - (double) renderedVideoFramesPerSec [read] , [nonatomic] , [assign]

The average number of video frames displayed per second.

#### - (NSUInteger) timeDecodingSingleVideoFrame [read] , [nonatomic] , [assign]

The time took to decode a video frame.

#### - (NSUInteger) timeRenderingSingleVideoFrame [read] , [nonatomic] , [assign]

The time took to render a video frame.

#### - (NSUInteger) totalAudioFrameBytes [read] , [nonatomic] , [assign]

The total size of all the audio frames, in bytes.

#### - (NSUInteger) totalDecodedVideoFrames [read] , [nonatomic] , [assign]

The total number of video frames decoded to play a video content.

#### - (NSUInteger) totalDroppedVideoFrames [read] , [nonatomic] , [assign]

The total number of video frames skipped while playing a video content.

#### - (NSUInteger) totalRenderedVideoFrames [read] , [nonatomic] , [assign]

The total number of video frames displayed during playing a video content.

#### - (NSUInteger) totalVideoFrameBytes [read] , [nonatomic] , [assign]

The total size of all the video frames of a video content, inbytes.

#### - (NSUInteger) totalVideoFrames [read] , [nonatomic] , [assign]

The total number of video frames to decode.

#### - (NSUInteger) videoFramesLastInterval [read] , [nonatomic] , [assign]

The number of video frames available to be decoded during the last interval of content.

### NXSubtitleTrack Class Reference

Represents a subtitle track available for the current content.

Note that this is not the same as the text track associated with streaming content. Although the two have a similar end result, functionally they are different and are implemented with different mechanisms.

For more information on local subtitles, see NXPlayer::subtitleTracks

For more information on text tracks for streaming content, see setVideoStream:audioStream:textStream:trackAttributes: (NXPlayer)

#### - (BOOL) enabled [read] , [write] , [nonatomic] , [assign]

Determines whether or not this track is enabled (included in subtitle displays).

This property can be set to YES to enable this track, or NO to disable this track. The change will take effect immediately.

#### - (NSDictionary ∗ ) metadata [read] , [nonatomic] , [strong]

A dictionary containing additional information about this subtitle track.

The information available varies depending on the subtitle file format. For SMI files, the "SMIClass" key will be set.

### NxTimedMetaExtraTag Class Reference

The properties in this interface define the different details of a custom tag in ID3 metadata.

#### - (BOOL) isPicture [read] , [nonatomic] , [assign]

This property checks whether the current tag contains any picture data and if they are accessible through thedata property.

If YES, the picture data format is inmimeType propertyand thedata propertycontains the binary data of
the image. If NO, the tag only includes text data and is accessible throughtext property.

### NXTrackInfo Class Reference

Information about a track in a media stream.

For any given stream, the list of available tracks is in NXMediaStreamInfo::tracks.

Any given stream may have multiple tracks containing the same content encoded at different quality levels to support different network conditions.

#### - (NXCodecID) codecID** [read] **,** [write] **,** [nonatomic] **,** [assign]

This indicates the codec used for the given track.

> **Warning** Do not trust this value in HLS, DASH and MS Smooth Streaming mode, as invalid values are sometimes provided.

#### - (unsigned int) internalId [read] , [write] , [nonatomic] , [assign]

An internal numeric ID that uniquely identifies a track.

This can be used to determine if two different NXTrackInfo objects refer to the same track:

```objc
if( [trackInfoA internalId] == [trackInfoB internalId] ) {
	// trackInfoA and trackInfoB refer to the same stream
}
```

However, since a given NXMediaStreamInfo object can only refer to one set of NXTrackInfo objects (one per track), it is generally safe to simply test for identitiy:

```objc
if( [mediaStreamInfo.tracks objectAtIndex:i] == mediaStreamInfo.currentTrack ){
	// The object at index i is the current track
}
```

The actual integer value that appears here is arbitrary and may be any 32-bit value. The method for assigning the
internal ID may change in future versions.

### NXWMDRMDescrambler Protocol Reference

The NXWMDRMDescrambler protocol must be adopted and implemented by objects that provide WM-DRM de-
scrambling services.

Any object can adopt this protocol, but it is typically adopted by either the NXPlayerDelegate, or by a dedicated DRM descrambling object.

An object that implements this protocol should be assigned to NXPlayer::WMDRMDescrambler.

This protocol supports both payload-level and packet-level descrambling. The method DRMType (NXWMDRM-
Descrambler-p) must return a value indicating the type of DRM that an objecting implementing this protocol will provide descrambling services for.

#### - (int) descrambleWMDRMForPlayer: (NXPlayer ∗ )playerinputBuffer:(unsigned char ∗ )pInputBuffer inputBufferSize:(unsigned int)uiInputBufferSizeoutputBuffer:(unsigned char ∗ )pOutputBuffer outputBufferSize:(unsigned int ∗ )puiOutputBufferSizeinitialVector:(unsigned char ∗ )pIVBuffer initialVectorSize:(unsigned int)dwIVBufferSize

Descrambles WM-DRM content.

The type of data passed for descrambling depends on the value that was returned by DRMType, but can be either packet data or payload data.


**Parameters**

| i/o  | Name  | Description  | 
|---|---|---|
| in | player | The calling NXPlayer instance. |
| in | pInputBuffer | The data to be descrambled |
| in | uiInputBufferSize | The size of the data, in bytes |
| out | pOutputBuffer | The location at which to place the descrambled output data. This may point to the same location as the input buffer, or it may point to a separate location. The size available for the output buffer is the same as the size of the input buffer. That is, the descrambled data may be smaller than the original data, but not larger. |
| out | puiOutputBufferSize | The size of the descrambled data. The callback must set this value. This may be equal to or smaller thanuiInputBufferSize, but not larger. |
| in | pIVBuffer | The initialization vector. dwIVBufferSize The size (in bytes) of the initialization vector. |

**Returns**

The method should return zero if the data was successfully descrambled. In the case of an error, it should
return -1.

#### - (NXDRMType) DRMType

Returns a value indicating the type of DRM that the descrambling method expects.

This may be NXDRMTypePayload or NXDRMTypePacket (NXDRMTypeFrame is not supported).
