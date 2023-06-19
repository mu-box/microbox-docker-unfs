FROM mubox/base

# Create directories
RUN mkdir -p /var/log/gomicro

ARG TARGETPLATFORM
COPY ${TARGETPLATFORM}/unfs3-0.9.22-r6.apk /root/unfs3.apk

RUN apk add --virtual .unfs --allow-untrusted --no-cache rpcbind nfs-utils rsync flex /root/unfs3.apk

RUN gem install remote_syslog_logger

RUN ln -s /data/var/db/unfs /app

RUN mkdir -p /opt/microbox/hooks /var/microbox && \
    get-hooks unfs

WORKDIR /app
