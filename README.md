# Amarcord

### A native Apple emulation framework in Swift and Metal

Amarcord is an independent emulation project built specifically around Apple's platforms and technologies.

The project is written in **Swift** and **Metal**, with a modular architecture designed to reproduce classic hardware while taking advantage of the Apple ecosystem.

---

## The idea

Amarcord is an exploration of how a modern emulation framework can be designed natively for Apple platforms.

The goal is not simply to make games run.

The goal is to build a complete, modular system where hardware emulation, graphics, audio, input, storage and application services work together as a single architecture.

---

## First milestone — NES

Development is currently focused on the **Nintendo Entertainment System**.

The NES implementation is being developed component by component, including:

- CPU
- Bus and memory
- PPU and video
- APU and audio
- DMA
- Interrupts
- Controllers
- Cartridge and mappers
- Timing and synchronization
- Save and save states

The first major milestone is to complete the NES hardware and validate it through the complete Amarcord pipeline.

```text
ROM
 │
 ▼
Importer
 │
 ▼
Recognizer
 │
 ▼
ROM Database
 │
 ▼
Library / Filesystem
 │
 ▼
NES
 ├── CPU
 ├── Bus
 ├── PPU
 ├── APU
 ├── DMA
 ├── Controllers
 └── Cartridge
 │
 ├── Audio
 └── Video / Metal
 │
 ▼
Amarcord Core
```

---

## Native Apple architecture

Amarcord is designed around native Apple technologies.

### Swift

Used for the emulation architecture, hardware components, services and application logic.

### Metal

Used for the graphics pipeline, with the objective of keeping video processing as close to the GPU as possible.

### Apple platforms

The architecture is being developed with Apple's frameworks and platform capabilities in mind rather than relying on an external emulator runtime.

---

## Architecture

Amarcord is organized around independent components with clearly defined responsibilities.

The long-term architecture includes:

- Emulation Core
- Console and Machine abstraction
- Hardware components
- Cartridge and mapper system
- Video pipeline
- Audio pipeline
- Controller system
- Filesystem
- ROM Importer
- ROM Recognizer
- ROM Database
- Metadata and artwork services
- Save and Save State system

The intention is to keep the architecture modular so that new systems can be introduced without redesigning the entire framework.

---

## Technical references

Emulation development requires understanding how the original hardware behaves.

Existing emulator projects, hardware documentation and technical material may therefore be studied as references during development.

MAME is used as a technical reference.

Amarcord does not use the MAME emulator runtime and does not use a MAME bridge.

The Amarcord emulation components are independently implemented as part of this project.

---

## Current status

Amarcord is an active development project.

The current priority is to complete the NES implementation and connect it to the rest of the Amarcord architecture.

The project is not yet a finished emulator.

There is still substantial hardware implementation, integration and validation work ahead.

---

## Future systems

Once the NES implementation and complete Amarcord pipeline have been validated, development can move toward additional classic systems.

The architecture is intended to support systems such as:

- Super Nintendo
- Master System
- Mega Drive
- PlayStation

The NES remains the first complete target.

---

## Technical discussion

The public repository exists as a project showcase and as a place for technical discussion.

Developers with experience in:

- emulation
- CPU / PPU / APU architecture
- Swift
- Metal
- Apple platforms
- low-level systems

are welcome to review the architecture, ask questions and share constructive technical feedback.

The Discussions section is the preferred place for technical conversations.

---

## Source code

Amarcord is proprietary, closed-source software.

The public repository contains project information, documentation and development material.

The Amarcord source code is not publicly distributed.

All rights reserved.

---

## Author

Alessandro Ceccarelli

Technology enthusiast, exploring emulation and Apple platforms with a little help from AI.

---

Amarcord — Proprietary Software
Copyright © 2026 Alessandro Ceccarelli. All rights reserved.
