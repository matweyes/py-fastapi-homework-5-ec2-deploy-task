FROM debian:bookworm-slim

# Install necessary dependencies
RUN apt update && apt install -y  \
    golang-go \
    wget \
    dos2unix \
    && apt clean

# Install a current Go toolchain directly from go.dev
ENV GO_VERSION=1.25.5
RUN wget -q https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz \
    && rm go${GO_VERSION}.linux-amd64.tar.gz

# Add Go's bin directory to the PATH to make MailHog executable globally
ENV PATH="/usr/local/go/bin:/root/go/bin:$PATH"

# Install MailHog using Go
RUN go install github.com/mailhog/MailHog@latest

# Copy the commands directory into the container
COPY commands/setup_mailhog_auth.sh /commands/setup_mailhog_auth.sh

# Ensure all scripts in the commands directory have Unix-style line endings and are executable
RUN dos2unix /commands/setup_mailhog_auth.sh && chmod +x /commands/setup_mailhog_auth.sh
