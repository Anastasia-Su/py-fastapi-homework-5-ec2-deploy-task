FROM golang:1.24-alpine

RUN apk add --no-cache bash wget dos2unix

# Install MailHog using Go
RUN go version

RUN go install github.com/mailhog/MailHog@v1.0.1 \
    && ls -l $(go env GOPATH)/bin

# Add Go's bin directory to the PATH to make MailHog executable globally
ENV PATH="/root/go/bin:$PATH"

# Copy the commands directory into the container
COPY commands/setup_mailhog_auth.sh /commands/setup_mailhog_auth.sh

# Ensure all scripts in the commands directory have Unix-style line endings and are executable
RUN dos2unix /commands/setup_mailhog_auth.sh && chmod +x /commands/setup_mailhog_auth.sh
