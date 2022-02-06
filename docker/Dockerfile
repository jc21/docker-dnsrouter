# This is a Dockerfile intended to be built using `docker buildx`
# for multi-arch support. Building with `docker build` may have unexpected results.
FROM jc21/gotools:latest AS gobuild

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG DNSROUTER_VERSION

ENV DNSROUTER_VERSION="${DNSROUTER_VERSION:-0.0.0}" \
	GO111MODULE=on

RUN mkdir -p /workspace
WORKDIR /workspace
RUN wget "https://github.com/jc21/dnsrouter/archive/refs/tags/v${DNSROUTER_VERSION}.tar.gz" -O dnsrouter.tgz
RUN tar -xzf dnsrouter.tgz
WORKDIR /workspace/dnsrouter-${DNSROUTER_VERSION}
RUN go build \
	-ldflags "-w -s -X main.version=${DNSROUTER_VERSION}" \
	-o /workspace/dnsrouter \
	./cmd/dnsrouter

#############
# Final Image
#############

FROM debian:buster-slim
LABEL maintainer="Jamie Curnow <jc@jc21.com>"

COPY --from=gobuild /workspace/dnsrouter /dnsrouter
COPY files/dnsrouter-config.json /dnsrouter-config.json

EXPOSE 53/udp
EXPOSE 53/tcp

ENTRYPOINT ["/dnsrouter", "-c", "/dnsrouter-config.json"]

LABEL org.label-schema.schema-version="1.0" \
	org.label-schema.license="MIT" \
	org.label-schema.name="dnsrouter" \
	org.label-schema.url="https://github.com/jc21/docker-dnsrouter" \
	org.label-schema.vcs-url="https://github.com/jc21/docker-dnsrouter.git" \
	org.label-schema.cmd="docker run --rm -ti jc21/dnsrouter:latest"
