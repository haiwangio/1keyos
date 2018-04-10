FROM ubuntu:latest

MAINTAINER Port Direct <support@port.direct>
RUN sed -i 's/security.ubuntu.com\/ubuntu\//mirrors.aliyun.com\/ubuntu\//g' /etc/apt/sources.list
RUN sed -i 's/archive.ubuntu.com\/ubuntu\//mirrors.aliyun.com\/ubuntu\//g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y curl  git bzip2  sudo 
#RUn apt-get update && apt-get install -y gpg
RUN curl -L -o cork https://github.com/coreos/mantle/releases/download/v0.8.2/cork-0.8.2-amd64
RUN curl -L -o cork.sig https://github.com/coreos/mantle/releases/download/v0.8.2/cork-0.8.2-amd64.sig
#RUN gpg --receive-keys 9CEB8FE6B4F1E9E752F61C82CDDE268EBB729EC7
#RUN gpg --verify cork.sig cork
RUN mkdir -p /home/root/
RUN mkdir coreos-sdk
RUN apt-get install -y vim 
RUN apt-get update && apt-get install --no-install-recommends -y git-core gitk git-gui subversion curl ca-certificates python xz-utils sudo
RUN groupadd -g 500 core; useradd -u 500 -g 500   core; chown -R core:core /home 
RUN echo "%core ALL=(ALL)  NOPASSWD: ALL" >> /etc/sudoers
RUN chmod +x cork && mkdir -p /home/core/.local/bin && mv cork /home/core/.local/bin
USER core
ENV PATH ${PATH}:/home/core/.local/bin
#COPY ./asset/ /mnt/host/source/
RUN mkdir -p  /mnt/host/source/
RUN git clone https://github.com/1keyos/scripts /mnt/host/source/src/
RUN chown -R core:core /mnt/host/source
RUN  cork create
