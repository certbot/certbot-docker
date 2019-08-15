# Docker Arch (amd64, arm32v6, ...)
ARG TARGET_ARCH
FROM certbot/cerbot:${TARGET_ARCH}-v0.37.1

# Qemu Arch (x86_64, arm, ...)
ARG QEMU_ARCH
ENV QEMU_ARCH=${QEMU_ARCH}
COPY qemu-${QEMU_ARCH}-static /usr/bin/

ARG PLUGIN_NAME

# Retrieve Certbot DNS plugin code
RUN wget -O certbot-${CERTBOT_VERSION}.tar.gz https://github.com/certbot/certbot/archive/v${CERTBOT_VERSION}.tar.gz \
 && tar xf certbot-${CERTBOT_VERSION}.tar.gz \
 && cp -r certbot-${CERTBOT_VERSION}/certbot-${PLUGIN_NAME} /opt/certbot/src/certbot-${PLUGIN_NAME} \
 && rm -rf certbot-${CERTBOT_VERSION}.tar.gz certbot-${CERTBOT_VERSION}

# Install the DNS plugin
RUN pip install --constraint /opt/certbot/docker_constraints.txt --no-cache-dir --editable /opt/certbot/src/certbot-${PLUGIN_NAME}
