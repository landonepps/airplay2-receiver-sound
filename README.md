# Experimental Airplay 2 (forked with sound)

Very quick python implementation of AP2 protocol using **minimal multi-room** features -- built and originally created by https://github.com/openairplay/airplay2-receiver


![IMG_489B6A3DA261-1](https://user-images.githubusercontent.com/48214337/117120989-55222c00-ad94-11eb-9520-2e22e601eb45.jpeg)


## So what's this fork for? Any big changes?

Nope, not really - little changes enabled **Streaming Audio to receiver with AirPlay 2**, the only difference to the beloved original.


**New and old Features related to sound**:

- Individual volume control from the sending device
- Set Latency / Delay to match playing speed with physical devices
- Connect with multiple virtual-receiver devices
- 

Tested with Sound: macOS 11.14 (Silicon Mac) / macOS 10.14 (built 2012) on Python 3.9
Tested pairing: Apple TV to virtual speaker,  


## Optimization and known issues

I wont be able to fix them but let you know

- Always begin streaming first to virtual and then physical devices, otherwise its likely to fail

- Multiple instances of virtual-receivers hosted on the same device won't work and mess mdns up

- Make sure you have 'pyaudio' and 'virtualenv' already installed & built before running any command

- Always enter the 'virtualenv' before starting AirPlay, without it the connection will break even if the device is visible



## Installation and Options (macOS)

**For Windows & Raspberry Pi check out the original code**

http://github.com - automatic!
[GitHub](http://github.com)

https://github.com/openairplay/airplay2-receiver/blob/master/README.md#raspberry-pi-4

* brew install python3  
* brew install portaudio
brew install virtualenv
brew install pyaudio

**Start receiver with this command:**

> virtualenv -p /usr/local/bin/python3 proto
> source proto/bin/activate

* pip install -r requirements.txt 
* pip install --global-option=build_ext --global-option="-I/usr/local/Cellar/portaudio/19.6.0/include" --global-option="-L/usr/local/Cellar/portaudio/19.6.0/lib" 
* pyaudio

> python ap2-receiver.py -m SpeakerName --netiface=en1



## Details that didn't changed from original

Tested on Python 3.7.5 / macOS 10.15.2 with iPhone X 13.3 and Raspberry Pi 4

- HomeKit transient pairing (SRP/Curve25519/ChaCha20-Poly1305)
- FairPlay (v3) authentication
- Receiving of both REALTIME and BUFFERED Airplay2 audio streams
- Airplay2 Service publication
- Decoding of ALAC/44100/2 or AAC/44100/2

Protocol notes > https://emanuelecozzi.net/docs/airplay2

