# VLSI Design Codespace

A GitHub Codespace environment for VLSI design workflows with OpenROAD, KLayout, and ngspice.

## Included Tools

- **OpenROAD-flow-scripts**: Complete RTL-to-GDS flow
- **OpenROAD**: Open-source physical design tools
- **KLayout**: Layout viewer and editor
- **ngspice**: Circuit simulator

## Usage

### Setting up the environment

1. Click "Code" → "Create codespace on main" in GitHub
2. Wait for the container to build (first time may take 15-20 minutes)
3. Once ready, you'll have access to all tools

### Running OpenROAD

```bash
cd ~/OpenROAD-flow-scripts/flow
source ../env.sh
make
```

### Using KLayout

```bash
klayout
```

### Using ngspice

```bash
ngspice
```

### Testing OpenROAD installation

```bash
openroad -version
yosys -version
```

## Notes

- All tools are installed in `/root/OpenROAD-flow-scripts/`
- The environment is based on Ubuntu 22.04
- OpenROAD binaries are in the PATH
- Use `source /root/OpenROAD-flow-scripts/env.sh` to set up the OpenROAD environment
