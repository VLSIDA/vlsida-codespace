FROM openroad/orfs:latest

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install KLayout from precompiled deb package
RUN apt-get update && apt-get install -y \
    wget \
    && wget https://www.klayout.org/downloads/Ubuntu-22/klayout_0.30.4-1_amd64.deb \
    && apt-get install -y ./klayout_0.30.4-1_amd64.deb \
    && rm klayout_0.30.4-1_amd64.deb \
    && rm -rf /var/lib/apt/lists/*

# Install ngspice dependencies and compile from source
RUN apt-get update && apt-get install -y \
    libxaw7-dev \
    libx11-dev \
    libxext-dev \
    libxmu-dev \
    libxrender-dev \
    libcairo2-dev \
    libpango1.0-dev \
    libreadline-dev \
    autoconf \
    automake \
    libtool \
    && rm -rf /var/lib/apt/lists/*

# Install ngspice 43 from source
ARG NGSPICE_TAG=ngspice-43
WORKDIR /tmp
RUN git clone git://git.code.sf.net/p/ngspice/ngspice
WORKDIR /tmp/ngspice
RUN git checkout ${NGSPICE_TAG}
RUN ./autogen.sh
RUN ./configure --enable-openmp --with-readline
RUN make -j$(nproc)
RUN make install
RUN rm -rf /tmp/ngspice

# Install ciel for PDK management
RUN apt-get update && apt-get install -y \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

RUN pip install ciel

# Enable sky130 PDK
RUN ciel enable --pdk sky130 0fe599b2afb6708d281543108caf8310912f54af

# Set working directory
WORKDIR /root

CMD ["/bin/bash"]
