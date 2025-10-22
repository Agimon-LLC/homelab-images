FROM debian:bullseye-slim

LABEL maintainer="Agimon Homelab <homelab@agimon.com>"
LABEL org.opencontainers.image.source="https://github.com/Agimon-LLC/homelab-images"

RUN apt-get update && apt-get install -y curl gnupg lsb-release \
    && curl -s https://repo.proxysql.com/ProxySQL/repo_pub_key | apt-key add - \
    && echo "deb https://repo.proxysql.com/ProxySQL/proxysql-2.6.x/$(lsb_release -sc)/ ./ " > /etc/apt/sources.list.d/proxysql.list \
    && apt-get update && apt-get install -y proxysql \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 6032 6033
ENTRYPOINT ["/bin/sh", "-c", "/usr/bin/proxysql -f \"$@\"", "--"]