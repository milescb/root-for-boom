FROM almalinux:9

LABEL maintainer.name="Miles Cochran-Branson"
LABEL maintainer.email="miles.cb@cern.ch"

ARG ROOT_VERSION=6.18.00
ARG PYTHON_VERSION=2.7

# Install dependencies
RUN yum install -y epel-release
RUN yum install -y git make cmake gcc-c++ gcc binutils \
libX11-devel libXpm-devel libXft-devel libXext-devel openssl-devel \
xrootd-client-devel xrootd-libs-devel
RUN yum install -y gcc-gfortran pcre-devel \
mesa-libGL-devel mesa-libGLU-devel glew-devel ftgl-devel mysql-devel \
fftw-devel cfitsio-devel graphviz-devel libuuid-devel \
avahi-compat-libdns_sd-devel openldap-devel python-devel python3-numpy \
libxml2-devel gsl-devel readline-devel qt5-qtwebengine-devel \
R-devel R-Rcpp-devel R-RInside-devel

WORKDIR /root-project
RUN git clone https://github.com/root-project/root.git /root_src
WORKDIR /root_src
RUN git checkout v6-18-00-patches
WORKDIR /..

# Configure and build ROOT
RUN mkdir root_build root_install 
WORKDIR /root_build
RUN cmake3 -DCMAKE_INSTALL_PREFIX=../root_install -DPYTHON_VERSION=${PYTHON_VERSION} ../root_src
RUN cmake3 --build . -- install -j4
RUN source ../root_install/bin/thisroot.sh

# Set environment variables
#ENV ROOTSYS=/usr/local
#ENV PATH=$ROOTSYS/bin:$PATH
#ENV LD_LIBRARY_PATH=$ROOTSYS/lib:$LD_LIBRARY_PATH
#ENV PYTHONPATH=$ROOTSYS/lib:$PYTHONPATH

# Clean up
RUN rm -rf ../root_build \
       && rm -rf ../root_src

# install and source happy dependency
#RUN git clone https://gitlab.cern.ch/ATauLeptonAnalysiS/HAPPy.git /happy
#WORKDIR happy
#RUN git checkout python2
#RUN source setup.sh


# Set default command to launch ROOT
#CMD ["root"]
