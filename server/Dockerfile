FROM java:8

RUN apt-get update && \
    apt-get install -y curl unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV GO_SERVER_URL https://download.go.cd/binaries/16.3.0-3183/generic/go-server-16.3.0-3183.zip

# Install the base go-server stuff
RUN mkdir -p /go-server/work && mkdir -p /go-server/config && cd /go-server && \
    curl -o server.zip "$GO_SERVER_URL" && \
    unzip -j server.zip && \
    chmod +x server.sh && \
    rm server.zip 

# Install the go-server plugins we want 
ENV STASH_PR_POLLER https://github.com/ashwanthkumar/gocd-build-github-pull-requests/releases/download/v1.2.3/stash-pr-poller-1.2.3.jar
ENV STASH_PR_STATUS https://github.com/gocd-contrib/gocd-build-status-notifier/releases/download/1.1/stash-pr-status-1.1.jar

ENV GITHUB_PR_POLLER https://github.com/ashwanthkumar/gocd-build-github-pull-requests/releases/download/v1.2.3/github-pr-poller-1.2.3.jar
ENV GITHUB_PR_STATUS https://github.com/gocd-contrib/gocd-build-status-notifier/releases/download/1.1/github-pr-status-1.1.jar

ENV SLACK_BUILD_NOTIFIER https://github.com/ashwanthkumar/gocd-slack-build-notifier/releases/download/v1.1.2/gocd-slack-notifier-1.1.2.jar
ENV EMAIL_NOTIFIER https://github.com/gocd-contrib/email-notifier/releases/download/v0.1/email-notifier-0.1.jar

ENV DOCKER_PIPELINE https://github.com/Haufe-Lexware/gocd-plugins/raw/master/bin/gocd-docker-pipeline-plugin-1.0.0.jar

RUN mkdir -p /go-server/work/plugins/external && cd /go-server/work/plugins/external && \
    curl -L -o stash-pr-poller.jar "$STASH_PR_POLLER" && \
    curl -L -o stash-pr-status.jar "$STASH_PR_STATUS" && \
    curl -L -o github-pr-poller.jar "$GITHUB_PR_POLLER" && \
    curl -L -o github-pr-status.jar "$GITHUB_PR_STATUS" && \
    curl -L -o slack-notifier.jar "$SLACK_BUILD_NOTIFIER" && \
    curl -L -o email-notifier.jar "$EMAIL_NOTIFIER" && \
    curl -L -o docker-pipeline-plugin.jar "$DOCKER_PIPELINE"

ENV DAEMON N
ENV GO_SERVER_PORT 8080
ENV GO_SERVER_SSL 8154
ENV SERVER_WORK_DIR /go-server/work

ADD startup /go-server/startup
ADD slack_notify.conf /root/go_notify.conf

EXPOSE 8080

WORKDIR /go-server
CMD ["/go-server/startup"]

