# 🌸 Aster

> **Composite Code. Cultivated Performance.**

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-0.1.0--alpha-green)
![Status](https://img.shields.io/badge/status-experimental-orange)

**Aster** (`.ax`) is a unified language environment that solves the *Two-Language Problem* by allowing high-level and low-level code to coexist in the **same syntax**, within the **same project**, under different execution contexts.

Instead of rewriting a prototype in another language, Aster lets you **change the environment**, not the code.

---

## 🌺 Philosophy

An **Aster** is a composite flower — what appears to be a single bloom is actually many structures working together.

* The **Core** is inward, dense, and deterministic — where structure and performance live.
* The **Crown** is outward, expressive, and adaptive — where interaction and iteration happen.

In Aster, your code does not change.
**Only its environment does.**

Execution behavior is defined by configuration, not syntax.

---

## 🌿 The Botanical Stack

| Component       | Name                | Description                                                 |
| --------------- | ------------------- | ----------------------------------------------------------- |
| Language        | **Aster**           | Unified syntax across execution environments                |
| Compiler        | **Proteus**         | Shape-shifting compiler targeting native or hosted runtimes |
| Config          | **Calyx**           | Directory-level configuration (`calyx.ax`)                  |
| Native Mode     | **Core**            | Deterministic, high-performance native execution            |
| Hosted Mode     | **Crown**           | Adaptive, dynamic, GC-managed execution                     |
| Interop         | **Graft**           | Auto-generated boundary bridges between Core and Crown      |
| Std Library     | **Lupine**          | Dual-mode standard library                                  |
| Package Manager | **Rhizome** (`rhi`) | Dependency distribution and resolution                      |

---

## 🏗️ Project Structure

Aster is **biome-based**.
Each directory defines its execution environment via a `calyx.ax` file.

```text
/my-project
  ├── /core              <-- Core biome (native)
  │   ├── physics.ax
  │   └── calyx.ax
  │
  ├── /ui                <-- Crown biome (hosted)
  │   ├── main.ax
  │   └── calyx.ax
  │
  └── aster.toml         <-- Workspace root
```

---

## 💻 Usage

### 1️⃣ Calyx Configuration

`calyx.ax` defines how all `.ax` files in the directory are compiled and executed.

### `/core/calyx.ax` — Core Environment

```javascript
import { Config } from "aster/calyx"

export const Environment = Config.define({
    mode: "core",          // Native execution
    safety: "strict",      // No unsafe memory
    optimization: "speed"
})
```

---

### `/ui/calyx.ax` — Crown Environment

```javascript
import { Config } from "aster/calyx"

export const Environment = Config.define({
    mode: "crown",         // Hosted execution
    platform: "web",
    hot_reload: true
})
```

---

## 2️⃣ Aster Code (`.ax`)

The syntax is consistent across environments — only semantics differ.

---

### Core Code (Native, Deterministic)

```typescript
struct Vector3 {
    x: f64
    y: f64
    z: f64
}

pub func add(v1: Vector3, v2: Vector3) -> Vector3 {
    return Vector3 {
        x: v1.x + v2.x,
        y: v1.y + v2.y,
        z: v1.z + v2.z
    }
}
```

This compiles to optimized native code via **Zig**.

---

### Crown Code (Hosted, Adaptive)

```typescript
import { Physics } from "../core/physics.ax"

func on_click() {
    let player_pos = { x: 10.0, y: 5.5, z: 0.0 }
    let move_vec   = { x: 1.0,  y: 0.0, z: 0.0 }

    // GRAFT:
    // Dynamic Crown objects are serialized and
    // packed automatically for Core execution.
    let new_pos = Physics.add(player_pos, move_vec)

    print("New Position: " + new_pos.x)
}
```

This runs in a hosted JavaScript runtime (QuickJS, browser, or embed).

---

## 🧬 Graft — Core ↔ Crown Interop

Cross-boundary calls require no manual FFI.

When Crown code calls Core code:

1. Proteus detects the boundary crossing
2. Generates a C-compatible serialization layer
3. Transforms layouts safely and deterministically
4. Executes native logic
5. Returns structured data back to Crown

You write **one function call**.

---

## 📦 Rhizome (Package Manager)

**Rhizome** distributes and resolves Aster modules across biomes.

```bash
# Add a dependency
aster rhi add https://github.com/aster-lang/lupine-math

# Build the workspace
aster build
```

Rhizome is environment-aware:
Core code never pulls Crown-only dependencies.

---

## 🌱 Lifecycle Vocabulary

Aster exposes execution and failure states explicitly:

* **Dormancy** — compiled but inactive
* **Bloom** — activated and live
* **Wilt** — recoverable degradation
* **Blight** — unrecoverable failure
* **Thorns** — enforced safety constraints

These are user-facing concepts, not internal jargon.

---

## 🚀 Getting Started

> ⚠️ Aster is currently **pre-alpha** and under active design.

```bash
curl -s https://aster-lang.org/install.sh | bash
aster init my-garden
cd my-garden
aster run ui/main.ax
```

---

## 🤝 Contributing

Aster is a solo-led project seeking thoughtful collaborators (“Gardeners”) in:

* **Proteus** — compiler & codegen
* **Lupine** — standard library expansion
* **Rhizome** — dependency resolution

---

## 📄 License

MIT © 2026 Aster Language
