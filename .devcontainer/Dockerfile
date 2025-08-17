FROM ubuntu:22.04

LABEL name="bico-rst"
LABEL version="1.0.0"
LABEL description="Sphinx documentation builder with RST support + PlantUML + Doxygen"
LABEL maintainer="bico"
LABEL org.opencontainers.image.title=name
LABEL org.opencontainers.image.version=version
LABEL org.opencontainers.image.description=description

# If you use proxy, set the following environment variables
# ENV MY_PROXY_IP=...
# ENV MY_PROXY_PORT=...
# ENV MY_PROXY_USER_NAME=...
# ENV MY_PROXY_PASSWORD=...
# ENV http_proxy=http://$MY_PROXY:$MY_PROXY_PORT
# ENV https_proxy=http://$MY_PROXY:$MY_PROXY_PORT

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV PLANTUML_JAR_PATH=/usr/bin/plantuml.jar

RUN apt-get update && \
    apt-get install -y \
        build-essential \
        default-jre \
        graphviz \
        curl \
        python-is-python3 \
        python3-pip \
        python3-dev \
        # Ubuntu instal CMake 3.22.1 by default, but we need 3.22.2, the 3.22.2 installation is done later
        # cmake \
        doxygen \
        git \
        vim \
        nano \
        wget

# Clean up apt cache to reduce image size
# RUN apt-get clean && \
    # rm -rf /var/lib/apt/lists/*

# =============================================================================
# PYTHON PACKAGE MANAGEMENT SETUP
# =============================================================================
# Upgrade pip, setuptools, and wheel to latest versions
# This ensures compatibility with modern Python packages and build systems
RUN python3 -m pip install --upgrade pip setuptools wheel

# =============================================================================
# SPHINX AND DOCUMENTATION DEPENDENCIES
# =============================================================================
# Install comprehensive set of Sphinx-related packages for documentation building
RUN python3 -m pip install --no-cache-dir \
    sphinx==8.1.3 \
    sphinx-rtd-theme==3.0.2 \
    sphinx-data-viewer==0.1.5 \
    sphinxcontrib-applehelp==2.0.0 \
    sphinxcontrib-devhelp==2.0.0 \
    sphinxcontrib-htmlhelp==2.1.0 \
    sphinxcontrib-qthelp==2.0.0 \
    sphinxcontrib-serializinghtml==2.0.0 \
    sphinxcontrib-jsmath==1.0.1 \
    sphinxcontrib-jquery==4.1 \
    sphinxcontrib-drawio==0.0.17 \
    sphinxcontrib-plantuml==0.30 \
    sphinxcontrib-programoutput==0.18 \
    sphinx_needs==5.1.0 \
    breathe==4.36.0 \
    doc8==1.1.2 \
    restructuredtext_lint==1.4.0 \
    rstcheck==6.2.5 \
    rstcheck-core==1.2.2 \
    docutils==0.21.2 \
    esbonio==0.16.5 \
    pyyaml==6.0

# Set the default working directory for the container
WORKDIR /workspaces
RUN mkdir -p /mnt/project && mkdir -p /mnt/_build

# Download and install PlantUML JAR file for UML diagram generation
# If using proxy, replace <userName> and <password> with actual credentials
# RUN curl --proxy-ntlm -x http://$MY_PROXY_USER_NAME:$MY_PROXY_PASSWORD@$MY_PROXY_IP:$MY_PROXY_PORT \
#     -L -o /usr/bin/plantuml.jar \
#     https://github.com/plantuml/plantuml/releases/download/v1.2025.3/plantuml-1.2025.3.jar
# If not using proxy, use the following line instead
RUN curl -L -o /usr/bin/plantuml.jar \
    https://github.com/plantuml/plantuml/releases/download/v1.2025.3/plantuml-1.2025.3.jar

# CMake 3.22.2 installation
RUN wget -P /workspaces/cmake_3.22.2 https://github.com/Kitware/CMake/releases/download/v3.22.2/cmake-3.22.2-linux-x86_64.tar.gz && \
    mkdir -p /opt/cmake && \
    tar -zxvf /workspaces/cmake_3.22.2/cmake-3.22.2-linux-x86_64.tar.gz -C /opt/cmake && \
    ln -s /opt/cmake/cmake-3.22.2-linux-x86_64/bin/cmake /usr/local/bin/cmake

# Bazel installation
# RUN curl --proxy-ntlm -x http://$MY_PROXY_USER_NAME:$MY_PROXY_PASSWORD@$MY_PROXY_IP:$MY_PROXY_PORT \
#     -L -o /usr/local/bin/bazel \
#     https://github.com/bazelbuild/bazelisk/releases/download/v1.27.0/bazelisk-linux-amd64
# RUN chmod +x /usr/local/bin/bazel
# RUN bazel --version


# Set the default command to keep the container running
# This allows the devcontainer to remain active for development work
CMD ["sleep", "infinity"]