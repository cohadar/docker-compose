FROM alpine AS build-stage
WORKDIR /opt
ENV _SCALA_VERSION=2.12
ENV _KAFKA_VERSION=2.1.1
COPY "kafka_${_SCALA_VERSION}-${_KAFKA_VERSION}.tgz" /opt/
RUN tar xzf "kafka_${_SCALA_VERSION}-${_KAFKA_VERSION}.tgz"
RUN mv "kafka_${_SCALA_VERSION}-${_KAFKA_VERSION}" kafka
###############################################################################
FROM alpine
COPY --from=build-stage /opt/kafka/ /opt/kafka/

## we need bash for kafka startup scripts and jre for kafka
RUN apk add --no-cache dumb-init bash openjdk8-jre-base openssl
WORKDIR /opt

##
WORKDIR /opt/kafka/bin
RUN mkdir -p /data/kafka

##
ENTRYPOINT ["/opt/kafka/bin/kafka-server-start.sh", "/etc/kafka/conf/server.properties"]
