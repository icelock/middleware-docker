FROM ubuntu:23.04

RUN apt-get update

RUN apt -y install curl

RUN curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | bash

RUN apt -y install sysbench


CMD ["bash"]

# docker build -f Dockerfile -t my-sysbench:latest .

# docker build -f Dockerfile -t my-sysbench:latest . --network host --build-arg HTTP_PROXY=http://192.168.91.1:1080 --build-arg HTTPS_PROXY=http://192.168.91.1:1080