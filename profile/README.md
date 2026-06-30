<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)">
    <img alt="Vora" src="./vora_logo.svg" height="120">
  </picture>
</p>

<h3 align="center">Vora — a dynamically typed scripting language.</h3>

<p align="center">
  <strong>JavaScript-like syntax. Lua-level simplicity. Wren-style object orientation.</strong>
</p>

<p align="center">
  <a href="https://github.com/Vora-lang/Vora/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-7c3aed"></a>
  <a href="https://github.com/Vora-lang/Vora-LSP"><img src="https://img.shields.io/badge/LSP-ready-blue"></a>
  <a href="https://github.com/Vora-lang/Vora-LSP"><img src="https://img.shields.io/badge/DAP-debugger-orange"></a>
  <a href="https://github.com/Vora-lang/Vora"><img src="https://img.shields.io/badge/standard-C%2B%2B17-00599C"></a>
</p>

---

## Quick look

```vora
// ── Objects with single & multiple inheritance (C3 MRO) ──
Obj Animal(name) {
    this.name = name
    func speak() { print(this.name + " makes a sound") }
}

Obj Dog : Animal(name, breed) {
    this.breed = breed
    func speak() { print("Woof! I'm " + this.name + " the " + this.breed) }
}

let d = Dog("Rex", "Husky")
d.speak()  // → Woof! I'm Rex the Husky

// ── Closures ──
func makeCounter(start) {
    func next() { start = start + 1; return start }
    return next
}
let c = makeCounter(0)
print(c())  // → 1
print(c())  // → 2

// ── Pattern matching ──
let grade = match 85 {
    90..=100 => "A",
    80..=89  => "B",
    70..=79  => "C",
    _        => "F"
}
print(grade)  // → B

// ── List comprehensions ──
let squares = [i * i for i in range(1, 6)]   // → [1, 4, 9, 16, 25]
let evens   = [i for i in range(20) if i % 2 == 0]

// ── Generators ──
func countTo(n) {
    for (let i = 1; i <= n; i = i + 1) { yield i }
}
for v in countTo(3) { print(v) }  // → 1, 2, 3

// ── Error handling with stack traces ──
try {
    throw {code: 404, message: "Not found"}
} catch (e) {
    print(e.message)  // → Not found
    print(e.stack)    // → file.va:2 — full call-stack trace
} finally {
    print("cleanup")
}
```

## Features

| Category | What's inside |
|----------|--------------|
| **Types** | Null, Bool, Int (`int64`), Float (`double`), String (UTF-8), Array, Dict, Set, Map, Function, Object |
| **Variables** | `let` (mutable), `const` (immutable), block-scoped, optional type annotations with runtime conversion |
| **Functions** | Closures, default/rest/named params, destructuring, lambdas, tail-call optimization |
| **Objects** | `Obj` keyword, single + multiple inheritance (C3 linearization), `super`, static methods |
| **Control flow** | `if`/`else`, `while`, `do`-`while`, C-style `for`, `for`-`in`, `match`, `break`/`continue` |
| **Error handling** | `try`/`catch`/`finally`, `throw` any value, auto `.stack` trace, `defer` |
| **Modules** | `import` / `from`-`import` / `export`, relative + stdlib resolution, circular import detection |
| **Generators** | `yield`, `iter()`/`next()` protocol, `StopIteration` |
| **Comprehensions** | List: `[expr for x in iter if cond]`, Dict: `{k: v for ...}` |
| **Operators** | `?.` optional chaining, `??` null-coalescing, `**` power (right-assoc), `++`/`--`, compound assignment |
| **String interpolation** | `"Hello ${name}!"`, `${obj.property}` nested |
| **Standard library** | `math`, `json`, `fs`, `os`, `datetime`, `array`, `string`, `regex` |
| **Tooling** | REPL, bytecode VM, `vora fmt`, LSP server, DAP debugger |
| **Embedding** | Single-header `vora.hpp` + `vora_lib.lib`, VM public API, zero external dependencies |
| **Performance** | NaN-boxed 8-byte Value, superinstruction fusion, constant folding, tail-call optimization |

## Build from source

```bash
# Prerequisites: CMake 3.21+, C++17 compiler (MSVC 2022 / GCC 11+ / Clang 14+)

# Quick build (interactive mode)
.\build.ps1          # Windows
./build.sh           # Linux / macOS

# Or specify target explicitly
.\build.ps1 -Architecture x64 -Config Release -Package    # → .msi installer
./build.sh -a x64 -c release -p                           # → .deb/.rpm/.pkg.tar.xz
```

~~Pre-built packages are available on the [Releases](https://github.com/Vora-lang/Vora/releases) page.~~

## Usage

```bash
vora hello.va         # execute a script
vora                  # interactive REPL
vora fmt -w file.va   # format source in-place
```

## Repositories

| | |
|-----|-----|
| [**Vora**](https://github.com/Vora-lang/Vora) | Language core — lexer, parser, AST, bytecode compiler, VM, stdlib |
| [**Vora-LSP**](https://github.com/Vora-lang/Vora-LSP) | LSP server (C++) + VS Code extension + DAP debug adapter |
| [**Vora-WASM**](https://github.com/Vora-lang/Vora-WASM) | Browser runtime via Emscripten + JavaScript bridge |
| [**Website**](https://github.com/Vora-lang/Vora-lang.github.io) | Generated user documentation site |

## Editor support

- **VS Code** — [`vora-lang`](https://marketplace.visualstudio.com/items?itemName=Vora-lang.vora-lang) extension: syntax highlighting, LSP (diagnostics, completion, go-to-def, hover, references, signature help), DAP debugger
- **Zed** — tree-sitter-vora grammar (developing)

---

<p align="center">
  <sub>Built with C++17. Zero external dependencies. <a href="https://github.com/Vora-lang/Vora/blob/main/LICENSE">MIT licensed</a>.</sub>
</p>
