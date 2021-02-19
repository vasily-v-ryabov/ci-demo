# Run on arm64 (aarch64) host - e.g. hpc-arm-01
# docker build --no-cache --network=host --rm --force-rm --build-arg ARCH=aarch64 -t harbor.mellanox.com/swx-infra/swx-jenkins-agent-jnlp:aarch64 .
# docker login harbor.mellanox.com/swx-infra
# docker push harbor.mellanox.com/swx-infra/jenkins-arm-agent-jnlp

# Possible ARCH values: x86_64, aarch64, ppc64le
ARG ARCH=x86_64

FROM harbor.mellanox.com/swx-infra/swx-jenkins-agent:$ARCH
LABEL Description="This is a base image, which allows connecting Jenkins agents via JNLP protocols under swx-jenkins user" Vendor="Jenkins project" Version="4.6"
COPY jenkins-agent /usr/local/bin/jenkins-agent
ENTRYPOINT ["jenkins-agent"]
