## in build stage we unzip zookeeper archive
FROM alpine AS build-stage
WORKDIR /tmp
COPY zookeeper-3.4.13.tar.gz /tmp
RUN tar xzf zookeeper-3.4.13.tar.gz && rm zookeeper-3.4.13.tar.gz
RUN mv zookeeper-3.4.13 /opt/zookeeper

###############################################################################
FROM alpine
## copy app from build stage
COPY --from=build-stage /opt/zookeeper/ /opt/zookeeper/

## create zookeeper user
## for security reasons always use random id: echo $RANDOM
RUN addgroup -g 24170 zookeeper
RUN adduser -D -H -u 24170 -G zookeeper zookeeper
RUN chown -R zookeeper:zookeeper /opt/zookeeper

## install zookeeper dependencies
RUN apk update && apk add bash openjdk8-jre-base

## user, workdir & ports
USER zookeeper
WORKDIR /opt/zookeeper/
EXPOSE 2181 2888 3888

## start the server
ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh", "start-foreground"]
