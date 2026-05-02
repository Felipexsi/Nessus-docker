FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl \
    libssl3 \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL \
    "https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.7.4-ubuntu1404_amd64.deb" \
    -o /tmp/nessus.deb \
    && dpkg -i /tmp/nessus.deb \
    && rm -f /tmp/nessus.deb

RUN mkdir -p /opt/nessus/var/nessus/logs

EXPOSE 8834

HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=3 \
    CMD curl -fsk https://localhost:8834/ || exit 1

CMD ["/opt/nessus/sbin/nessusd", "-D"]
