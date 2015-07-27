FROM ubuntu:14.04

MAINTAINER Ofer Affias

ENV OTP_VERSION 17.5
ENV REBAR_VERSION beta-1

RUN apt-get update -qq \
    && apt-get install -y \
       build-essential \
       git \
       wget \
       libncurses5-dev \
       openssl \
       libssl-dev \
       fop \
       xsltproc \
       unixodbc-dev

ADD http://erlang.org/download/otp_src_${OTP_VERSION}.tar.gz /usr/src/
RUN cd /usr/src \
    && tar xf otp_src_${OTP_VERSION}.tar.gz \
    && cd otp_src_${OTP_VERSION} \
    && ./configure \
    && make \
    && make install \
    && cd / && rm -rf /usr/src/otp_src_${OTP_VERSION}*

ADD https://github.com/rebar/rebar3/archive/${REBAR_VERSION}.tar.gz  /usr/src/rebar3-${REBAR_VERSION}.tar.gz
RUN cd /usr/src \
    && tar zxf rebar3-${REBAR_VERSION}.tar.gz \
    && cd rebar3-${REBAR_VERSION} \
    && escript bootstrap \
    && cp rebar3 /usr/bin/rebar3 \
    && cd / && rm -rf /usr/src/rebar3-${REBAR_VERSION}*

CMD ["erl"]
