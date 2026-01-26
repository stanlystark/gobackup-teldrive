FROM ghcr.io/ptero-eggs/yolks:debian

LABEL author="Stanislav suganov" maintainer="s@r70.net"
LABEL org.opencontainers.image.source="https://github.com/stanlystark/gobackup-egg"
LABEL org.opencontainers.image.licenses=MIT

ENV DEBIAN_FRONTEND noninteractive

RUN apt update \
    && apt install -y default-mysql-client pigz python3 python3-pip python3-venv ca-certificates curl tar

RUN mkdir -p /tmp/tu \
  && curl -L "https://github.com/Nekmo/telegram-upload/archive/refs/heads/master.tar.gz" \
     | tar -xz -C /tmp/tu --strip-components=1 \
  && mkdir -p /home/container/telegram_upload \
  && cp -a /tmp/tu/telegram_upload/. /home/container/telegram_upload/ \
  && cp -a /tmp/tu/requirements.txt /tmp/requirements.txt \
  && rm -rf /tmp/tu

#COPY requirements.txt /tmp/requirements.txt
#RUN python3 -m pip install --no-cache-dir -r /tmp/requirements.txt
RUN python3 -m pip install --no-cache-dir -r /tmp/requirements.txt --break-system-packages

COPY --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
