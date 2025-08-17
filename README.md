# 📚 Bico RST Documentation Builder

A comprehensive Docker-based development environment for building Sphinx documentation with reStructuredText (RST) support, PlantUML, Doxygen, and documentation tools.

**Note**: This project provides the development environment only. Your documentation source files come from separate repositories that you mount into the container.

## 🎯 Purpose

This devcontainer environment allows you to:

- **Live Preview in VSCode**
- Edit RST files with full IDE support
- Build documentation without installing tools locally

## Features

- **Complete Sphinx Environment** - Latest Sphinx with extensive plugin ecosystem
- **VS Code Integration** - Optimized devcontainer with essential extensions
- **Live Preview** - Real-time documentation preview with Esbonio language server
- **RST Support** - Full reStructuredText editing with syntax highlighting and linting

## 📋 Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running
- [Visual Studio Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## 🛠️ Quick Start

### 1. Prepare Your Project

**Option A: Use your existing project**

- Ensure it has `conf.py` and RST files

**Option B: Use the example project**

```bash
git clone https://github.com/VoLinhTruc/sphinx_test.git
```

### 2. Clone This Development Environment

```bash
git clone https://github.com/LinhTrucVo/bico_rst_docker.git
cd bico_rst_docker
```

### 3. Configuration

⚠️ **IMPORTANT**: Update the proxy information in `.devcontainer\Dockerfile`

```dockerfile
ENV MY_PROXY_IP=...
ENV MY_PROXY_PORT=...
ENV MY_PROXY_USER_NAME=...
ENV MY_PROXY_PASSWORD=...
```

⚠️ **IMPORTANT**: Update the artifact paths in `.devcontainer/devcontainer.json`:

```jsonc
  "mounts": [
    // 📁 UPDATE THIS PATH
    "source=<PROJECT_DIRECTORY>,target=/mnt/project,type=bind",
    // 📁 UPDATE THIS PATH
    "source=<DOCUMENT_BUILT_DIRECTORY>,target=/mnt/_build,type=bind"
  ],
  // 📁 UPDATE THIS PATH
  "workspaceFolder": "<PROJECT_DOCUMENTATION_DIRECTORY>",  
```

Replace **<PROJECT_DIRECTORY>** with the absolute path to your project folder on your local machine (not in the container).
Replace **<DOCUMENT_BUILT_DIRECTORY>** with the absolute path to the folder on your local machine (not in the container) where your documentation build output is stored.
Replace **<PROJECT_DOCUMENTATION_DIRECTORY>** with the absolute path to the folder in container that contain your documentation source files (usually is the sub folder in the project folder).

### 4. Open in VS Code

1. Open the project folder in VS Code
2. Press `Ctrl+Shift+P` → "Dev Containers: Reopen in Container"
3. Wait for the container to build (first time takes a few minutes)

## 🔍 Troubleshooting

**Container won't start:**
- Check Docker Desktop is running
- Verify paths in `devcontainer.json` exist
- Try rebuilding: `Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

**Live preview not working:**
- Restart language server: `Ctrl+Shift+P` → "Esbonio: Restart Language Server"


## ❤ If this is useful for you :)
