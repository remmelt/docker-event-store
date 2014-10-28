FROM debian:sid

MAINTAINER Remmelt Pit <remmelt@remmelt.com>

# Install wget
RUN apt-get update -qq \
    && apt-get install -yqq wget \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/*

# Install mono
RUN apt-get update -qq \
    && apt-get install -yqq mono-complete
    && apt-get autoclean
    && rm -rf /var/lib/apt/lists/*

#Install the Event Store
ENV EVENT_STORE_DIR /var/eventstore
ENV EVENT_STORE_VERSION EventStore-OSS-Linux-v3.0.1

RUN mkdir -p $EVENT_STORE_DIR
WORKDIR $EVENT_STORE_DIR
RUN (wget -qO- http://download.geteventstore.com/binaries/$EVENT_STORE_VERSION.tar.gz | tar zx)

WORKDIR $EVENT_STORE_DIR/$EVENT_STORE_VERSION

ADD run-node.sh $EVENT_STORE_DIR/$EVENT_STORE_VERSION/run-node.sh
RUN chmod +x $EVENT_STORE_DIR/$EVENT_STORE_VERSION/run-node.sh

VOLUME ["/db", "/logs"]
EXPOSE 1113 2113

ENTRYPOINT ["./run-node.sh", \
            "--db", "/db", \
            "--log", "/logs", \
            "--ext-ip=0.0.0.0", \
            "--http-prefixes=http://*:2113/"]
