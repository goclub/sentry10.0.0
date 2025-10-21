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

# 修复 GPG 密钥问题
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 0E98404D386FA1D9 || \
    apt-key adv --keyserver pgp.mit.edu --recv-keys 0E98404D386FA1D9 || \
    echo "密钥 0E98404D386FA1D9 添加失败，继续执行..."

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 6ED0E7B82643E131 || \
    apt-key adv --keyserver pgp.mit.edu --recv-keys 6ED0E7B82643E131 || \
    echo "密钥 6ED0E7B82643E131 添加失败，继续执行..."

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 605C66F00D6C9793 || \
    apt-key adv --keyserver pgp.mit.edu --recv-keys 605C66F00D6C9793 || \
    echo "密钥 605C66F00D6C9793 添加失败，继续执行..."

RUN ln -s /lib/x86_64-linux-gnu/libpcre.so.3.13.3  /lib/libpcre.so.1
RUN apt-get update && apt-get install -y --no-install-recommends cron && \
    rm -r /var/lib/apt/lists/*

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
