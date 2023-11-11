FROM ubuntu

RUN apt-get update \
	&& apt-get install -y \
	curl \
	git \
	golang \
	sudo \
	vim \
	wget \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -s https://deb.nodesource.com/setup_18.x | sudo bash
# Install nodejs and npm
RUN sudo apt update \
	&& apt-get install -y \
	unzip \
	curl \
	git \
	golang \
	sudo \
	vim \
	wget \
	&& rm -rf /var/lib/apt/lists/*

RUN sudo apt-get update

# Install Node JS
RUN curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash
RUN sudo apt-get install -y nodejs

# # Install AWS Cli
# RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
# 	&& unzip awscliv2.zip \
# 	&& sudo ./aws/install

# Install Docker
RUN curl -fsSL https://get.docker.com | sh

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash


RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
RUN apt-get update
RUN apt-get install -y \
	azure-functions-core-tools-4 \
	python3.10-venv \
	python3-pip


# INSTALL BALLERINA
RUN wget https://dist.ballerina.io/downloads/2201.8.2/ballerina-2201.8.2-swan-lake-linux-x64.deb
RUN dpkg -i ballerina-2201.8.2-swan-lake-linux-x64.deb
RUN rm ballerina-2201.8.2-swan-lake-linux-x64.deb

# recommended: remove the system-wide environment override
RUN rm /etc/environment

# recommended: adjust OpenSSH config
RUN echo "PermitUserEnvironment yes" >> /etc/ssh/sshd_config && \
  echo "X11Forwarding yes" >> /etc/ssh/sshd_config && \
  echo "X11UseLocalhost no" >> /etc/ssh/sshd_config

ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}
