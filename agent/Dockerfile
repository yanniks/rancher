FROM ioft/armhf-ubuntu

RUN apt-get update && \
     apt-get install --no-install-recommends -y \
     arptables \
     bridge-utils \
     ca-certificates \
     curl \
     iptables \
     libssl-dev \
     libffi-dev \
     gcc \
     make \
     conntrack \
     libaio1 \
     fio && \
    curl -s https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz | tar -zxv -C /tmp/ && \
    cd /tmp/Python-2.7.11 && ./configure && make && make install && \
    curl -s https://bootstrap.pypa.io/get-pip.py | python && \
    pip install eventlet cattle docker-py && \
    pip install --upgrade requests[security]==2.9.1 &&\
    apt-get remove -y --purge make libffi-dev libssl-dev gcc && apt-get autoremove -y && \
    rm -rf /tmp/Python-2.7.11 && \
    curl -s http://stedolan.github.io/jq/download/linux64/jq > /usr/bin/jq; chmod +x /usr/bin/jq

# Get the raspberry pi (arm) docker binaries.
RUN apt-get install -y docker.io

RUN mkdir -p /var/lib/cattle /var/lib/rancher
COPY register.py resolve_url.py run.sh /
ENTRYPOINT ["/run.sh"]
LABEL "io.rancher.container.system"="rancher-agent"
ENV HOST_DOCKER_SOCK /var/run/docker.sock
ENV RANCHER_AGENT_IMAGE rancher/agent:v1.0.2
