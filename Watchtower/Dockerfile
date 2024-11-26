# syntax=docker/dockerfile:latest
# From https://github.com/containrrr/watchtower/blob/main/dockerfiles/Dockerfile.self-contained
FROM containrrr/watchtower:1.7.1 AS watchtower

FROM alpine:3.20.3

RUN set -ex; \
    apk upgrade --no-cache -a; \
    apk add --no-cache bash

COPY --from=watchtower /watchtower /watchtower

HEALTHCHECK CMD [ "/watchtower", "--health-check"]

ENTRYPOINT ["/watchtower"]