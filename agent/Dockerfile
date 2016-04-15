FROM java:8

RUN apt-get update && \
    apt-get install -y curl unzip git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV DOCKER_INSTALL https://get.docker.com/builds/Linux/x86_64/docker-1.11.0.tgz

RUN curl -o /docker.tgz "$DOCKER_INSTALL" && \
    tar -xvf docker.tgz && \
    rm docker.tgz

ENV PATH $PATH:/docker
ENV GO_AGENT_URL https://download.go.cd/binaries/16.3.0-3183/generic/go-agent-16.3.0-3183.zip

# Install the base go-server stuff
RUN mkdir -p /go-agent/work && mkdir -p /go-agent/config && cd /go-agent && \
    curl -o agent.zip "$GO_AGENT_URL" && \
    unzip -j agent.zip && \
    chmod +x agent.sh && \
    rm agent.zip 

ENV AGENT_WORK_DIR /go-agent/work
ENV PRODUCTION_MODE Y
ENV DAEMON N

ENV GO_SERVER go-server

ADD startup /go-agent/startup
WORKDIR /go-agent
CMD ["/go-agent/startup"]
