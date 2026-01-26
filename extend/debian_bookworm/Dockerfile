FROM ghcr.io/ptero-eggs/yolks:debian

LABEL author="Stanislav suganov" maintainer="s@r70.net"
LABEL org.opencontainers.image.source="https://github.com/stanlystark/gobackup-egg"
LABEL org.opencontainers.image.licenses=MIT

ENV DEBIAN_FRONTEND noninteractive

RUN apt update \
    && apt install -y default-mysql-client pigz python3 python3-pip python3-venv ca-certificates curl tar

RUN python3 -m pip install telegram-upload --break-system-packages
    
COPY --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
