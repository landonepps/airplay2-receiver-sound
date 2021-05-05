# Experimental (forked with sound)

Very quick python implementation of AP2 protocol using **minimal
multi-room** features. For now it implements:


- Volume control

Tested with Sound: macOS 11.14 (Silicon Mac) / macOS 10.14 (built 2012) on Python 3.9

**This code is experimental. This receiver do not expect to be a real receiver but a toolbox for learning/debugging all airplay protocols and related pairing/authentication methods.** 


## Known tricks and issues
I wont be able to fix them but let you know

- Make sure you have 'pyaudio' and 'virtualenv' already installed before everything else
- 
- Start streaming to the virtual receiver and then to other devices enhances latency / quality
-   



## Installation and remaining

On macOS go along with these commands:

brew install python3
brew install portaudio
virtualenv -p /usr/local/bin/python3 proto
source proto/bin/activate
pip install -r requirements.txt
pip install --global-option=build_ext --global-option="-I/usr/local/Cellar/portaudio/19.6.0/include" --global-option="-L/usr/local/Cellar/portaudio/19.6.0/lib" pyaudio

python ap2-receiver.py -m myap2 --netiface=en0


(Lookup installation for Raspberry Pi & Windows)



### Unchanged from original fork

Tested on Python 3.7.5 / macOS 10.15.2 with iPhone X 13.3 and Raspberry Pi 4

- HomeKit transient pairing (SRP/Curve25519/ChaCha20-Poly1305)
- FairPlay (v3) authentication
- Receiving of both REALTIME and BUFFERED Airplay2 audio streams
- Airplay2 Service publication
- Decoding of ALAC/44100/2 or AAC/44100/2

### Protocol notes

https://emanuelecozzi.net/docs/airplay2

