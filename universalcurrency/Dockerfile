FROM ubuntu:16.04
MAINTAINER krit@hashbx.io

RUN apt-get update -qq && apt-get -y install build-essential \
  libssl-dev libboost-all-dev libdb-dev libtool
RUN apt-get -y install libdb5.3 libdb5.3-dev libdb5.3++-dev
RUN apt-get -y install git ntp make g++ gcc autoconf cpp ngrep iftop sysstat autotools-dev pkg-config
RUN apt-get -y install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev wget
RUN wget http://miniupnp.free.fr/files/download.php?file=miniupnpc-2.0.tar.gz -O /opt/miniupnpc-2.0.tar.gz
WORKDIR /opt
RUN cd /opt && tar xzf miniupnpc-2.0.tar.gz
RUN cd miniupnpc-2.0 && make install && cd .. && rm -rf miniupnpc-2.0 miniupnpc-2.0.tar.gz

RUN git clone https://github.com/unitcurrency/unitcurrency.git \
  && cd unitcurrency/src/leveldb/ \
  && chmod 755 build_detect_platform \
  && make libleveldb.a libmemenv.a \
  && cd .. \
  && make -f makefile.unix \
  && cp UniversalCurrencyd /usr/sbin/
CMD ['/usr/bin/UniversalCurrencyd']
