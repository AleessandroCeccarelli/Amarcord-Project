# Amarcord

A native Apple emulation framework in Swift and Metal.

## About

Amarcord is an independent, native emulation framework designed for Apple platforms.

The project is being developed in Swift and Metal with a modular architecture focused on hardware emulation, performance, portability and integration with the Apple ecosystem.

The first development target is the Nintendo Entertainment System (NES).

The long-term goal is to provide a complete emulation environment for multiple classic systems while keeping the architecture modular and native to Apple platforms.

## Current Development

NES emulation is currently under active development.

The current work focuses on completing the NES hardware implementation and integrating all the components required for a complete end-to-end system, including:

- CPU
- Bus and memory mapping
- PPU and video
- APU and audio
- Cartridge and mapper support
- DMA
- Interrupt handling
- Controller input
- Timing and synchronization
- Save and save states
- Filesystem integration
- ROM recognition and importing
- ROM database
- Metadata and artwork integration
- Amarcord Core integration

The first major milestone is to run and validate a real NES ROM through the complete Amarcord pipeline.

## Architecture

Amarcord is being developed as a modular system where emulation hardware, platform services and application-level components have clearly separated responsibilities.

The architecture is designed around native Apple technologies and avoids relying on an external emulator runtime.

## Technical References

During development, existing emulator projects and technical documentation may be studied as references to understand hardware behaviour and emulation techniques.

MAME is used as a technical reference during development.

Amarcord does not use the MAME emulator runtime and does not use a MAME bridge.

Amarcord's emulation components are independently implemented as part of the Amarcord project.

## Project Status

Amarcord is an active development project and is not currently considered a finished emulator.

The public repository is intended to document the project, its architecture and its development progress.

## Community & Technical Discussion

Experienced developers with knowledge of emulation, CPU/PPU architecture, Swift, Metal or Apple platform development are welcome to discuss the project and provide technical feedback.

Constructive technical reviews and independent opinions are particularly welcome.

## Source Code

Amarcord is proprietary, closed-source software.

The source code is not publicly distributed through this repository.

All rights reserved.

## Author

Copyright © 2026 Alessandro Ceccarelli.

Amarcord — Proprietary Software.