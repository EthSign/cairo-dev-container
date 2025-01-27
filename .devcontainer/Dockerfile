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

# Install Starknet Foundry
RUN curl --proto '=https' --tlsv1.2 -sSf -y https://sh.rustup.rs | sh
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.15.0
RUN . "$HOME/.asdf/asdf.sh" && \
    asdf plugin add scarb && \
    asdf install scarb latest && \
    asdf global scarb latest && \
    asdf plugin add starknet-foundry && \
    asdf install starknet-foundry latest && \
    asdf global starknet-foundry latest
RUN echo '. "$HOME/.asdf/asdf.sh"' >> /home/vscode/.bashrc && \
    echo '. "$HOME/.asdf/completions/asdf.bash"' >> /home/vscode/.bashrc