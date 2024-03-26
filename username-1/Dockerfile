FROM ubuntu:focal-20240123 as base

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get upgrade -y && \
apt-get install -y tar python3 nano sudo jq git make \
&& apt-get autoremove -y && \
apt-get clean

ARG username=github
RUN useradd -ms /bin/bash ${username}
RUN echo "%${username} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER ${username}
ENV HOME=/home/${username}


# trust git folders with different owners
RUN echo "W3NhZmVdCglkaXJlY3RvcnkgPSAqCg==" | base64 -d > $HOME/.gitconfig
RUN sudo git config --global --add safe.directory '*'

WORKDIR $HOME
