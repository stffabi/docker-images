FROM alpine:latest
MAINTAINER stffabi@users.noreply.github.com

# Set up certificates and our base tools.
RUN apk --no-cache add ca-certificates openssl git curl \
    && curl -sLO https://github.com/github/git-lfs/releases/download/v2.0.1/git-lfs-linux-amd64-2.0.1.tar.gz \
    && tar zxvf git-lfs-linux-amd64-2.0.1.tar.gz \
    && mv git-lfs-2.0.1/git-lfs /usr/bin/ \
    && rm -rf git-lfs-2.0.1 \
    && rm -rf git-lfs-linux-amd64-2.0.1.tar.gz
    && git lfs install

RUN apk --no-cache add py-pygments

# Download and install hugo
ENV HUGO_VERSION 0.19
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux_amd64
ENV HUGO_DOWNLOAD_FILE hugo_${HUGO_VERSION}_Linux-64bit.tar.gz

ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_DOWNLOAD_FILE} /tmp/hugo.tar.gz
RUN tar -xvzf /tmp/hugo.tar.gz -C /tmp/ \
	&& mv /tmp/${HUGO_BINARY}/${HUGO_BINARY} /usr/bin/hugo && rm -rf /tmp/hugo*

# Create working directory
RUN mkdir /usr/share/blog
WORKDIR /usr/share/blog

# Expose default hugo port
EXPOSE 1313

# Automatically build site
ONBUILD ADD site/ /usr/share/blog
ONBUILD RUN hugo -d /usr/share/nginx/html/

# By default, serve site
ENV HUGO_BASE_URL http://localhost:1313
CMD hugo server -b ${HUGO_BASE_URL} --bind=0.0.0.0