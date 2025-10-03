# VLSI Design Codespace

A GitHub Codespace environment for VLSI design workflows with OpenROAD, KLayout, and ngspice.

## Included Tools

- **OpenROAD-flow-scripts**: Complete RTL-to-GDS flow
- **OpenROAD**: Open-source physical design tools
- **KLayout**: Layout viewer and editor (v0.30.4)
- **ngspice**: Circuit simulator (v43)
- **sky130 PDK**: Installed via ciel

## Getting Started

See the [chip-tutorials](chip-tutorials/README.md) for tutorials and examples.

## Notes

- Based on the official `openroad/orfs` Docker image
- OpenROAD environment is automatically sourced in each terminal
- KLayout tech files are linked from chip-tutorials
- VNC desktop available on port 6080 (password: `bananaslugs!`)
