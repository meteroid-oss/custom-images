ARG GO_VERSION=1.26

FROM --platform=$BUILDPLATFORM golang:${GO_VERSION} AS builder
ARG SMOKESCREEN_VERSION
ARG TARGETOS
ARG TARGETARCH
WORKDIR /src
ADD --keep-git-dir=true https://github.com/stripe/smokescreen.git#${SMOKESCREEN_VERSION} ./
RUN CGO_ENABLED=0 GOFLAGS=-mod=vendor GOOS=$TARGETOS GOARCH=$TARGETARCH \
    go build -trimpath -ldflags="-s -w" -o /out/smokescreen .

FROM gcr.io/distroless/static:nonroot
COPY --from=builder --chmod=0555 /out/smokescreen /smokescreen
USER 65532:65532
EXPOSE 4750
ENTRYPOINT ["/smokescreen"]
CMD ["--listen-ip", "0.0.0.0", "--listen-port", "4750"]
