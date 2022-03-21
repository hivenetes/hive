FROM ubuntu:focal

LABEL Description="rogue"

ARG user=rogue
ARG uid=1000
ARG shell=/bin/bash

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils software-properties-common \ 
    sudo \
    xz-utils curl wget unzip \
    git ssh vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* 



# --- User environment configuration ---
# Create and add user
RUN useradd -ms ${shell} ${user} \
  && export uid=${uid} gid=${uid} \
  && mkdir -p /etc/sudoers.d \
  && echo "${user}:x:${uid}:" >> /etc/group \
  && echo "${user} ALL=(ALL) NOPASSWD: ALL" > "/etc/sudoers.d/${user}" \
  && chmod 0440 "/etc/sudoers.d/${user}"

# Switch to ${user}
ENV USER=${user}
USER ${user}

WORKDIR /home/${user}/code
