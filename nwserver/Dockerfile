# syntax=docker/dockerfile:1
FROM debian:bookworm-slim
LABEL maintainer "urothis@gmail.com"
ARG TARGETOS TARGETARCH
COPY docker_data/data/data /nwn/data/data/data
COPY docker_data/run-server.sh /nwn/run-server.sh
COPY docker_data/data/bin/${TARGETOS}-${TARGETARCH}/nwserver-linux /nwn/data/bin/${TARGETOS}-${TARGETARCH}/nwserver-linux
COPY docker_data/lang/ /nwn/data/lang/
COPY ./module/DockerDemo.mod /nwn/data/data/mod/
RUN apt-get update && \
  apt-get --no-install-recommends -y install libc6 libstdc++6 && \
  rm -r /var/cache/apt /var/lib/apt/lists
RUN mkdir -p /nwn/home /nwn/run
RUN chmod +x /nwn/run-server.sh
VOLUME /nwn/home
EXPOSE ${NWN_PORT:-5121}/udp
ENV NWN_TAIL_LOGS=y
ENV NWN_EXTRA_ARGS="-userdirectory /nwn/run"
WORKDIR /nwn/data/bin/${TARGETOS}-${TARGETARCH}
ENTRYPOINT ["/bin/bash", "/nwn/run-server.sh"]
