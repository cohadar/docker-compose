## Using the best alpine+java base image I could find
## https://hub.docker.com/r/anapsix/alpine-java/
FROM alpine AS build-stage
WORKDIR /tmp
COPY zookeeper-3.4.13.tar.gz /tmp
RUN tar xzf zookeeper-3.4.13.tar.gz && rm zookeeper-3.4.13.tar.gz
RUN mv zookeeper-3.4.13 /opt/zookeeper
###############################################################################
FROM alpine
COPY --from=build-stage /opt/zookeeper/ /opt/zookeeper/

## workdir & ports
WORKDIR /opt/zookeeper/
EXPOSE 2181 2888 3888

## conf data volume
VOLUME ["/opt/zookeeper/conf"]

## start the server
ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh", "start-foreground"]
