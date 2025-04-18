ARG FLUENTD_BASE_VERSION \
    GO_VERSION=1.24.1

FROM golang:${GO_VERSION} as builder

RUN mkdir -p /fluentd
RUN mkdir -p /code
COPY . /code/
WORKDIR /code
RUN echo $(ls -al /code)
RUN CGO_ENABLED=0 go build -ldflags '-w -s' -o /fluentd/fluentd-watcher /code/cmd/fluent-watcher/fluentd/main.go

# See https://github.com/fluent/fluentd-docker-image/issues/425
FROM fluent/fluentd:v${FLUENTD_BASE_VERSION}-debian-1.0

LABEL org.opencontainers.image.description "A Fluentd image for use with fluent-operator"

USER root

RUN buildDeps="make gcc g++ libc-dev" \
 && apt-get update \
 && apt-get install -y --no-install-recommends $buildDeps \
 && gem install \
        fluent-plugin-s3 \
        fluent-plugin-grok-parser \
        fluent-plugin-rewrite-tag-filter \
        fluent-plugin-oss \
        fluent-plugin-dedot_filter \
        fluent-plugin-sumologic_output \
        fluent-plugin-kafka \
        fluent-plugin-label-router \
        fluent-plugin-record-modifier \
        fluent-plugin-multi-format-parser \
        fluent-plugin-aws-elasticsearch-service \
        fluent-plugin-opensearch \
        fluent-plugin-grafana-loki \
        fluent-plugin-cloudwatch-logs \
        fluent-plugin-datadog \
        fluent-plugin-prometheus \
 && gem sources --clear-all \
 && apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

 COPY ./cmd/fluent-watcher/fluentd/etc/fluent.conf /fluentd/etc/
 COPY ./cmd/fluent-watcher/fluentd/etc/app.conf /fluentd/etc/

 COPY --from=builder /fluentd/fluentd-watcher /fluentd/bin/fluentd-watcher

 USER fluent

 ENTRYPOINT ["/fluentd/bin/fluentd-watcher"]
