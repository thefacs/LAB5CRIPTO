# Dockerfile para C4/S1 (Ubuntu 22.10 - EOL)
FROM ubuntu:22.10

RUN sed -i 's/http:\/\/archive\.ubuntu\.com/http:\/\/old-releases\.ubuntu\.com/g' /etc/apt/sources.list && \
    sed -i 's/http:\/\/security\.ubuntu\.com/http:\/\/old-releases\.ubuntu\.com/g' /etc/apt/sources.list

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt install -y openssh-client openssh-server net-tools && \
    apt clean

EXPOSE 22
RUN mkdir -p /run/sshd
CMD ["/usr/sbin/sshd", "-D"]
