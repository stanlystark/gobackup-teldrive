# Используем существующий образ как базовый
FROM ghcr.io/ptero-eggs/yolks:debian

LABEL author="Stanislav suganov" maintainer="s@r70.net"
LABEL org.opencontainers.image.source="https://github.com/stanlystark/gobackup-egg"
LABEL org.opencontainers.image.licenses=MIT

ENV DEBIAN_FRONTEND noninteractive

# Добавляем MySQL
RUN apt update \
    && apt install -y default-mysql-client pigz python3-full pipx

RUN pipx install telegram-upload

# Копируем и настраиваем entrypoint.sh, чтобы он продолжал работать с нашим новым сервисом
COPY --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Указываем начальную команду
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
