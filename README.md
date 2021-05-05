# Experimental Airplay 2 (forked with sound)

> Very quick python implementation of AP2 protocol using **minimal multi-room** features 
> - built and originally created by [openairplay](https://github.com/openairplay/airplay2-receiver)


![IMG_489B6A3DA261-1](https://user-images.githubusercontent.com/48214337/117120989-55222c00-ad94-11eb-9520-2e22e601eb45.jpeg)

With only little changes made from the original, it showcases **streaming Audio to/from virtual-receiver devices with AirPlay 2** for learning/debugging/playing in an easy, reproduceable and working way.


## Features and possibilities

- Create a virtual device receiving AirPlay 2 streams and plays them 

- Config latency / delay to match playing speed of other devices

- Control speaker volume individually from the streaming device

- Connect with multiple virtual-receiver devices and otherwise


**I won't be able to fix them, but let you know ...**


- Always begin streaming first to virtual and then physical devices, otherwise its likely to fail

- Multiple instances of virtual-receivers hosted on the same device won't work and mess mdns up

- Always requires the 'virtualenv', without the connection will break (even if the device is visible correctly)

- Make sure you have 'pyaudio' and 'virtualenv' installed & built files before setting the receiver up

- Rarely an earlier closed connection prevents you from reconnecting, try `sudo killall -HUP mDNSResponder` to reset this behaviour


**Tested devices & pairings**


- [x] iOS device + other AirPlay 2 speakers
- [x] HomePod streaming direct (standalone)
- [☑️] iOS device streaming directly
- [ ] h#
- [ ] 
- h


* macOS 11.14 (Silicon Mac) 
* iMac (built 2012) - macOS 10.14 - Python 3.9

Tested pairing: Apple TV to virtual speaker,  


## Installation and usage (macOS)

Find installation for **[Windows](https://github.com/openairplay/airplay2-receiver/blob/master/README.md#windows) & [Raspberry Pi](https://github.com/openairplay/airplay2-receiver/blob/master/README.md#raspberry-pi-4)** in the original code.


```
brew install python3  
brew install portaudio
brew install virtualenv
brew install pyaudio
```

Start virtual receiver target:

```
virtualenv -p /usr/local/bin/python3 proto
source proto/bin/activate
pip install -r requirements.txt 
pip install --global-option=build_ext --global-option="-I/usr/local/Cellar/portaudio/19.6.0/include" --global-option="-L/usr/local/Cellar/portaudio/19.6.0/lib" 
pyaudio

python ap2-receiver.py -m SpeakerName --netiface=en1
```



## Details that didn't changed from original

Tested on Python 3.7.5 / macOS 10.15.2 with iPhone X 13.3 and Raspberry Pi 4

- HomeKit transient pairing (SRP/Curve25519/ChaCha20-Poly1305)
- FairPlay (v3) authentication
- Receiving of both REALTIME and BUFFERED Airplay2 audio streams
- Airplay2 Service publication
- Decoding of ALAC/44100/2 or AAC/44100/2

Protocol notes > https://emanuelecozzi.net/docs/airplay2

