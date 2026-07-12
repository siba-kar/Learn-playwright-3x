# Compiler vs Interpreter — IQ Breakdown

## 1. The Big Picture

Both turn *human-readable source code* into *machine-executable instructions*. They just do it differently.

| Layer | Compiler | Interpreter |
|---|---|---|
| **Translation timing** | Ahead of time (whole program at once) | On the fly (line by line) |
| **Output** | Standalone binary/executable (`.exe`, `.out`) | No persistent output — runs immediately |
| **Speed of execution** | Fast — translation is a separate step | Slower — translates at runtime, every run |
| **Error detection** | All errors caught at compile time, no execution | Errors surface mid-run, partial execution before the bug |
| **Distribution** | Ship the binary, user doesn't need the source or compiler | User needs the interpreter and the source |
| **Optimization** | Can deeply optimize across the whole program | Limited to what it sees moment-to-moment |
| **Examples** | C, C++, Rust, Go, Swift | Python, Ruby, JavaScript (classic), Bash |
| **Hybrid model** | **JIT (Just-in-Time):** Mix of both — compiles hot paths at runtime (Java JVM, V8, LuaJIT) | |

---

## 2. Walkthrough — Same Code, Both Worlds

Take this tiny program:

```c
// demo.c — compiled language
#include <stdio.h>

int main() {
    int a = 5;
    int b = 10;
    int c = a + b;      // line 7 — bug: forgot semicolon?
    printf("%d\n", c);
    return 0;
}
```

```python
# demo.py — interpreted language
a = 5
b = 10
c = a + b              # no semicolons, fine
print(c)
```

### 🔷 Compiler path (C → machine code)

```
 ┌──────────────────────────────────────────────────────────┐
 │ 1. Source code  →  Preprocessor  →  Compiler(s)          │
 │    (demo.c)         (#include, #define)    (demo.s)       │
 │                                                           │
 │ 2. Assembly  →  Assembler  →  Object file                 │
 │    (demo.s)                     (demo.o)                  │
 │                                                           │
 │ 3. Object + libs  →  Linker  →  Executable               │
 │    (stdio, crt0)                    (a.out / demo.exe)    │
 └──────────────────────────────────────────────────────────┘
```

**What happens at each stage with our example:**

| Stage | Input | Work done | Output |
|---|---|---|---|
| **Preprocessing** | `demo.c` | `#include <stdio.h>` pulls in ~30K lines of header code | Expanded `demo.i` (huge) |
| **Compilation** | `demo.i` | Parses `int a = 5; ...` → builds AST → optimizes (`c = a+b` becomes a constant) → emits x86-64 assembly | `demo.s` (assembly text) |
| **Assembly** | `demo.s` | Mnemonic → binary opcodes (mov, add, push, call) | `demo.o` (relocatable object) |
| **Linking** | `demo.o` + `libc` | Resolves `printf` address, fixes relative jumps, produces PE/ELF header | `demo.exe` / `a.out` |

**Distribution:** Ship only `demo.exe`. Zero dependencies. Works forever on that OS.

### 🔶 Interpreter path (Python → execution)

```
 ┌────────────────────────────────────────────────────────────┐
 │ Source  →  Lexer  →  Parser  →  Bytecode  →  VM executes  │
 │ (demo.py)   (tokens)    (AST)       (.pyc)    (line by     │
 │                                                       line)│
 └────────────────────────────────────────────────────────────┘
```

**What happens at each stage with our example:**

| Stage | Input | Work done | Output |
|---|---|---|---|
| **Lexing** | `demo.py` | `a`, `=`, `5`, `b`, `=` ... → token stream | `[NAME:a, OP:=, INT:5, ...]` |
| **Parsing** | Tokens | Grammar rules → Abstract Syntax Tree | AST (`Assign(a, 5)`, ...) |
| **Compilation** | AST | AST → **bytecode** (platform-independent IR) | Bytecode (`LOAD_CONST`, `STORE_NAME`) |
| **Execution (VM)** | Bytecode | Bytecode loop: fetch → decode → execute (native calls under the hood) | Print `15` to stdout |

**Key difference:** Bytecode is *not* an executable. Python's VM runs it fresh every time you type `python demo.py`.

---

## 3. Pipeline Diagram

```
COMPILER (C):
  .c ──[preprocess]──> .i ──[compile]──> .s ──[assemble]──> .o ──[link]──> a.out
  Step 1               Step 2            Step 3              Step 4        Step 5
  ╔═══════════════════════════════════════════════════════════════════════════╗
  ║                        COMPILE TIME (runs once)                          ║
  ╚═══════════════════════════════════════════════════════════════════════════╝
                                                                            ╔═══╗
                                                                            ║ RUN ║
                                                                            ╚═══╝

INTERPRETER (Python):
  .py ──[lex]──> tokens ──[parse]──> AST ──[compile]──> bytecode ──[VM]──> output
  ╔═══════════════════════════════════════════════════════════════════════════╗
  ║                        RUNTIME (every execution)                         ║
  ╚═══════════════════════════════════════════════════════════════════════════╝

HYBRID (JVM / V8):
  .java ──[javac]──> .class ──[JIT]──> native code ──> runs
  ╔══════════╗    ╔═══════════════════════════════════════════════╗
  ║  Compile  ║    ║         Runtime (profiles + recompiles)       ║
  ╚══════════╝    ╚═══════════════════════════════════════════════╝
```

---

## 4. TL;DR

| | Compiler | Interpreter |
|---|---|---|
| **Does the work** | Before you run (once) | While you run (every time) |
| **You ship** | A binary | Your source code |
| **Catches bugs** | All at once, up front | One at a time, as you hit them |
| **Speed** | Fast execution, slow build | Fast to start, slow execution |
| **Example** | `gcc demo.c -o demo && ./demo` | `python demo.py` |
