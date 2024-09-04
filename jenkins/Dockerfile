FROM docker.io/jenkins/jenkins:2.474

USER root

ARG _JAVA_OPTIONS

RUN apt update \
    && apt install -y \
      curl \
      lsb-release \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/
ADD --chown=root:root \
    --chmod=644 \
    https://download.docker.com/linux/debian/gpg \
    /usr/share/keyrings/docker-archive-keyring.asc
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt update \
    && apt install -y \
      docker-ce-cli \
      podman \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

USER jenkins

RUN jenkins-plugin-cli --plugins "docker-workflow"