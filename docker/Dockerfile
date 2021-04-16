FROM python:3.8.6-slim-buster as compile

RUN apt-get update -yy && \
    apt-get install -yy \
        build-essential \
        pkg-config \
#        avahi-daemon \
#        avahi-discover \
#        avahi-utils \
#        libnss-mdns \
#        dnsutils \
#        libffi-dev \
        alsa-utils \
        libavformat-dev \
        libavcodec-dev \
        libavdevice-dev \
        libavutil-dev \
        libavfilter-dev \
        libswscale-dev \
        libswresample-dev \
		libsamplerate-dev \ # for alsa dsp 
		libfftw3-dev \ # for alsa dsp 
        libasound2-dev \
        libssl-dev \
        libffi-dev \
        python3-dev \
        cargo

COPY ap2-receiver.py /airplay2/ap2-receiver.py
COPY ap2 /airplay2/ap2
COPY requirements.txt /airplay2/requirements.txt

RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN pip3 install -r /airplay2/requirements.txt

FROM python:3.8.6-slim-buster as build

RUN apt-get update -yy && \
    apt-get install -yy --no-install-recommends \
        avahi-daemon \
        avahi-discover \
        avahi-utils \
        libnss-mdns \
        dnsutils \
#        libffi-dev \
        alsa-utils \
#       libavformat-dev \
#       libavcodec-dev \
       libavdevice-dev \
#       libavutil-dev \
       libavfilter-dev \
       libswscale-dev \
       libswresample-dev \
#	   libsamplerate-dev
#       libasound2-dev 


COPY --from=compile /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY ap2-receiver.py /airplay2/ap2-receiver.py
COPY ap2 /airplay2/ap2

COPY docker/avahi-daemon.conf /etc/avahi/avahi-daemon.conf
COPY docker/start.sh /

RUN chmod +x /start.sh

CMD ["/start.sh"]
