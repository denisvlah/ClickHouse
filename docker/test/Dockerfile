FROM ubuntu:17.10

ARG repository="deb http://repo.yandex.ru/clickhouse/deb/stable/ main/"
ARG version=\*

RUN apt-get update && \
    apt-get install -y apt-transport-https dirmngr && \
    mkdir -p /etc/apt/sources.list.d && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv E0C56BD4 && \
    echo $repository | tee /etc/apt/sources.list.d/clickhouse.list && \
    apt-get update && \
    apt-get install --allow-unauthenticated -y clickhouse-test && \
    rm -rf /var/lib/apt/lists/* /var/cache/debconf && \
    apt-get clean

# clickhouse-test bug: it doesn't start without server config, remove after release 1.1.54372 :
RUN mkdir -p /etc/clickhouse-server && echo "<y></y>" > /etc/clickhouse-server/config.xml

ENTRYPOINT ["/usr/bin/clickhouse-test"]
