# `Aster`

> A vertical language from intent to silicon.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Status](https://img.shields.io/badge/status-experimental-red.svg)
![Version](https://img.shields.io/badge/version-0.0.x--prototype-orange.svg)

**`Aster`** is a statically-typed systems language designed around one invariant:

> Human intent must survive lowering.

`Aster` spans conceptual guarantees, structural definition, deterministic behavior, and exact machine execution — without implicit transitions, silent abstraction, or semantic leakage.

Source files use the `.ax` extension.
The compiler CLI is `ax`.

---

# Design Overview

`Aster` is built around three orthogonal axes:

1. **Epistemic Modes** — how we reason about systems
2. **Targets** — where code executes
3. **Domain Profiles** — what constraints apply

These axes are independent and composable.

---

# I. Epistemic Modes (Fixed, Universal)

`Aster` defines exactly four epistemic modes.
They are permanent and non-negotiable.

They are not runtime switches.
They are layers of truth.

---

## 1. Concept Mode — *Why*

Expresses:

* Invariants
* Guarantees
* Safety constraints
* Capability policies
* SLOs

Properties:

* Non-executable
* No time
* No memory
* No control flow

Concept Mode constrains all lower layers.
If intent cannot be upheld → compile error.

---

## 2. Structure Mode — *What exists*

Defines:

* Types
* Ownership models
* Memory layout
* Component topology
* Interfaces

Properties:

* Non-executable
* Deterministic
* Spatial (not temporal)

Structure Mode shapes the ontology of the system.

---

## 3. Control Mode — *How it behaves*

Defines:

* Algorithms
* Explicit control flow
* Deterministic execution
* Concurrency
* Memory usage

Properties:

* Executable
* Explicit
* Abstracted from physical instruction selection

Most application logic lives here.

---

## 4. Machine Mode — *What silicon does*

Defines:

* Instruction DAGs (not linear assembly)
* Virtual registers
* Explicit memory contracts
* ISA-parametric intent (x86, ARM, RISC-V, WASM)
* Hard lowering guarantees

Rules:

* No optimizer freedom
* No implicit instruction selection
* No silent rewriting
* If lowering cannot be exact → compile error

Machine Mode is the lowest layer humans are allowed to author.

---

# II. Targets (Execution Backends)

Targets define where code executes.

They are not epistemic modes.
They are deployment envelopes.

Examples:

* `native`
* `hosted`
* `wasm`
* `bare`
* `kernel`

Targets may enable or restrict certain epistemic modes.

For example:

* `native` may allow Machine Mode
* `hosted` may seal Machine Mode
* `wasm` may restrict instruction contracts

Targets are extensible.

---

# III. Domain Profiles (Constraint Envelopes)

Domains define constraint profiles.

They:

* Enable or disable epistemic modes
* Restrict constructs
* Set concurrency and memory defaults
* Enforce safety guarantees

Domains do not add abstractions.
They remove freedom.

Examples:

### UI Domain

* Concept + Structure emphasized
* Machine Mode sealed
* Managed execution
* No timing guarantees

### Embedded Domain

* All modes allowed
* No allocation after init
* Fixed memory
* ISA restricted

### Systems Domain

* Structure + Control dominant
* Machine optional
* Deterministic concurrency

Domains are orthogonal to Targets.

---

# IV. Biomes

`Aster` projects are organized into **biomes**.

A biome is a directory governed by a `calyx.ax` configuration file.

Each biome defines:

* Target
* Domain profile
* Allowed epistemic modes
* Constraint policies

Example:

```
/my-project
  ├── /engine
  │   ├── calyx.ax
  │   └── physics.ax
  │
  ├── /ui
  │   ├── calyx.ax
  │   └── view.ax
  │
  └── `Aster`.toml
```

Architecture is spatial, not syntactic.

---

# Calyx Configuration

`calyx.ax` defines biome behavior.

Example:

```ax
import { Config } from "`Aster`/calyx"

export const Environment = Config.define({
    target: "native",
    domain: "embedded",
    machine: "enabled",
    safety: "strict"
})
```

Calyx does not introduce semantics.
It constrains them.

---

# 🌿 The Botanical Stack

`Aster` retains its botanical naming scheme, each tied to a concrete architectural role.

| Component         | Name                   | Description                                                                     |
| ----------------- | ---------------------- | ------------------------------------------------------------------------------- |
| Language          | **``Aster``**            | Vertically structured language spanning Concept → Structure → Control → Machine |
| Compiler          | **Proteus**            | Lowering engine translating `.ax` through IR into target backends               |
| Configuration     | **Calyx**              | Biome-level configuration (`calyx.ax`) defining target, domain, and constraints |
| Execution Backend | **Target**             | Deployment backend (`native`, `hosted`, `wasm`, etc.)                           |
| Domain Profile    | **Domain**             | Constraint envelope shaping semantics and capability                            |
| Boundary System   | **Graft**              | Explicit, generated bridges between biomes and targets                          |
| Standard Library  | **Lupine**             | Mode-aware, target-aware standard library                                       |
| Package Manager   | **Rhizome** (`ax rhi`) | Deterministic dependency resolution and distribution                            |
| Ephemeral Runner  | **`axx`**              | Fast experimental runner for development                                        |

---

# V. Graft — Explicit Boundary Crossing

When code crosses biome boundaries:

* Target differences are resolved
* Domain constraints are enforced
* Epistemic legality is checked
* Serialization or ABI layers are generated if required

There are no hidden FFI boundaries.

Graft makes cross-boundary interaction explicit and auditable.

---

# VI. Rhizome — Package Distribution

`Aster` uses **Rhizome** (`ax rhi`) for dependency management.

Rhizome is:

* Target-aware
* Domain-aware
* Deterministic
* Lockfile-driven

Example:

```bash
ax rhi add github.com/example/lib
ax build
```

---

# Language Basics (.ax)

## Primitive Types

```
i32
i64
f32
f64
bool
```

All types are explicit.

No implicit casting.
No hidden allocation.

---

## Structs (Structure Mode)

```ax
struct Vector3 {
    x: f64
    y: f64
    z: f64
}
```

---

## Functions (Control Mode)

```ax
pub func add(a: Vector3, b: Vector3) -> Vector3 {
    return Vector3 {
        x: a.x + b.x,
        y: a.y + b.y,
        z: a.z + b.z
    }
}
```

---

## Control Flow

```ax
if (cond) { }
while (cond) { }
```

---

# Compiler Architecture

The `ax` compiler pipeline:

```
.ax
  ↓
Lexer
  ↓
Parser → AST
  ↓
Type Check
  ↓
Typed IR
  ↓
Target Lowering
  ↓
Backend (Zig / WASM / etc.)
```

Machine Mode integrates before final lowering.

---

# CLI

Compile:

```bash
ax build file.ax
```

Run:

```bash
ax run file.ax
```

Ephemeral runner:

```bash
axx file.ax
```

---

# Current Implementation Status

The current public prototype focuses on:

* Structure + Control
* Deterministic lowering to Zig
* Native target
* No Machine Mode (yet)
* No hosted target (yet)

The vertical architecture is defined and will be implemented incrementally.

---

# Roadmap

| Version | Milestone                                                  |
| ------- | ---------------------------------------------------------- |
| v0.0.x  | Minimal deterministic lowering (Structure + Control → Zig) |
| v0.1    | Multi-file + Calyx + biome architecture                    |
| v0.2    | Ownership model                                            |
| v0.3    | Hosted target                                              |
| v0.4    | Machine Mode                                               |
| v1.0    | Stable vertical system                                     |

---

# Philosophy

`Aster` is not designed for convenience.
It is designed for correctness across layers.

> Where intent cannot be preserved, compilation must fail.

`Aster` defines the boundary between human reasoning and silicon execution — and refuses to blur it.

---

# License

MIT © 2026 `Aster`