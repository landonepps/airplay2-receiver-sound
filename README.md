# About this fork
This fork replaces pyaudio / portaudio with [alsaaudio](http://larsimmisch.github.io/pyalsaaudio/]). This was done because portaudio (and therefore pyaudio) does not seem to function correctly on the Raspberry Pi 4. This has the consequence of breaking Windows/macOS support.

* The volume control uses alsaaudio's mixer object.
* There is an equalizer plugin included. To use the plugin, create a .asoundrc file and map it into the container with `-v /path/to/asoundrc:/root/.asoundrc`. [See this stack exchange post](https://dsp.stackexchange.com/a/74760/57001) for instructions on creating a multiband equalizer with the ACDf ladspa / alsa plugin.
* The dockerfile is a multistage build, which reduces the image size by roughly 50%

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

# Experimental Airplay 2 (forked with working sound)

> Very quick python implementation of AP2 protocol using **minimal multi-room** features created by [openairplay](https://github.com/openairplay/airplay2-receiver)

With only little changes made from the original, it showcases **streaming Audio to/from virtual-receiver devices with AirPlay 2** for learning/debugging/playing in an easy, reproducible and working way.

![IMG_489B6A3DA261-1](https://user-images.githubusercontent.com/48214337/117120989-55222c00-ad94-11eb-9520-2e22e601eb45.jpeg)




## Features and possibilities

- Create a virtual device receiving AirPlay 2 streams and plays them 

- Config latency/delay to match playing speed of other devices

- Control speaker volume individually from the streaming device

- Connect with multiple virtual-receiver devices and otherwise

To load the equalizer, map an asoundrc file:
```zsh
docker run -it --rm --device /dev/snd -v ~/my_asoundrc:/root/.asoundrc  --env AP2IFACE=eth0 --net host invano/ap2-receiver
```

## macOS Catalina

Not supported 

## Windows

Not supported




**I won't be able to fix them, but let you know ...**

- Always begin streaming first to virtual and then physical devices, otherwise it's likely to fail

- Multiple instances of virtual receivers hosted on the same device won't work and mess mdns up

- Always requires the 'virtualenv', without the connection will break (even if the device is visible correctly)

- Make sure you have 'pyaudio' and 'virtualenv' installed & built files before setting the receiver up

- Rarely an earlier closed connection prevents you from reconnecting, try `sudo killall -HUP mDNSResponder` to reset this behaviour



**Working pairings and cases**
* ☑️ iOS device streaming on multiple AP2 speakers
* ☑️ iOS device streaming directly
* ☑️ Control volume/playstate when in group
* ❌ HomePod streaming directly (standalone)
* ☑️ Mac streaming directly (single device)
* ❌ Streaming out of iTunes in general


**Devices tested with sound/airplaying**
* Silicon Mac (M1) - macOS 11.14 - Python 3.9
* Apple Mac - macOS 10.15 - Python 3.7.5
* iMac from 2012 - macOS 10.14 - Python 3.8



## Installation and usage (macOS)

Find installation for **[Windows](https://github.com/openairplay/airplay2-receiver/blob/master/README.md#windows) & [Raspberry Pi](https://github.com/openairplay/airplay2-receiver/blob/master/README.md#raspberry-pi-4)** in the original code.

```zsh
docker run -it --rm --device /dev/snd --net host invano/ap2-receiver
```
brew install python3  
brew install portaudio
brew install virtualenv
brew install pyaudio
```

Default network device is wlan0, you can change this with AP2IFACE env variable:
Start virtual receiver target:

```zsh
docker run -it --rm --device /dev/snd --env AP2IFACE=eth0 --net host invano/ap2-receiver
```

```zsh
virtualenv -p /usr/local/bin/python3 proto
source proto/bin/activate
pip install -r requirements.txt 
pip install --global-option=build_ext --global-option="-I/usr/local/Cellar/portaudio/19.6.0/include" --global-option="-L/usr/local/Cellar/portaudio/19.6.0/lib" 
pyaudio

python ap2-receiver.py -m SpeakerName --netiface=en1
```

**Many many thanks to [openairplay](https://github.com/openairplay/airplay2-receiver) for creating and maintaining this project!**

## Details that didn't change from original

- HomeKit transient pairing (SRP/Curve25519/ChaCha20-Poly1305)
- FairPlay (v3) authentication
- Receiving of both REALTIME and BUFFERED Airplay2 audio streams
- Airplay2 Service publication
- Decoding of ALAC/44100/2 or AAC/44100/2

Protocol notes > https://emanuelecozzi.net/docs/airplay2
