
---
title: Set the Voice Changer and Reverberation Effects
description: How to adjust pitch and tone on Windows
platform: Windows
updatedAt: Sun Sep 29 2019 08:20:06 GMT+0800 (CST)
---
# Set the Voice Changer and Reverberation Effects
## Introduction 

In social and entertainment scenarios, users often need various voice effects to enhance interactive experiences. Agora provides multiple preset voice changers and reverberation effects. You can also flexibly change the users' voice, such as adjusting the pitch and setting the equalization and reverberation modes.

## Implementation

Before proceeding, ensure that you implement a basic call or live broadcast in your project. See [Start a Call](../../en/Audio%20Broadcast/start_call_windows.md) or [Start a Live Broadcast](../../en/Audio%20Broadcast/start_live_windows.md) for details.

### Use a preset voice changer and reverberation effect

You can use one of the following preset voice changer options by calling  `setLocalVoiceChanger`:

- An old man's voice.
- A little boy's voice.
- A little girl's voice.
- Zhu Bajie's voice (Zhu Bajie is a character from Journey to the West who has a voice like a growling bear).
- Ethereal vocal effects.
- Hulk's voice.

You can use one of the following preset reverberation effects by calling `setLocalVoiceReverbPreset`:

- Pop music
- R&B
- Rock music
- Hip-hop
- Pop concert
- Karaoke
- Recording studio

```c++
// Initialize objects
RtcEngineParameters rep(*m_lpAgoraEngine);
VOICE_CHANGER_PRESET voiceChanger;
AUDIO_REVERB_PRESET reverbPreset;

// Set the voice changer as old man
voiceChanger = VOICE_CHANGER_OLDMAN;
rep.setLocalVoiceChanger(voiceChanger);

// Turn off the voice changer
voiceChanger = VOICE_CHANGER_OFF;
rep.setLocalVoiceChanger(voiceChanger);

// Set the reverberation effect as pop
reverbPreset = AUDIO_REVERB_POPULAR;
rep.setLocalVoiceReverbPreset(reverbPreset);

// Turn off the reverberation effect
reverbPreset = AUDIO_REVERB_OFF;
rep.setLocalVoiceReverbPreset(reverbPreset);
```

### Customize the voice effects

You can also customize the voice effects by adjusting the voice pitch, equalization, and reverberation settings.

The following sample code shows how to change from the original voice to Hulk's voice.

```c++
// Initialization
RtcEngineParameters rep(*lpAgoraEngine);

// Sets the pitch. The value ranges between 0.5 and 2.0. The lower the value, the lower the pitch. The default value is 1.0, which is the original pitch.
int nRet = rep.setLocalVoicePitch(0.5);

// Sets the local voice equalization.
// The first parameter sets the band frequency. The value ranges between 0 and 9. Each value represents the center frequency of the band: 31, 62, 125, 250, 500, 1k, 2k, 4k, 8k, and 16k Hz
// The second parameter sets the gain of each band. The value ranges between -15 and 15 dB. The default value is 0.
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_31, -15);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_62, 3);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_125, -9);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_250, -8);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_500, -6);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_1K, -4);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_2K, -3);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_4K, -2);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_8K, -1);
nRet = rep.setLocalVoiceEqualization(AUDIO_EQUALIZATION_BAND_16K, 1);

// The level of the dry signal in dB. The value ranges between -20 and 10.
nRet = rep.setLocalVoiceReverb(AUDIO_REVERB_DRY_LEVEL, 10);

// The level of the early reflection signal (wet signal) in dB. The value ranges between -20 and 10.
nRet = rep.setLocalVoiceReverb(AUDIO_REVERB_WET_LEVEL, 7);

// The room size of the reverberation. A larger room size means a stronger reverberation. The value ranges between 0 and 100.
nRet = rep.setLocalVoiceReverb(AUDIO_REVERB_ROOM_SIZE, 6);

// The length of the initial delay of the wet signal (ms). The value ranges between 0 and 200.
nRet = rep.setLocalVoiceReverb(AUDIO_REVERB_WET_DELAY, 124);

// The reverberation strength. The value ranges between 0 and 100. The higher the value, the stronger the reverberation.
nRet = rep.setLocalVoiceReverb(AUDIO_REVERB_STRENGTH, 78);
```

### API reference

- [`setLocalVoicePitch`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a1fef48b6aa3954d7e76164a43d660b94)
- [`setLocalVoiceEqualization`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#a3de79ba906e6b254b997eda4d395d052)
- [`setLocalVoiceReverb`](https://docs.agora.io/en/Audio%20Broadcast/API%20Reference/cpp/classagora_1_1rtc_1_1_rtc_engine_parameters.html#aa00e903b1cc6f2752373afbe556ef456)

## Considerations

The API methods have return values. If the method call fails, the return value is < 0.