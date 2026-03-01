FROM ubuntu:22.04

ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get upgrade -y \
    && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Set the environment variables
ENV SHELL=/bin/bash
ENV PATH="/home/$USERNAME/.local/bin:${PATH}"

# Install common tools
RUN apt-get update && apt-get install -y \
    curl \
    git \
    git-lfs \
    htop \
    iputils-ping \
    nano \
    net-tools \
    nmap \
    p7zip-full \
    tmux \
    tree \
    unzip \
    vim \
    wget \
    zip \
    && rm -rf /var/lib/apt/lists/*

# Install python packages
# Reference: https://squidfunk.github.io/mkdocs-material/setup/
RUN pip3 install --no-cache-dir \
    mkdocs-material \
    mkdocs-minify-plugin \
    mkdocs-redirects \
    mkdocs-git-revision-date-localized-plugin \
    mkdocs-macros-plugin \
    mkdocs-git-committers-plugin-2

# Set the default user
USER $USERNAME
CMD ["/bin/bash"]
COPY --chown=$USERNAME:$USERNAME \
    .bashrc /home/$USERNAME/.bashrc

# Claude Code CLI configuration
ARG CLAUDE_CODE=""
COPY --chown=$USERNAME:$USERNAME \
    modules/install_claude_code.sh /tmp/install_claude_code.sh
RUN /tmp/install_claude_code.sh && rm /tmp/install_claude_code.sh

# Install custom environment
RUN git clone https://github.com/YuZhong-Chen/.setup_env.git ~/.setup_env \
    && ~/.setup_env/install.sh