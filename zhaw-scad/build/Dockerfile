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

# # Install nodejs and npm
# RUN sudo apt update \
# 	&& apt-get install -y \
# 	nodejs \
# 	npm \
# 	unzip 

# # Install AWS Cli
# RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
# 	&& unzip awscliv2.zip \
# 	&& sudo ./aws/install

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash


RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg

RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
RUN apt-get update
RUN apt-get install -y \
	azure-functions-core-tools-4 \
	python3.10-venv

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
