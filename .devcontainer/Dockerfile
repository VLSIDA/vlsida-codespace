FROM ubuntu:22.04

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Install basic dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    git \
    wget \
    curl \
    python3 \
    python3-pip \
    tcl \
    tcl-dev \
    swig \
    libboost-all-dev \
    libeigen3-dev \
    libtool \
    autoconf \
    automake \
    bison \
    flex \
    libfl-dev \
    libreadline-dev \
    libffi-dev \
    libssl-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# Install KLayout dependencies and KLayout
RUN apt-get update && apt-get install -y \
    qtbase5-dev \
    qttools5-dev \
    libqt5xmlpatterns5-dev \
    qtmultimedia5-dev \
    libqt5multimediawidgets5 \
    libqt5svg5-dev \
    ruby \
    ruby-dev \
    python3-dev \
    libz-dev \
    libgit2-dev \
    && rm -rf /var/lib/apt/lists/*

# Install KLayout from source
ARG KLAYOUT_TAG=v0.30.4
WORKDIR /root
RUN git clone https://github.com/KLayout/klayout
WORKDIR /root/klayout
RUN git checkout ${KLAYOUT_TAG}
RUN ./build.sh -qt5 -j$(nproc)
RUN cp -r bin-release /usr/local/klayout
RUN ln -s /usr/local/klayout/klayout /usr/local/bin/klayout
RUN rm -rf /root/klayout

# Install ngspice dependencies and ngspice
RUN apt-get update && apt-get install -y \
    libxaw7-dev \
    libx11-dev \
    libxext-dev \
    libxmu-dev \
    libxrender-dev \
    libcairo2-dev \
    libpango1.0-dev \
    && rm -rf /var/lib/apt/lists/*

# Install ngspice from source
ARG NGSPICE_TAG=ngspice-43
WORKDIR /root
RUN git clone git://git.code.sf.net/p/ngspice/ngspice
WORKDIR /root/ngspice
RUN git checkout ${NGSPICE_TAG}
RUN ./autogen.sh
RUN ./configure --enable-openmp --with-readline
RUN make -j$(nproc)
RUN make install
RUN rm -rf /root/ngspice

# Install OpenROAD-flow-scripts
WORKDIR /root
RUN git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts.git && \
    cd OpenROAD-flow-scripts && \
    ./build_openroad.sh --local

# Set environment variables for OpenROAD
ENV PATH="/root/OpenROAD-flow-scripts/tools/install/OpenROAD/bin:${PATH}"
ENV PATH="/root/OpenROAD-flow-scripts/tools/install/yosys/bin:${PATH}"

# Set working directory
WORKDIR /root/OpenROAD-flow-scripts

# Create a helper script to source environment
RUN echo '#!/bin/bash\nsource /root/OpenROAD-flow-scripts/env.sh' > /usr/local/bin/setup-orfs && \
    chmod +x /usr/local/bin/setup-orfs

CMD ["/bin/bash"]
