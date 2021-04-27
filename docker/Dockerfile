FROM python:3.8.6-slim-buster as compile

RUN apt-get update -yy && \
    apt-get install -yy \
        build-essential \
        pkg-config \
        alsa-utils \
        libavformat-dev \
        libavcodec-dev \
        libavdevice-dev \
        libavutil-dev \
        libavfilter-dev \
        libswscale-dev \
        libswresample-dev \
        libasound2-dev \
        libssl-dev \
        libffi-dev \
        python3-dev \
        cargo

# Add ACDF plugin for alsa ladspa equalization
RUN apt-get install -yy \
		ladspa-sdk \
		curl

RUN curl -LO "http://audio.claub.net/software/LADSPA/ACDF_v3.tar"
RUN tar -xf ACDF_v3.tar
WORKDIR ACDF_v3
RUN make
WORKDIR /
# 

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
		alsa-utils \
		libavdevice-dev \
		libavfilter-dev \
		libswscale-dev \
		libswresample-dev

COPY --from=compile /opt/venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY ap2-receiver.py /airplay2/ap2-receiver.py
COPY ap2 /airplay2/ap2
COPY ACDF_v3/ACDf.so /usr/lib/ladspa/ACDf.so

COPY docker/avahi-daemon.conf /etc/avahi/avahi-daemon.conf
COPY docker/start.sh /

RUN chmod +x /start.sh

CMD ["/start.sh"]
