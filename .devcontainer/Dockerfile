FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04

RUN apt update && apt -y upgrade
RUN apt -y install build-essential wget git curl sudo
RUN apt -y install python3 python3-pip

# add user
ARG username=remote
RUN echo "root:root" | chpasswd && \
    adduser --disabled-password --gecos "" "${username}" && \
    echo "${username}:${username}" | chpasswd && \
    echo "%${username}    ALL=(ALL)   NOPASSWD:    ALL" >> /etc/sudoers

# pyenv
USER remote
RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(pyenv init --path)"' >> ~/.bashrc

# poetry
USER root
ENV POETRY_HOME=/opt/poetry
RUN curl -sSL https://install.python-poetry.org | python3 - && \
    cd /usr/local/bin && \
    ln -s /opt/poetry/bin/poetry && \
    poetry config virtualenvs.in-project true --local
