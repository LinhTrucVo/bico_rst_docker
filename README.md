# 📚 Bico RST Documentation Builder

A comprehensive Docker-based development environment for building Sphinx documentation with reStructuredText (RST) support, PlantUML integration, and professional documentation tools.

**Note**: This project provides the development environment only. Your documentation source files come from separate repositories that you mount into the container.

## 🎯 Purpose

This devcontainer environment allows you to:
- Work with any Sphinx project
- Edit RST files with full IDE support
- Build documentation without installing tools locally
- Maintain consistent documentation builds across teams

##  Features

- **Complete Sphinx Environment** - Latest Sphinx with extensive plugin ecosystem
- **RST Support** - Full reStructuredText editing with syntax highlighting and linting
- **PlantUML Integration** - Create UML diagrams directly in your documentation
- **Quality Tools** - Built-in linting and validation (doc8, rstcheck, restructuredtext_lint)
- **VS Code Integration** - Optimized devcontainer with essential extensions
- **Live Preview** - Real-time documentation preview with Esbonio language server
- **Multi-format Output** - Generate HTML, PDF, and other documentation formats

## 📋 Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running
- [Visual Studio Code](https://code.visualstudio.com/) with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## 🛠️ Quick Start

### 1. Prepare Your Project

You need a separate project with Sphinx source files:

**Option A: Use the example project**
```bash
git clone https://github.com/VoLinhTruc/sphinx_test.git
```

**Option B: Use your existing project**
- Ensure it has a `docs/` folder with `conf.py` and RST files

### 2. Clone This Development Environment

```bash
git clone https://github.com/LinhTrucVo/bico_rst_docker.git
cd bico_rst_docker
```

### 3. Configure Your Documentation Paths

⚠️ **IMPORTANT**: Update the paths in `.devcontainer/devcontainer.json`:

```jsonc
"mounts": [
  "source=C:\\Path\\To\\Your\\sphinx_test,target=/mnt/project,type=bind",
  "source=C:\\Path\\To\\Your\\Build\\Output,target=/mnt/_build,type=bind"
]
```

### 4. Open in VS Code

1. Open the project folder in VS Code
2. Press `Ctrl+Shift+P` → "Dev Containers: Reopen in Container"
3. Wait for the container to build (first time takes a few minutes)

## 📁 Project Structure

```
bico_rst_docker/                    # This development environment
├── .devcontainer/
│   ├── devcontainer.json          # VS Code devcontainer configuration
│   ├── Dockerfile                 # Container definition with all tools
│   └── docker-compose.yml         # Optional: Docker Compose setup
└── README.md                      # This file

your-project/                       # Your separate project
├── docs/                          # Sphinx documentation source
│   ├── conf.py                    # Sphinx configuration
│   ├── index.rst                  # Main documentation file
│   └── ...                       # Your RST files
```

## � What's Included

### Container Configuration
- **Base Image**: Ubuntu 22.04 LTS
- **Python**: Python 3.10+ with pip
- **Java Runtime**: For PlantUML support
- **Build Tools**: GCC, make, and development headers

### VS Code Extensions
- **Esbonio** - Sphinx language server with live preview
- **reStructuredText Pack** - Comprehensive RST support
- **PlantUML** - UML diagram support and preview

### Key Python Packages
- `sphinx==8.1.3` - Core documentation generator
- `sphinx-rtd-theme==3.0.2` - Read the Docs theme
- `sphinxcontrib-plantuml==0.30` - PlantUML integration
- `doc8==1.1.2` - Documentation linting
- `rstcheck==6.2.5` - RST validation

## 📖 Usage

### Building Documentation

```bash
# Build HTML documentation
sphinx-build -b html /mnt/project/docs /mnt/_build

# Clean build
sphinx-build -E -a -b html /mnt/project/docs /mnt/_build
```

### Quality Checking

```bash
# Check documentation style
doc8 /mnt/project/docs

# Validate RST syntax
rstcheck /mnt/project/docs/*.rst
```

### PlantUML Diagrams

```rst
.. uml::

   @startuml
   Alice -> Bob: Hello
   Bob -> Alice: Hi there
   @enduml
```

## 🔍 Troubleshooting

**Container won't start:**
- Check Docker Desktop is running
- Verify paths in `devcontainer.json` exist
- Try rebuilding: `Ctrl+Shift+P` → "Dev Containers: Rebuild Container"

**Build errors:**
- Check `conf.py` syntax
- Use `sphinx-build` with `-v` flag for verbose output

**Live preview not working:**
- Restart language server: `Ctrl+Shift+P` → "Esbonio: Restart Language Server"

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test in the devcontainer
4. Submit a pull request

## 🙏 Acknowledgments

- [Sphinx](https://www.sphinx-doc.org/) - Documentation generator
- [PlantUML](https://plantuml.com/) - UML diagram creation
- [Esbonio](https://github.com/swyddfa/esbonio) - Sphinx language server

---

**Happy documenting! 📝✨**
