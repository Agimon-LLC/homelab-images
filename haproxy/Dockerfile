# homelab HAProxy image for Percona XtraDB Cluster
FROM haproxy:2.8

LABEL maintainer="ray@agimon.com" \
      org.opencontainers.image.source="https://github.com/Agimon-LLC/homelab-images" \
      description="Custom HAProxy image for Percona XtraDB Cluster in Agimon homelab"

# Add a lightweight wrapper entrypoint script
RUN mkdir -p /usr/local/bin && \
    printf '%s\n' \
    '#!/bin/sh' \
    'set -e' \
    'if [ -f /etc/haproxy/haproxy.cfg ]; then' \
    '  echo "[INFO] Starting HAProxy with provided configuration..."' \
    '  exec haproxy -f /etc/haproxy/haproxy.cfg -db' \
    'else' \
    '  echo "[WARN] /etc/haproxy/haproxy.cfg not found - waiting for Percona operator"' \
    '  sleep 5' \
    '  exec haproxy -f /usr/local/etc/haproxy/haproxy.cfg -db' \
    'fi' \
    > /usr/local/bin/run.sh && \
    chmod +x /usr/local/bin/run.sh

CMD ["/usr/local/bin/run.sh"]
