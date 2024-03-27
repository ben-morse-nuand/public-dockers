FROM ubuntu:focal-20240123 as base

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get upgrade -y && \
apt-get install -y tar python3 nano sudo jq git make \
&& apt-get autoremove -y && \
apt-get clean

ARG username=github
RUN useradd -u 1000 -ms /bin/bash ${username}
RUN echo "%${username} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
ENV HOME=/home/${username}

RUN sudo groupadd -g 127 docker
# RUN sudo useradd -u 1001 -g 127 -c ' ' -m -d /home/runner -s /bin/bash runner
# RUN sudo useradd -u 1001 -g 127 -ms /bin/bash runner
RUN sudo useradd -u 1001 -ms /bin/bash runner
RUN echo "%runner ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN usermod -aG docker github
RUN usermod -aG docker runner

USER ${username}

# trust git folders with different owners
# RUN echo "W3NhZmVdCglkaXJlY3RvcnkgPSAqCg==" | base64 -d > $HOME/.gitconfig
# RUN sudo git config --global --add safe.directory '*'

# RUN git config --global --add safe.directory /__w/privatecast/privatecast
# RUN sudo git config --global --add safe.directory /__w/privatecast/privatecast

WORKDIR $HOME
