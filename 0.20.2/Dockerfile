FROM go:1.8.0
MAINTAINER slovacus@gmail.com

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  && apt-get update \
  && apt-get -y upgrade \
  && locale-gen en_US.UTF-8 \
  && apt-get install -y build-essential \
  && apt-get install -y software-properties-common \
  && apt-get install -y curl git man unzip vim wget zsh \
# Install pygments (for syntax highlighting)
  && DEBIAN_FRONTEND=noninteractive apt-get -qq install -y --no-install-recommends python-pygments \
  && rm -rf /var/lib/apt/lists/*

# Download and install hugo
ENV HUGO_VERSION 0.22.2
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux-64bit

RUN rm -rf /usr/local/bin/hugo &> /dev/null
ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY}.tgz /usr/local/
RUN tar xzf /usr/local/${HUGO_BINARY}.tgz -C /usr/local/ \
    && ln -s /usr/local/${HUGO_BINARY}/${HUGO_BINARY} /usr/local/bin/hugo \
    && rm /usr/local/${HUGO_BINARY}.tgz

# Define working directory.
WORKDIR /docker

# Expose default hugo port
EXPOSE 1313

# By default, serve site
ENV HUGO_BASE_URL http://localhost:1313
