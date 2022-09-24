FROM beamdog/nwserver:latest AS nwn
FROM debian:bookworm-slim
ARG NWN_ARCH=linux-x86
LABEL maintainer "urothis@gmail.com"
RUN apt-get update && \
  apt-get --no-install-recommends -y install libc6 libstdc++6 && \
  rm -r /var/cache/apt /var/lib/apt/lists && \
  mkdir -p /nwn/home /nwn/run
COPY --from=nwn /nwn/data/data/ /nwn/data/data/
COPY --from=nwn /nwn/data/lang/ /nwn/data/lang/
COPY scripts/run-server.sh scripts/prep-nwn-ini.awk scripts/prep-nwnplayer-ini.awk /nwn/
COPY /data/bin/${NWN_ARCH} /nwn/data/bin/${NWN_ARCH}
RUN chmod +x /nwn/data/bin/${NWN_ARCH}/nwserver-linux
RUN chmod +x /nwn/run-server.sh
VOLUME /nwn/home
EXPOSE ${NWN_PORT:-5121}/udp
ENV NWN_TAIL_LOGS=y
ENV NWN_EXTRA_ARGS="-userdirectory /nwn/run"
WORKDIR /nwn/data/bin/${NWN_ARCH}
ENTRYPOINT ["/bin/bash", "/nwn/run-server.sh"]