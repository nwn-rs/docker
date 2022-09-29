FROM debian:bookworm-slim
LABEL maintainer "urothis@gmail.com"
RUN apt-get update && \
  apt-get --no-install-recommends -y install libc6 libstdc++6 && \
  rm -r /var/cache/apt /var/lib/apt/lists && \
  mkdir -p /nwn/home /nwn/run
COPY docker_data/ /nwn/
COPY ./module/DockerDemo.mod /nwn/data/data/mod/
RUN if $(dpkg --print-architecture) = "arm64"; then chmod +x /nwn/data/bin/linux-arm64/nwserver-linux ; else chmod +x /nwn/data/bin/linux-x86/nwserver-linux ; fi
RUN chmod +x /nwn/run-server.sh
VOLUME /nwn/home
EXPOSE ${NWN_PORT:-5121}/udp
ENV NWN_TAIL_LOGS=y
ENV NWN_EXTRA_ARGS="-userdirectory /nwn/run"

WORKDIR /nwn/data/bin
ENTRYPOINT ["/bin/bash", "/nwn/run-server.sh"]
