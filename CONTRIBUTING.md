

### WSL2 / Ubuntu on Windows

For development on Windows, we recommend using WSL2 (Windows Subsystem for Linux) with Ubuntu. This setup allows you to follow the Ubuntu instructions below.

#### Prerequisites

1. **Install WSL2** and Ubuntu 22.04 or newer from Microsoft Store
2. **Node.js via nvm** (required version: see `.nvmrc`):
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
   source ~/.bashrc
   nvm install node
   nvm use node
   ```
3. **Yarn via corepack** (streamlit uses Yarn PnP, requires corepack):
   ```bash
   corepack enable
   corepack prepare yarn@stable --activate
   ```
4. **Protobuf compiler** (minimum 3.20):
   ```bash
   # Ubuntu 22.04 ships protoc 3.12 — too old!
   PROTOC_VERSION=3.20.0
   curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip
   sudo unzip -o protoc-${PROTOC_VERSION}-linux-x86_64.zip -d /usr/local bin/protoc
   sudo unzip -o protoc-${PROTOC_VERSION}-linux-x86_64.zip -d /usr/local 'include/*'
   protoc --version
   ```
5. **Build frontend dependencies**:
   ```bash
   make frontend-init
   ```

#### Common WSL2 Issues

- **`node_modules state file` error**: Run `cd frontend && yarn install --immutable` first
- **ECONNREFUSED on port 8501**: The dev server is still starting; wait a few seconds and refresh
- **libprotoc version error**: See step 4 above
