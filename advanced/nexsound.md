# NexSound

NexSound API allow you to control several features of the player.

## PlaybackRate

#### - NXError setPlaybackRate(float playRate);

This method is used to change the playback rate.

This method makes it possible to allow users to adjust the playback rate, from 0.1 of the original speed to 4x speed, by changing the value of the parameter.
For example, to play content at half-speed, playRate should be set to 0.5

This method doesn't work if it is called when NexPlayer is stopped.

The playRate float parameter represents the rate by which to change the playback rate.  
It must be in the range of 0.1 to 4.0, which adjusts the playback speed from 0.1x to 4x the original speed of the content with **HW** decoder.  
It must be in the range of 0.1 to 2.0, which adjusts the playback speed from 0.1x to 2x the original speed of the content with **SW** decoder.  
It must be in the range of 0.5 to 2.0, when you use **AirPlay** mode. (isAirPlayActive is YES)

When using this method with HLS or Smooth Streaming content, playing multitrack content may cause unstable performance.  
Therefore, playing content as a single track is encouraged.  
When using this method with Live content, buffering may occur more frequently.

## Pitch
#### - NXError setAudioPitch(int value);

This method is used to change the pitch of the content.

This method allows int parameters from -12 to 12, Negative values for low pitch, and positive values for high pitch.

## Resampler
#### - NXError setResamplerParamCommand(int paramCommand, int value);

- **Input Sampling Rate**: paramCommand 56, value (1, 384.000)
- **Input Channels**: paramCommand 57, value (1, 6)
- **Output Sampling Rate**: paramCommand 59, value (1, 384.000)
- **Quality Level**: paramCommand 61, value (0, 3)


## MaxVolume
#### - NXError setMaxVolumeParamCommand(int paramCommand, int volume);

This method allows to set different effects on max volume, which are:

- **Max Volume Strength**: paramCommand 21
- **Max Volume Release**: paramCommand 22
- **Make Up Volume**: paramCommand 23
- **Max Volume Threshold**: paramCommand 24
- **Max Volume High Cut Frequency**: paramCommand 25

This features automatically maintains a constant volume level for all different kinds of sound sources such as movies, music, or mobile TV.

## Sound Effect
#### - NXError setSoundEffectParamCommand(int paramCommand, int value);

This method allows to set different effects on playback audio. The available effects are:

- **Ear confort**: param Command 0xF001, EarComfort mode moves the sound image to a position outside of the listener’s head, simulating the more comfortable feeling of listening to speakers but through earphones.
- **Live concert**: param Command 0xF002, Live concert mode adds reverb to audio
- **Stereo chorus**: param Command 0xF003
- **Music enhancer**: param Command 0xF004

## Sound Equalizer
#### - NXError setSoundEqualizerBand(int band, int paramCommand, int value);

Allows changing Gain (how much of the selected frequency is added or removed) and Q (the ratio of center frequency to bandwidth) for differents frequencies.

The allowed values for the frequencies are:  
- **64 hz**: band param value has to be 1.  
- **125 hz**: band param value has to be 2.  
- **250 hz**: band param value has to be 3.  
- **500 hz**: band param value has to be 4.  
- **1 kHz**: band param value has to be 5.  
- **2 kHz**: band param value has to be 6.  
- **4 kHz**: band param value has to be 7.  
- **8 kHz**: band param value has to be 8.  
- **16 kHz**: band param value has to be 9.  

Param command for Gain must be 71. And value for it should be between -12 and 12.  
Param command for Q must be 73. And value for it should be between 1 and 20.  





