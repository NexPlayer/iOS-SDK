# Dolby Audio Settings

NexPlayer provides various Dolby Audio settings that can be controlled using NexPlayer APIs. Please refer to `DolbyPlugin` class for the implementation.


###  Dolby Audio Postprocessing (DAP)

This configuration sets the Dolby Audio postprocessing (AC3 and AC4) on and off

### End point Configuration

Use the media player framework interface to indicate the active end point. The default end point is headphone.

Note: While changing to an external (Bluetooth) end point does not require a change to a Dolby Audio library setting, the system must do some processing (such as initialize the new device and enable the new audio path) so some additional mute may be unavoidable.

### Enhancement Gain 

Dialogue enhancement is postprocessing that improves dialogue intelligibility. 
 
The dialogue enhancement control monitors the audio being played, detects the presence of dialogue, and dynamically applies processing to improve the intelligibility of the spoken portion of a recording.

The Dialogue Enhancer is enabled by default and the dialogue enhancement gain is set to its default value 6. 


### Virtualizer

Turns on virtualization on or off. Virtulization is enabled by default.

Note: Virtualization must be enabled for Dolby Atmos Music content and is recommended for the
other Dolby Atmos content.

### Output reference level setting

Output reference level is the gain value that controls the output loudness of audio content.
The level control monitors the audio being played, and dynamically applies processing to adjust output signal at the target reference level.

The default output reference level is -14. 

### Presentation Index

Used to select which presentation to decode. The default value is 0, indicating that the Dolby Audio library selects the first decodable presentation in the bitstream to decode. This control is specific to only Dolby AC-4.

### Main ASSO Preference (Mix level setting)

When the selected presentation has two substreams, use this setting to configure 
the relative volumes of the main and associated programs.

The default mix level is -32. This control is specific to only Dolby AC-4.

