# Run on arm64 (aarch64) host - e.g. hpc-arm-01
# docker build --no-cache --network=host --rm --force-rm --build-arg ARCH=arm64v8 -t harbor.mellanox.com/swx-infra/swx-jenkins-agent:aarch64 .
# docker login harbor.mellanox.com/swx-infra
# docker push harbor.mellanox.com/swx-infra/jenkins-arm-agent

# Possible ARCH values: amd64, arm64v8, ppc64le
ARG ARCH=amd64

FROM $ARCH/openjdk:11.0.3-jre

ENV HOME /home/swx-jenkins
RUN addgroup --system swx-jenkins
RUN adduser --system --home $HOME --ingroup swx-jenkins swx-jenkins
LABEL Description="This is a base image, which provides the Jenkins agent executable (slave.jar) under swx-jenkins user" Vendor="Jenkins project" Version="4.6"

ARG VERSION=4.6
ARG AGENT_WORKDIR=/home/swx-jenkins/agent

RUN apt-get update \
  && apt-get install -y curl bash git openssh-client openssl \
  && curl --create-dirs -sSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar
USER swx-jenkins
ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /home/swx-jenkins/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/swx-jenkins/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/swx-jenkins
