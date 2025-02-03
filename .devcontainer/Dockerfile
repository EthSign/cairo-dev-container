FROM ubuntu:24.04

SHELL ["/bin/bash", "-l", "-c"]

# Install essential packages
RUN apt-get update && apt-get install -y \
    curl \
    git \
    build-essential \
    procps \
    file \
    unzip \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Create sudoers directory and non-root user
RUN mkdir -p /etc/sudoers.d && \
    useradd -m -s /bin/bash vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/vscode

# Switch to non-root user
USER vscode
WORKDIR /home/vscode
ENV HOME=/home/vscode

ENV PATH=${PATH}:${HOME}/.local/bin

# Install Rust, Scarb, Starknet Foundry
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
ENV PATH=${PATH}:${HOME}/.cargo/bin
RUN curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh -s -- -v 2.9.2
RUN curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/foundry-rs/starknet-foundry/master/scripts/install.sh | sh -s
RUN snfoundryup -v 0.36.0