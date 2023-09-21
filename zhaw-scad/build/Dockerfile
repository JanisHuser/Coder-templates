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

# Install nodejs and npm
RUN sudo apt update \
	&& apt-get install -y \
	nodejs \
	npm \
	unzip 

# Install AWS Cli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
	&& unzip awscliv2.zip \
	&& sudo ./aws/install




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
