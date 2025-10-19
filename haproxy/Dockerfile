# homelab HAProxy image for Percona XtraDB Cluster
FROM haproxy:2.8

LABEL maintainer="ray@agimon.com" \
      org.opencontainers.image.source="https://github.com/Agimon-LLC/homelab-images" \
      description="Custom HAProxy image for Percona XtraDB Cluster in Agimon homelab"

# Ensure the entrypoint matches what the Percona Operator expects
RUN mkdir -p /usr/local/bin && \
    echo '#!/bin/sh' > /usr/local/bin/run.sh && \
    echo 'set -e' >> /usr/local/bin/run.sh && \
    echo 'if [ -f /etc/haproxy/haproxy.cfg ]; then' >> /usr/local/bin/run.sh && \
    echo '  echo "[INFO] Starting HAProxy with provided configuration..."' >> /usr/local/bin/run.sh && \
    echo '  exec haproxy -f /etc/haproxy/haproxy.cfg -db' >> /usr/local/bin/run.sh && \
    echo 'else' >> /usr/local/bin/run.sh && \
    echo '  echo "[WARN] /etc/haproxy/haproxy.cfg not found - waiting for Percona operator"' >> /usr/local/bin/run.sh && \
    echo '  sleep 5; exec haproxy -f /usr/local/etc/haproxy/haproxy.cfg -db' >> /usr/local/bin/run.sh && \
    echo 'fi' >> /usr/local/bin/run.sh && \
    chmod +x /usr/local/bin/run.sh

CMD ["/usr/local/bin/run.sh"]
