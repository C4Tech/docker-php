FROM composer/composer:master

ENV DEBIAN_FRONTEND noninteractive

COPY hhvm.list /etc/apt/sources.list.d/hhvm.list
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449
RUN apt-get update && apt-get install -y hhvm

ENTRYPOINT ["hhvm", "/usr/local/bin/composer", "--ansi"]
CMD ["-"]
