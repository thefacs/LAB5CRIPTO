# Dockerfile para C1 (Ubuntu 20.10 - EOL)
FROM ubuntu:20.10

RUN sed -i 's/http:\/\/archive\.ubuntu\.com/http:\/\/old-releases\.ubuntu\.com/g' /etc/apt/sources.list && \
    sed -i 's/http:\/\/security\.ubuntu\.com/http:\/\/old-releases\.ubuntu\.com/g' /etc/apt/sources.list

RUN apt update && \
    apt install -y openssh-client && \
    apt clean
    
CMD ["/bin/bash"]
