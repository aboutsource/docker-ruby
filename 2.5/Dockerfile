FROM ubuntu:18.04

ENV RUBY_MAJOR 2.5
ENV RUBY_VERSION 2.5.4
ENV RUBY_DOWNLOAD_SHA256 46f6eff655a6be1939f70c7a4c1bf58f76663e7e804738bc52f4d47ca31dee3d
ENV RUBYGEMS_VERSION 3.0.3
ENV BUNDLER_VERSION 1.17.3

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
    libcurl4-openssl-dev \
    libjemalloc-dev \
    libmagic-dev \
    libmagickwand-dev \
    libreadline6-dev \
    libssl-dev \
    libxml2-dev \
    libxslt-dev \
    libyaml-dev \
    tzdata \
    zlib1g-dev \
  && curl -L "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR}/ruby-$RUBY_VERSION.tar.xz" > ruby.tar.xz\
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
	&& gem update --system "$RUBYGEMS_VERSION" \
	&& gem install bundler --version "$BUNDLER_VERSION" --force --no-document \
	&& rm -r /root/.gem/

CMD ["irb"]
