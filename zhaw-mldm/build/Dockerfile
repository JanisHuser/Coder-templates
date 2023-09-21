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

RUN apt-get update \
    && apt-get install -y \
	python3 \
	python3-pip

RUN mkdir -p ~/miniconda3 \
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh \
	&& bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3 \
	&& rm -rf ~/miniconda3/miniconda.sh \
	&& ~/miniconda3/bin/conda init bash

ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}
