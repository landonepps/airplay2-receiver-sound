# About this fork
This fork replaces pyaudio / portaudio with [alsaaudio](http://larsimmisch.github.io/pyalsaaudio/]). This was done because portaudio (and therefore pyaudio) does not seem to function correctly on the Raspberry Pi 4. This has the consequence of breaking Windows/macOS support.

# Experimental

Very quick python implementation of AP2 protocol using **minimal
multi-room** features. For now it implements:
- HomeKit transient pairing (SRP/Curve25519/ChaCha20-Poly1305)
- FairPlay (v3) authentication
- Receiving of both REALTIME and BUFFERED Airplay2 audio streams
- Airplay2 Service publication
- Decoding of all Airplay2 supported CODECs: ALAC, AAC, OPUS, PCM.
 Ref: [here](https://emanuelecozzi.net/docs/airplay2/audio/) and 
      [here](https://emanuelecozzi.net/docs/airplay2/rtsp/#setup)
- Output latency compensation for sync with other Airplay receivers

For now it does not implement:
 - MFi Authentication / FairPlay v2 (one of them is required by iTunes/Windows)
 - Audio Sync
 
**This code is experimental. This receiver do not expect to be a real receiver but a toolbox for learning/debugging all airplay protocols and related pairing/authentication methods.** 

Latest additions:
 - Implement RTP buffer (manage FLUSHBUFFERED) : play/pause/timeline/playlist

Next steps:
 - PTP (Precision Time Protocol)
 - Remove all os specific code (Soft Volume management)
 - Sender (branch-sender) - Implementation
 - Implement RSA Authentication
 - Raspbian package
 - DACP/(+MRP?) Support
 - FairPlay v2 Support
---

## Raspberry Pi 4

Install docker and then build the image:

```zsh
docker build -f docker/Dockerfile -t invano/ap2-receiver .
```

To run the receiver:

```zsh
docker run -it --rm --device /dev/snd --net host invano/ap2-receiver
```

Default network device is wlan0, you can change this with AP2IFACE env variable:

```zsh
docker run -it --rm --device /dev/snd --env AP2IFACE=eth0 --net host invano/ap2-receiver
```

## macOS Catalina

Not supported 

## Windows

Not supported


---

Tested on Python 3.7.5 / macOS 10.15.2 with iPhone X 13.3 and Raspberry Pi 4

### Protocol notes

https://emanuelecozzi.net/docs/airplay2

 
