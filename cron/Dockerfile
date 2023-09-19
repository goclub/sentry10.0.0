ARG BASE_IMAGE
FROM ${BASE_IMAGE}
USER 0
RUN if [ -z "${http_proxy}" ]; then echo "Acquire::http::proxy \"${http_proxy}\";" >> /etc/apt/apt.conf; fi
RUN if [ -z "${https_proxy}" ]; then echo "Acquire::https::proxy \"${https_proxy}\";" >> /etc/apt/apt.conf; fi
RUN echo "\
    deb http://mirrors.aliyun.com/debian/ bullseye main non-free contrib \
    deb-src http://mirrors.aliyun.com/debian/ bullseye main non-free contrib \
    deb http://mirrors.aliyun.com/debian-security/ bullseye-security main \
    deb-src http://mirrors.aliyun.com/debian-security/ bullseye-security main \
    deb http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib \
    deb-src http://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib \
    deb http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib \
    deb-src http://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib \
" > /etc/apt/sources.list
RUN apt-get clean

RUN ln -s /lib/x86_64-linux-gnu/libpcre.so.3.13.3  /lib/libpcre.so.1
RUN apt-get update && apt-get install -y --no-install-recommends cron && \
    rm -r /var/lib/apt/lists/*

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
