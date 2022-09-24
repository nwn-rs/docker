FROM beamdog/nwserver:latest AS nwn
FROM debian:bookworm-slim
COPY --from=nwn /nwn/data/data/ /nwn/data/data/
ARG NWN_ARCH=linux-x86
LABEL maintainer "urothis@gmail.com"
RUN apt-get update && \
  apt-get --no-install-recommends -y install libc6 libstdc++6 && \
  rm -r /var/cache/apt /var/lib/apt/lists
RUN mkdir -p /nwn/home /nwn/run
COPY /data/bin/${NWN_ARCH} /nwn/data/bin/${NWN_ARCH}
RUN chmod +x /nwn/data/bin/${NWN_ARCH}/nwserver-linux
COPY nwserver/ /nwn/
RUN chmod +x /nwn/run-server.sh
VOLUME /nwn/home
EXPOSE ${NWN_PORT:-5121}/udp
ENV NWN_TAIL_LOGS=y
ENV NWN_EXTRA_ARGS="-userdirectory /nwn/run"
WORKDIR /nwn/data/bin/${NWN_ARCH}
ENTRYPOINT ["/bin/bash", "/nwn/run-server.sh"]