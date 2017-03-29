FROM publysher/hugo
MAINTAINER stffabi@users.noreply.github.com

RUN echo 'deb http://http.debian.net/debian wheezy-backports main' > /etc/apt/sources.list.d/wheezy-backports-main.list \
    && curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash \
    && apt-get install -y git-core git-lfs
    && rm -rf /var/lib/apt/lists/*
    && git lfs install