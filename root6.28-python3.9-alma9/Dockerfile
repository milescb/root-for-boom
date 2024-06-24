FROM almalinux:9

LABEL maintainer.name="Miles Cochran-Branson"
LABEL maintainer.email="miles.cb@cern.ch"

ARG ROOT_VERSION=6.28.00
ARG PYTHON_VERSION=3.9

# Install dependencies
RUN dnf install -y epel-release
## Required dependencies
RUN dnf install -y git make cmake gcc-c++ gcc binutils \
    libX11-devel libXpm-devel libXft-devel libXext-devel openssl-devel \
    xrootd-client-devel xrootd-libs-devel python3-devel python3-numpy

# Clone appropriate version of ROOT
WORKDIR /root-project
RUN git config --global http.postBuffer 1048576000
RUN git clone --branch v6-28-00-patches --depth=1 https://github.com/root-project/root.git /root_src

# Configure and build ROOT
RUN mkdir root_build root_install 
WORKDIR /root_build
RUN cmake3 -DCMAKE_INSTALL_PREFIX=../root_install -DPYTHON_VERSION=${PYTHON_VERSION} ../root_src
RUN cmake3 --build . -- install -j4

# Set environment variables
ENV ROOTSYS=/root_install
ENV PATH=$ROOTSYS/bin:$PATH
ENV LD_LIBRARY_PATH=$ROOTSYS/lib:$LD_LIBRARY_PATH
ENV PYTHONPATH=$ROOTSYS/lib:$PYTHONPATH

# Clean up
WORKDIR /root-project
RUN rm -rf ../root_build \
       && rm -rf ../root_src

WORKDIR /boom
