# Kafka and Zookeeper

#FROM java:openjdk-8-jre
FROM ppc64le/openjdk:8-jre

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 2.0.0
#http://apache.mirrors.spacedump.net/kafka/2.0.0/kafka_2.11-2.0.0.tgz

ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper and other needed things
RUN apt-get update && \
    apt-get install -y zookeeper wget supervisor dnsutils procps net-tools vim mc tree nano less strace traceroute ifstat man && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    echo "" && \
    curl http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -o /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    echo "" && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    ln -s "$KAFKA_HOME" /opt/kafka && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

ADD files/.bashrc /root/.bashrc
# Supervisor config
ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
