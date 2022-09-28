FROM debian:bookworm-slim
LABEL maintainer "urothis@gmail.com"
RUN apt-get update && \
  apt-get --no-install-recommends -y install libc6 libstdc++6 && \
  rm -r /var/cache/apt /var/lib/apt/lists && \
  mkdir -p /nwn/home /nwn/run
COPY docker_data/data/ /nwn/data/data/
COPY docker_data/lang/ /nwn/data/lang/
COPY docker_data/bin/ /nwn/data/bin/
COPY scripts/run-server.sh scripts/prep-nwn-ini.awk scripts/prep-nwnplayer-ini.awk /nwn/
COPY module/DockerDemo.mod /nwn/data/data/mod/
RUN mkdir /nwn/data/bin/linux && dpkg --print-architecture
RUN if $(dpkg --print-architecture) = "arm64"; then mv /nwn/data/bin/linux-arm64/nwserver-linux /nwn/data/bin/linux/nwserver-linux ; else mv /nwn/data/bin/linux-x86/nwserver-linux /nwn/data/bin/linux/nwserver-linux ; fi
RUN chmod +x /nwn/data/bin/linux/nwserver-linux
RUN chmod +x /nwn/run-server.sh
VOLUME /nwn/home
EXPOSE ${NWN_PORT:-5121}/udp
ENV NWN_TAIL_LOGS=y
ENV NWN_EXTRA_ARGS="-userdirectory /nwn/run"
WORKDIR /nwn/data/bin/linux
ENTRYPOINT ["/bin/bash", "/nwn/run-server.sh"]


