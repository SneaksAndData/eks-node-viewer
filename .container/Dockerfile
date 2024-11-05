FROM golang:1.23-bookworm as build

WORKDIR /app

COPY . .

RUN go mod tidy && \
    go build -o eks-node-viewer ./cmd/eks-node-viewer && \
    rm -rf /go/pkg /go/src

FROM debian:bookworm-slim

WORKDIR /app

# Install CA certificates
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

COPY --from=build /app/eks-node-viewer /app/eks-node-viewer

CMD ["./eks-node-viewer"]