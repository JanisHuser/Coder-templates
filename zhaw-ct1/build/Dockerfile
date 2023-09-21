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

RUN apt-get update && apt-get install -y \
    build-essential \
    systemd \
	socat \
	gdb \
	make \
	cmake \
	libusb-1.0-0-dev \
	gcc \
	build-essential

# Download STM32
RUN mkdir stm32
RUN cd stm32
RUN git clone https://github.com/stlink-org/stlink
RUN cd stlink
# RUN cmake .
# RUN make
# RUN cd bin
# RUN cp st-* /usr/local/bin
# RUN cd ../lib
# RUN cp *.so* /lib32
# RUN cp stlink/config/udev/rules.d/49-stlinkv* /etc/udev/rules.d/

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
