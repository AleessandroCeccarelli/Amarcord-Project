# Amarcord — The Story

> A complicated piece of software should not require a complicated experience.

## The Beginning

Amarcord started with a simple idea.

What if emulation could be technically extremely complicated behind the scenes, while remaining extremely simple for the person using it?

The user should not have to understand emulators, cores, BIOS files, memory mappings, controller configurations, video settings, audio settings or dozens of technical options.

The idea was simple:

**Choose a game. Play.**

Everything else should be Amarcord's responsibility.

The software should take care of the decisions and technical details that would otherwise consume the user's time.

This principle became one of the foundations of Amarcord:

> **Complexity belongs inside the architecture, not in the user's experience.**

Amarcord is therefore not intended to be just a collection of emulators.

The long-term vision is a complete environment where hardware emulation, graphics, audio, controllers, storage, ROM recognition, metadata and application services work together as one coherent system.

---

## The Apple TV idea

The original direction for Amarcord was **Apple TV**.

The idea of bringing a native emulation experience to tvOS was one of the reasons the project started in the first place.

Apple TV presented an interesting challenge.

The platform is deliberately simple from the user's point of view, which matched the philosophy behind Amarcord perfectly:

**sit down, choose a game and play.**

At the beginning, the project was therefore designed with Apple TV in mind.

We explored the architecture, the platform limitations and the possibilities of building an emulation environment that could feel native to Apple rather than simply being a port of an existing emulator.

---

## Moving to macOS

During development, however, it became clear that macOS offered a much more flexible environment for building the project.

Development tools, debugging possibilities, filesystem access and the overall freedom of the platform made macOS a much more practical environment in which to build Amarcord.

The project therefore moved its primary development target to **macOS**.

This was not an abandonment of the Apple TV idea.

It was a change in development strategy.

macOS became the environment where Amarcord could be built, tested and understood with fewer restrictions.

---

## Apple TV is still part of the vision

The original tvOS idea has never been abandoned.

One of the architectural goals of Amarcord is to avoid building a system that is permanently tied to macOS.

The project is being structured so that the core emulation architecture and the platform-independent parts of the system can potentially be reused on other Apple platforms in the future.

This means that Apple TV remains part of Amarcord's long-term direction.

macOS is the development ground.

tvOS remains a possible destination.

The architecture is being built with that distinction in mind.

---

## From an emulator to a framework

As the project grew, the original idea of "an emulator" became something larger.

A complete emulation environment requires much more than a CPU and a video renderer.

It needs hardware emulation, timing, memory, cartridges, controllers, audio, video, storage, save states and communication between all of these components.

It also needs the infrastructure surrounding the emulator.

That led Amarcord toward a modular architecture containing concepts such as:

- Amarcord Core
- Console and Machine abstractions
- CPU
- Bus and memory
- PPU
- APU
- DMA
- Interrupt handling
- Cartridge and mapper systems
- Controller hardware
- Timing and synchronization
- Video
- Audio
- Filesystem
- Save and Save State systems
- ROM recognition
- ROM importing
- ROM database
- Metadata and artwork services

The important part is not the number of components.

It is the separation of responsibilities.

Each component should have a clear purpose and communicate with the rest of the system through defined boundaries.

---

## The first system: NES

The **Nintendo Entertainment System** became the first complete system targeted by Amarcord.

The NES is complex enough to expose the difficult parts of emulation while remaining a manageable first target.

The decision was therefore made to complete the NES properly before moving on to additional systems.

The goal is not simply to make an NES game appear on screen.

The goal is to complete the entire path:

```text
ROM
 ↓
Importer
 ↓
Recognizer
 ↓
ROM Database
 ↓
Library / Filesystem
 ↓
NES Hardware
 ↓
CPU / Bus / PPU / APU / DMA
 ↓
Controller / Audio / Video
 ↓
Amarcord Core
 ↓
User

Only when this complete pipeline works reliably should Amarcord move toward other systems.

⸻

The ScreenScraper idea

Another important part of the original vision was that the user should not have to manually organize and identify everything.

A game library should be able to understand what has been imported and present useful information about it.

This led to the integration of ScreenScraper.

The role of ScreenScraper in Amarcord is not to emulate anything.

Its role is to enrich recognized games with information such as:

* game metadata
* artwork
* titles
* regional information
* descriptive information
* other available library information

The important architectural distinction is that Amarcord first needs to understand what the ROM is.

The Recognizer and ROM Database are therefore responsible for identifying the software.

ScreenScraper then becomes the metadata and artwork layer built on top of that identity.

The intended flow is:
ROM
 ↓
Amarcord Recognizer
 ↓
ROM identity
 ↓
ScreenScraper
 ↓
Metadata + Artwork
 ↓
Amarcord Library

This separation is important.

The emulator should not have to understand online metadata services.

The library should not have to understand CPU emulation.

Each part should do one job.

⸻

ROM recognition and the database

As the project evolved, another requirement became clear.

Amarcord needs a reliable way to understand imported software before placing it into the library.

This led to the concept of a centralized ROM database.

The current direction is to use XML data describing supported software and systems, with a common Amarcord service responsible for loading, parsing, normalizing and making that information available to the rest of the application.

The intention is to avoid having multiple independent components trying to understand the same ROM database.

One source.

One service.

Multiple consumers.

The Recognizer, Importer, Library and metadata system can therefore work from the same information.

⸻

The MAME chapter

MAME played an important role during the development of Amarcord.

At one point, the idea was to bring MAME itself into Amarcord.

A bridge between Amarcord and MAME was considered as a possible way of obtaining a large amount of existing emulation functionality.

It was an attractive idea for obvious reasons.

MAME is an enormous body of knowledge and existing emulation work.

But it also created a fundamental problem.

It would have changed what Amarcord actually was.

Instead of building an independent Apple-native emulation framework, Amarcord would have become an application built around an external emulator runtime.

That was not the original vision.

⸻

The decision to turn back

The decision was therefore made to take a step back.

The MAME runtime and the bridge approach were abandoned.

Amarcord would be built as its own project.

The emulation architecture would be implemented in Swift and Metal, with the original hardware behaviour studied through technical references and existing emulator projects where appropriate.

MAME remains a technical reference during development.

It is not Amarcord’s runtime.

There is no MAME bridge.

The goal is to keep Amarcord as clean, native and independent as possible.

This decision made development harder.

It also made the project more meaningful.

Instead of connecting existing pieces together, we are building the architecture ourselves.

⸻

The cost of doing it independently

Building an emulator from the ground up is not a small task.

A component can compile perfectly and still be wrong.

A CPU can execute instructions correctly but fail because the bus does not behave correctly.

A PPU can render pixels but still be incorrect because of timing.

DMA can appear to work while stealing the wrong number of CPU cycles.

Interrupts can be individually correct while being incorrectly routed through the machine.

A mapper can work in isolation and fail when connected to a real cartridge.

This is one of the most important lessons of Amarcord’s development:

Compilation is not validation.

The architecture has to work as a system.

That is why the project is being developed progressively, with integration becoming increasingly important as each hardware component is completed.

⸻

The difficult part: integration

One of the biggest challenges is not writing individual components.

It is making them behave correctly together.

The NES is a collection of tightly connected pieces.

CPU, PPU, APU, DMA, interrupts, cartridge hardware, controllers and timing all influence each other.

The same principle applies to Amarcord itself.

The emulator must eventually communicate correctly with:

* Amarcord Core
* Video
* Audio
* Controllers
* Filesystem
* Save systems
* Importer
* Recognizer
* ROM Database
* Metadata services

This is why the project is deliberately resisting the temptation to simply keep adding isolated features.

The goal is to build a system.

⸻

Human + AI

Amarcord is also an experiment in a different way of developing software.

The project is being developed through a collaboration between a human and AI.

AI contributes to technical exploration, architecture discussions, implementation, analysis and review.

The final direction of Amarcord, however, remains a human decision.

The project is not an attempt to pretend that everything is being done by a traditional software engineering team.

It is an experiment in what can be built when a technology enthusiast, persistent curiosity and AI-assisted development work together.

The important thing is not to hide that process.

The important thing is to make something real.

⸻

Where Amarcord is today

Amarcord is still an active development project.

The NES remains the primary target.

The current priority is to complete the NES hardware and connect it properly to the rest of Amarcord.

The project must eventually reach the point where a real game can travel through the complete pipeline:

ROM
 ↓
Import
 ↓
Recognition
 ↓
Library
 ↓
NES
 ↓
Controller
 ↓
Audio
 ↓
Video
 ↓
Save / State
 ↓
Playable game

Only after this complete path has been validated will additional emulators become the next priority.

⸻

What comes next

The long-term vision remains larger than the NES.

Possible future systems include:

* Super Nintendo
* Master System
* Mega Drive
* PlayStation

But the philosophy remains the same.

Build the architecture carefully.

Keep the user experience simple.

Do not add complexity where it is not necessary.

And make Amarcord responsible for the complicated parts.

The user should never have to care how difficult the software is.

They should simply be able to:

Choose a game.

Play.

⸻

An evolving story

This document is intentionally not a final specification.

Amarcord is still being built.

Architecture will evolve.

Ideas will change.

Some decisions will prove wrong.

New problems will appear.

This file will be updated from time to time to document those changes and preserve the story of how Amarcord evolves.

The goal is not to pretend that the path was perfectly planned from the beginning.

The goal is to document the real path.

⸻

Amarcord — Proprietary Software
Copyright © 2026 Alessandro Ceccarelli. All rights reserved.

