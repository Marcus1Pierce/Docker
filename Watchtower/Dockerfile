# syntax=docker/dockerfile:latest
# From https://github.com/containrrr/watchtower/blob/main/dockerfiles/Dockerfile.self-contained
FROM containrrr/watchtower:1.7.1 AS watchtower

FROM alpine:3.20.5 

RUN apk upgrade --no-cache -a
RUN apk add --no-cache \
    bash \
    tzdata \
    ca-certificates

COPY --from=watchtower /watchtower /watchtower

HEALTHCHECK CMD [ "/watchtower", "--health-check"]

ENTRYPOINT ["/watchtower"]
