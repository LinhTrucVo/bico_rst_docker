# =============================================================================
# Sphinx Documentation Builder with RST Support
# =============================================================================
# This Dockerfile creates a comprehensive environment for building Sphinx 
# documentation with reStructuredText (RST) support, including PlantUML 
# diagrams and various Sphinx extensions.
#
# Base Image: Ubuntu 22.04 LTS (Jammy Jellyfish)
# Primary Use: Documentation generation, RST editing, Sphinx building
# =============================================================================

FROM ubuntu:22.04

# =============================================================================
# IMAGE METADATA
# =============================================================================
# Labels provide metadata about the image for identification and management
LABEL name="bico-rst"
LABEL version="1.0.0"
LABEL description="Sphinx documentation builder with RST support and PlantUML integration"
LABEL maintainer="bico"
LABEL org.opencontainers.image.title="Bico RST Documentation Builder"
LABEL org.opencontainers.image.description="Complete environment for Sphinx documentation with RST, PlantUML, and development tools"
LABEL org.opencontainers.image.version="1.0.0"

# =============================================================================
# ENVIRONMENT CONFIGURATION
# =============================================================================
# Prevent interactive prompts during package installation
# This is crucial for automated Docker builds
ENV DEBIAN_FRONTEND=noninteractive

# Set locale to prevent encoding issues with documentation
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

# PlantUML JAR path - will be set after downloading the JAR file
ENV PLANTUML_JAR_PATH=/usr/bin/plantuml.jar

# =============================================================================
# SYSTEM DEPENDENCIES INSTALLATION
# =============================================================================
# Install essential system packages required for:
# - Java Runtime Environment (for PlantUML)
# - Graphviz (for diagram generation)
# - Python development tools
# - Build essentials for compiling Python packages
# - Curl for downloading external resources
RUN apt-get update && \
    apt-get install -y \
        # Java Runtime Environment - Required for PlantUML execution
        default-jre \
        # Graphviz - Graph visualization software for generating diagrams
        graphviz \
        # Curl - Command line tool for downloading files from URLs
        curl \
        # Python interpreter and development tools
        python-is-python3 \
        python3-pip \
        python3-dev \
        # Build essentials - Compiler and libraries for building Python packages
        build-essential \
        # Additional useful tools
        git \
        vim \
        nano && \
    # Clean up apt cache to reduce image size
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

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
    # Core Sphinx documentation generator
    sphinx==8.1.3 \
    # Sphinx themes and styling
    sphinx-rtd-theme==3.0.2 \
    # Data visualization extensions
    sphinx-data-viewer==0.1.5 \
    # Core Sphinx contrib packages for various output formats
    sphinxcontrib-applehelp==2.0.0 \
    sphinxcontrib-devhelp==2.0.0 \
    sphinxcontrib-htmlhelp==2.1.0 \
    sphinxcontrib-qthelp==2.0.0 \
    sphinxcontrib-serializinghtml==2.0.0 \
    # Mathematical and interactive content support
    sphinxcontrib-jsmath==1.0.1 \
    sphinxcontrib-jquery==4.1 \
    # Diagram and drawing extensions
    sphinxcontrib-drawio==0.0.17 \
    sphinxcontrib-plantuml==0.30 \
    # Program output and execution extensions
    sphinxcontrib-programoutput==0.18 \
    # Requirements management and traceability
    sphinx_needs==5.1.0 \
    # C++ documentation support (Doxygen integration)
    breathe==4.36.0 \
    # Document linting and quality checking tools
    doc8==1.1.2 \
    restructuredtext_lint==1.4.0 \
    rstcheck==6.2.5 \
    rstcheck-core==1.2.2 \
    # Core documentation utilities
    docutils==0.21.2 \
    # Language server for enhanced RST editing experience
    esbonio==0.16.5 \
    # YAML parsing support (often needed for configuration files)
    pyyaml==6.0

# =============================================================================
# PLANTUML INSTALLATION
# =============================================================================
# Download and install PlantUML JAR file for UML diagram generation
# PlantUML is a component that allows to quickly write UML diagrams using a simple textual description language
RUN curl -L -o /usr/bin/plantuml.jar \
    https://github.com/plantuml/plantuml/releases/download/v1.2025.3/plantuml-1.2025.3.jar && \
    # Make the JAR file executable (though not strictly necessary, it's good practice)
    chmod +x /usr/bin/plantuml.jar

# =============================================================================
# WORKING DIRECTORY SETUP
# =============================================================================
# Set the default working directory for the container
# This is where the documentation source files will be located
WORKDIR /workspace

# =============================================================================
# CONTAINER RUNTIME CONFIGURATION
# =============================================================================
# Set the default command to keep the container running
# This allows the devcontainer to remain active for development work
CMD ["sleep", "infinity"]

# =============================================================================
# USAGE NOTES
# =============================================================================
# This container provides a complete environment for:
# 1. Editing reStructuredText (RST) files with syntax highlighting and linting
# 2. Building Sphinx documentation with multiple output formats (HTML, PDF, etc.)
# 3. Creating UML diagrams with PlantUML integration
# 4. Validating documentation quality with multiple linting tools
# 5. Managing documentation requirements and traceability with sphinx_needs
#
# To use this container:
# 1. Mount your documentation source directory to /workspace
# 2. Run sphinx-build commands to generate documentation
# 3. Use the various linting tools (doc8, rstcheck) to validate your content
# 4. Leverage PlantUML for creating technical diagrams
# =============================================================================
