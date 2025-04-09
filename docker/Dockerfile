ARG ARCH
ARG VERSION
ARG VARIANT

#FROM scratch:${VERSION}

FROM debian:bookworm
RUN apt-get update && apt-get install -y --no-install-recommends \
	libgl1 \
	libxkbcommon0 \
	libxkbcommon-x11-0 \
	libxcb-icccm4 \
	libxcb-keysyms1 \
	libxcb-shape0 \
	libegl1 \
	libfontconfig1 \
	libdbus-1-3 \
	libxcb1 \
	libsm6 \
	libxcb-cursor0 \
	libgstreamer-plugins-base1.0 \
	libgstreamer1.0-0 \
	locales && \
	sed -i "s/# en_US.UTF-8/en_US.UTF-8/" /etc/locale.gen && locale-gen && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	apt-get auto-remove -y

# Set UTF-8 locale
ENV LANG=en_US.UTF-8 \
	LANGUAGE=en_US:en \
	LC_ALL=en_US.UTF-8

ARG FILENAME="URL"
ADD $FILENAME /opt/mvtec/
RUN chmod -R o=u /opt/mvtec/*

 
ARG ARCH
ARG VERSION
ARG VARIANT

RUN [ ! -z "${ARCH}" ]
RUN [ ! -z "${VERSION}" ]

ADD entrypoint.sh .
RUN chmod a+rx entrypoint.sh
ENTRYPOINT ["./entrypoint.sh"]
