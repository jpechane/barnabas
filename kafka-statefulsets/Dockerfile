FROM fedora:25

RUN dnf -y install which java-1.8.0-openjdk libaio python gettext hostname iputils wget && dnf clean all -y

# set Scala and Kafka version
ENV SCALA_VERSION=2.11
ENV KAFKA_VERSION=0.11.0.0
# set Kafka home folder
ENV KAFKA_HOME=/opt/kafka

# Set from build args
ARG version=latest
ENV VERSION ${version}

# downloading/extracting Apache Kafka
RUN wget http://www.eu.apache.org/dist/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz

RUN mkdir $KAFKA_HOME \
    && tar xvfz kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz -C $KAFKA_HOME --strip-components=1

WORKDIR $KAFKA_HOME

# copy template configuration files
COPY ./config/zookeeper.properties.template $KAFKA_HOME/config/
# copy scripts for starting Kafka
COPY ./scripts/ $KAFKA_HOME
