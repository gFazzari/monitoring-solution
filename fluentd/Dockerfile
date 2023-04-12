FROM fluent/fluentd:edge-debian

USER root

RUN apt update && apt install -y ruby-dev && \
    gem update --system && \
    fluent-gem install fluent-plugin-opensearch --no-document && \
    fluent-gem install fluent-plugin-s3 --no-document
