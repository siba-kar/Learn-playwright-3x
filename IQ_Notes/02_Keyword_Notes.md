# Keywords in JS — IQ Breakdown

## 1. The Big Picture

A **keyword** is a reserved word the language keeps for itself. You cannot use it as a variable name, function name, or identifier. Think of them as the language's built-in commands.

| Category | Keywords | Can you use as a variable? |
|---|---|---|
| **Declaration** | `var`, `let`, `const` | ❌ `let let = 5` → SyntaxError |
| **Control flow** | `if`, `else`, `for`, `while`, `do`, `switch`, `case`, `break`, `continue`, `return` | ❌ `var return = 10` → SyntaxError |
| **Function / Class** | `function`, `class`, `extends`, `new`, `this`, `super`, `yield`, `await`, `async` | ❌ `let class = "math"` → SyntaxError |
| **Variable / Value** | `true`, `false`, `null`, `undefined`, `NaN`, `Infinity` | ❌ `let null = 0` → SyntaxError |
| **Error handling** | `try`, `catch`, `finally`, `throw` | ❌ `var catch = "me"` → SyntaxError |
| **Module** | `import`, `export`, `from`, `default` | ❌ `let import = 1` → SyntaxError |
| **Type operators** | `typeof`, `instanceof`, `void`, `delete`, `in` | ❌ `var typeof = "check"` → SyntaxError |
| **Object / Iteration** | `of`, `in`, `with`, `get`, `set` | ❌ `let of = "preposition"` → SyntaxError |
| **Legacy / Strict** | `debugger`, `arguments`, `eval`, `implements`, `interface`, `package`, `private`, `protected`, `public`, `static` | ❌ Reserved in strict mode |

---

## 2. Walkthrough — Keywords in Action Across the Codebase

### 2a. Declaration keywords — `02_let_concept.js`

```javascript
let a = 10;               // let = declare a block-scoped variable
console.log(a);           

for (let a = 0; a < 12; a++) {   // for = loop construct
    console.log(a);               // a = keyword? No — it's an identifier
    functioncall();               // functioncall = user-defined identifier
}

function functioncall() {         // function = declaration keyword
    console.log("Hello");         // console = identifier (not keyword)
}
```

| Token | Type | Why |
|---|---|---|
| `let` | **Keyword** | JS engine recognizes it as a declaration keyword |
| `a` | **Identifier** | User-chosen variable name |
| `for` | **Keyword** | Loop construct — grammar rule: `for (init; test; update)` |
| `function` | **Keyword** | Declaration keyword — grammar rule: `function name(params) body` |
| `console` | **Identifier** | Global object — not reserved |
| `log` | **Identifier** | Property access on `console` |

### 2b. Value keywords — `07_Literal.js`

```javascript
let isStudent = true;     // true = boolean keyword
let pi = 3.14;            // pi = identifier (user-chosen)
let nullValue = null;     // null = keyword (absence of value)
let undefinedValue;       // undefined = implicit, also a keyword

console.log(typeof age);  // typeof = operator keyword
```

| Token | Type | Role |
|---|---|---|
| `true` | **Keyword** | Boolean literal keyword — evaluates to `1` / `true` |
| `false` | **Keyword** | Boolean literal keyword |
| `null` | **Keyword** | Null literal — intentional absence |
| `undefined` | **Keyword** | Default value of uninitialized variables |
| `typeof` | **Keyword** | Unary operator — returns type as a string |

### 2c. What happens if you break the rules — `06_Identifer_IQ.js`

```javascript
// ❌ These will NOT run — uncomment and the parser stops you:
// let class = "invalid";     // SyntaxError: Unexpected keyword
// let const = "invalid";     // SyntaxError: let is disallowed as a lexically bound name
// let function = "invalid";  // SyntaxError: Unexpected token

// ✅ This IS valid — JavaScript is case-sensitive:
let Function = "invalid";    // "Function" ≠ "function" — capital F saves it
```

---

## 3. Layer-by-Layer — How the Engine Handles Keywords

```
Source Code:  let isStudent = true;
```

| Layer | What happens | Example |
|---|---|---|
| **1. Lexing** | Scanner reads char by char, matches against keyword table | `l-e-t` → matches `let` keyword token. `t-r-u-e` → matches `true` keyword token. `i-s-S-t-u-d-e-n-t` → no keyword match → emitted as **identifier** token |
| **2. Parsing** | Parser reads token stream against JS grammar rules: `Declaration : let Identifier = Expression ;` | `[let] [isStudent] [=] [true] [;]` → matches `VariableDeclaration` node |
| **3. Keyword collision check** | If you try `let let = 5`, parser sees `[let] [let]` — expects an identifier after `let`, finds another keyword → **SyntaxError** immediately | `let const = 10` → `SyntaxError: Unexpected token 'const'` |
| **4. Execution** | Interpreter/VM runs the AST — `true` evaluates to the boolean value | `isStudent` gets assigned `true` in memory |

### Where keywords are stored in the engine

```
                  ┌──────────────────────┐
                  │   Source code chars   │
                  └──────┬───────────────┘
                         ↓
                  ┌──────────────────────┐
                  │    KEYWORD TABLE      │  ← built into the lexer
                  │  ┌──────────────────┐ │
                  │  │ break            │ │
                  │  │ case             │ │
                  │  │ catch            │ │
                  │  │ const            │ │
                  │  │ continue         │ │
                  │  │ debugger         │ │
                  │  │ default          │ │
                  │  │ delete           │ │
                  │  │ do               │ │
                  │  │ else             │ │
                  │  │ ... (~60 total)  │ │
                  │  └──────────────────┘ │
                  └──────────────────────┘
                         ↓
                  ┌──────────────────────┐
                  │   PARSER GRAMMAR      │
                  │  IfStatement:         │
                  │    'if' '(' expr ')'  │
                  │    statement          │
                  │    ('else' statement)?│
                  └──────────────────────┘
                         ↓
                  ┌──────────────────────┐
                  │     AST (executed)    │
                  └──────────────────────┘
```

---

## 4. Pipeline — Keyword Through the JS Engine

```
Source: if (a > 0) { return a; }

                  ↓
[LEXER]           ↓
           ┌──────────────┐
           │ 'if'  → IF   │── keyword token
           │ '('   → LPAR │
           │ 'a'   → ID   │── identifier
           │ '>'   → GT   │
           │ '0'   → NUM  │── number literal
           │ ')'   → RPAR │
           │ '{'   → LBRACE│
           │ 'return'→ RET │── keyword token
           │ 'a'   → ID   │
           │ ';'   → SEMI │
           │ '}'   → RBRACE│
           └──────────────┘
                  ↓
[PARSER]          ↓
           ┌────────────────────────────────┐
           │ IfStatement                    │
           │  ├─ test: BinaryExpression     │
           │  │      ├─ left: Identifier(a) │
           │  │      ├─ op: >               │
           │  │      └─ right: Literal(0)   │
           │  └─ consequent: BlockStatement │
           │       └─ body: ReturnStatement │
           │            └─ arg: Identifier(a)│
           └────────────────────────────────┘
                  ↓
[EXECUTION]       ↓
           Checks condition, true → jumps to return
```

---

## 5. Full Keyword List (ES2025+)

```
await         break         case          catch         class
const         continue      debugger      default       delete
do            else          export        extends       false
finally       for           function      if            import
in            instanceof    let           new           null
of            return        super         switch        this
throw         true          try           typeof        undefined
var           void          while         with          yield
```

**Reserved for future / strict mode:**
```
implements    interface     package       private       protected
public        static
```

---

## 6. TL;DR

| Question | Answer |
|---|---|
| **What's a keyword?** | A word the language reserves for its own syntax |
| **Can I use a keyword as a variable name?** | ❌ No — `let class = 5` throws `SyntaxError` |
| **Are keywords case-sensitive?** | ✅ Yes — `Function` ≠ `function`. `Function` is a valid identifier |
| **Where are keywords checked?** | In the **lexer** — it has a built-in lookup table. If the chars match a keyword, it emits a keyword token, not an identifier token |
| **How many keywords in JS?** | ~60+ depending on the spec version and strict mode |
| **What's the difference between a keyword and a literal?** | Keywords are syntax (`if`, `for`, `return`). `true`, `false`, `null` are keywords that also act as literal values |
