FROM alpine

LABEL maintainer="erik@coretechonomy.com"
LABEL version="1.0"

ENV prometheus_version 2.10.0

RUN adduser -s /bin/false -D -H prometheus \
    && adduser -s /bin/false -D -H node_exporter \
    && apk update \
    && apk --no-cache add curl \
    && curl -LO https://github.com/prometheus/prometheus/releases/download/v${prometheus_version}/prometheus-${prometheus_version}.linux-armv7.tar.gz \
    && tar -xvzf prometheus-${prometheus_version}.linux-armv7.tar.gz \
    && mkdir -p /etc/prometheus /var/lib/prometheus \
    && cp prometheus-${prometheus_version}.linux-armv7/promtool /usr/local/bin/ \
    && cp prometheus-${prometheus_version}.linux-armv7/prometheus /usr/local/bin/ \
    && cp -R prometheus-${prometheus_version}.linux-armv7/console_libraries/ /etc/prometheus/ \
    && cp -R prometheus-${prometheus_version}.linux-armv7/consoles/ /etc/prometheus/ \
    && rm -rf prometheus-${prometheus_version}.linux-armv7* \
    && chown prometheus:prometheus /usr/local/bin/prometheus \
    && chown prometheus:prometheus /usr/local/bin/promtool \
    && chown -R prometheus:prometheus /etc/prometheus \
    && chown prometheus:prometheus /var/lib/prometheus \
    && apk del curl

VOLUME /etc/prometheus

VOLUME /var/lib/prometheus

ADD conf/prometheus.yml /etc/prometheus/
ADD conf/alert.rules /etc/prometheus/

ENTRYPOINT /usr/local/bin/prometheus \ 
            --config.file /etc/prometheus/prometheus.yml \ 
            --storage.tsdb.path /var/lib/prometheus/ \
            --web.console.libraries=/usr/share/prometheus/console_libraries \
            --web.console.templates=/usr/share/prometheus/consoles

EXPOSE 9090