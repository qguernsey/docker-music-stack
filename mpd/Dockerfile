FROM alpine:3.13.6
MAINTAINER @qguernsey https://github.com/qguernsey

# ENV MPD_VERSION 0.22.11
# ENV MPC_VERSION 0.27-r0

# https://docs.docker.com/engine/reference/builder/#arg
ARG user=mpd
ARG group=audio

RUN apk -q update \
    && apk -q --no-progress add mpd mpc ncmpc \
    && setcap -r /usr/bin/mpd \
    && rm -rf /var/cache/apk/*

RUN mkdir -p /var/lib/mpd/music \
    && mkdir -p /var/lib/mpd/playlists \
    && mkdir -p /var/lib/mpd/database \
    && mkdir -p /var/log/mpd/mpd.log \
    && chown -R ${user}:${group} /var/lib/mpd \
    && chown -R ${user}:${group} /var/log/mpd/mpd.log


COPY mpd.conf /etc/mpd.conf

# Entry point for mpc update and stuff
EXPOSE 6600

CMD ["mpd", "--stdout", "--no-daemon"]
