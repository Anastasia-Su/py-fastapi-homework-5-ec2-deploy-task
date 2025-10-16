# FROM debian:bookworm-slim
FROM golang:1.24-alpine

# Install necessary dependencies
# RUN apt update && apt install -y  \
#     golang-go \
#     wget \
#     dos2unix \
#     && apt clean

# Install Go 1.23 manually
# RUN wget https://go.dev/dl/go1.23.2.linux-amd64.tar.gz && \
#     rm -rf /usr/local/go && \
#     tar -C /usr/local -xzf go1.23.2.linux-amd64.tar.gz && \
#     rm go1.23.2.linux-amd64.tar.gz


RUN apk add --no-cache bash wget dos2unix

# Install MailHog using Go
RUN go version
#RUN go install github.com/mailhog/MailHog@latest
#RUN go install github.com/mailhog/MailHog@v1.0.1
RUN go install github.com/mailhog/MailHog@v1.0.1 \
    && ls -l $(go env GOPATH)/bin

# Add Go's bin directory to the PATH to make MailHog executable globally
ENV PATH="/root/go/bin:$PATH"

# Copy the commands directory into the container
COPY commands/setup_mailhog_auth.sh /commands/setup_mailhog_auth.sh

# Ensure all scripts in the commands directory have Unix-style line endings and are executable
RUN dos2unix /commands/setup_mailhog_auth.sh && chmod +x /commands/setup_mailhog_auth.sh
