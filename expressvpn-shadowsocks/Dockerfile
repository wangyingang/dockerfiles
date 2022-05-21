FROM ubuntu:20.04

ENV EXPRESSVPN_DOWNLOAD_URL=https://www.download-express-apps.net/clients/linux/xv_3.23.1.0-1_amd64.deb
ENV EXPRESSVPN_CLIENT_VERSION=3.23.1.0
ENV EXPRESSVPN_CLIENT_BUILD=0
ENV SHADOWSOCKS_DOWNLOAD_URL=https://github.com/shadowsocks/shadowsocks-rust/releases/download/v1.14.3/shadowsocks-v1.14.3.x86_64-unknown-linux-musl.tar.xz
ENV SHADOWSOCKS_VERSION=v1.14.3

ENV VPN_LOCATION=smart
ENV SS_METHOD=chacha20-ietf-poly1305
ENV SS_PASSWORD=password

RUN apt update && \
    apt install -y iproute2 wget curl iptables xz-utils supervisor && \
    wget ${EXPRESSVPN_DOWNLOAD_URL} -O /tmp/expressvpn.deb && \
    wget ${SHADOWSOCKS_DOWNLOAD_URL} -O /opt/shadowsocks.tar.xz && \
    apt install -y /tmp/expressvpn.deb && \
    cd /opt/ && \
    xz -d ./shadowsocks.tar.xz && \
    tar xf ./shadowsocks.tar && \
    cd / && \
    rm /tmp/expressvpn.deb && \
    rm /opt/shadowsocks.tar && \ 
    rm -rf /var/lib/apt/lists/*

COPY ./supervisor.conf /etc/supervisor/conf.d/supervisor.conf
COPY ./entrypoint.sh /entrypoint.sh

VOLUME /var/lib/expressvpn

CMD ["/entrypoint.sh"]
