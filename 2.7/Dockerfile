FROM ubuntu:18.04

ENV LANG=en_US.UTF-8
ENV RUBY_MAJOR 2.7
ENV RUBY_VERSION 2.7.2
ENV RUBY_DOWNLOAD_SHA256 1b95ab193cc8f5b5e59d2686cb3d5dcf1ddf2a86cb6950e0b4bdaae5040ec0d6

ARG BUILD_ID

LABEL ruby.version="$RUBY_VERSION"
LABEL ruby.build.id="$BUILD_ID"

RUN set -ex \
  && export DEBIAN_FRONTEND=noninteractive \
  && apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    curl \
    git \
    libcurl4-openssl-dev \
    libjemalloc-dev \
    libmagic-dev \
    libmagickwand-dev \
    libmariadbclient-dev-compat \
    libreadline6-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    locales \
    tzdata \
    zlib1g-dev \
  && locale-gen "$LANG" \
  && curl -L "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR}/ruby-$RUBY_VERSION.tar.xz" > ruby.tar.xz \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
  && mkdir -p /usr/src/ruby \
  && tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
  && rm ruby.tar.xz \
  && cd /usr/src/ruby \
  && ./configure \
    --disable-install-doc \
    --enable-shared \
    --with-jemalloc \
  && make \
  && make install \
  && cd / \
	&& rm -r /usr/src/ruby \
	&& rm -rf /root/.gem/

CMD ["irb"]
