FROM golang:1.8.0
MAINTAINER slovacus@gmail.com

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y build-essential \
  && apt-get install -y software-properties-common \
  && apt-get install -y curl git man unzip vim wget zsh \
# Install pygments (for syntax highlighting)
  && DEBIAN_FRONTEND=noninteractive apt-get -qq install -y --no-install-recommends python-pygments \
  && rm -rf /var/lib/apt/lists/*

# Download and install hugo
RUN rm -rf /usr/local/bin/hugo &> /dev/null

ADD https://github.com/spf13/hugo/releases/download/v0.20.2/hugo_0.20.2_Linux-64bit.tar.gz /usr/local/

RUN tar xzf /usr/local/hugo_0.20.2_Linux-64bit.tar.gz -C /usr/local/ \
    && ln -s /usr/local/hugo_0.20.2_linux_amd64/hugo_0.20.2_linux_amd64 /usr/local/bin/hugo \
    && rm /usr/local/hugo_0.20.2_Linux-64bit.tar.gz

# Define working directory.
WORKDIR /docker

# Expose default hugo port
EXPOSE 1313

# By default, serve site
ENV HUGO_BASE_URL http://localhost:1313
