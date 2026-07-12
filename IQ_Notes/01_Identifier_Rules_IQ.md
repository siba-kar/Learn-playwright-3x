# Identifier Rules — IQ Breakdown

## 1. The Big Picture

An **identifier** is a name you give to a variable, function, class, or object. Every language has rules for what makes a valid name.

| Rule | Valid | Invalid |
|---|---|---|
| **First character** | Letter (`a-z`, `A-Z`), underscore (`_`), or dollar sign (`$`) | Digit (`0-9`), space, or any symbol |
| **Remaining characters** | Letters, digits, `_`, `$` | Spaces, hyphens, `@`, `#`, `%`, etc. |
| **Case sensitivity** | `name` and `Name` are **different** variables | — |
| **Reserved words** | `myVar`, `totalCount` | `var`, `let`, `if`, `return`, `class` |
| **Length** | No practical limit (but be sane) | — |
| **Unicode support** | Most modern langs allow `ñ`, `é`, `中文`, `α` | Depends on language spec |
| **Keyword collision** | Avoid language keywords as names | `var var = 5` → SyntaxError |

---

## 2. Walkthrough — `03_Identifer_Rules.js`

```javascript
var a = 10;           // ✅ Single letter — shortest valid identifier
console.log(a);

var $ = 10;           // ✅ Dollar sign is valid as first char (unusual but legal)
var _a = 23;          // ✅ Underscore first — common for "private" convention
var pp = 34;          // ✅ Two lowercase letters

var ab123 = 23;       // ✅ Letters + digits after the first char
// var 45 = 34;       // ❌ STARTS WITH DIGIT — SyntaxError
var _ = 10;           // ✅ Underscore alone — valid (lodash uses this)

var Name = "sibaa";   // ✅ Capital N
var name = "sa";      // ✅ Lowercase n — different variable than `Name` (case-sensitive)

// var siba k = "hello"; // ❌ CONTAINS SPACE — SyntaxError
var siba_k = "hello";    // ✅ Underscore replaces space (snake_case)
var Siba$K = "hello";    // ✅ Dollar sign in the middle is fine
var $siba = "hello";     // ✅ Dollar sign first — common in jQuery / generated code
// var 1siba = "1";     // ❌ STARTS WITH DIGIT — SyntaxError
var _1siba = "1";        // ✅ Underscore first, digit after — perfectly valid
```

### Layer-by-layer breakdown

| Layer | What happens | Example hit |
|---|---|---|
| **Lexing (tokenization)** | Scanner reads characters, groups them into tokens | `var` → keyword token, `a` → identifier token, `=` → operator token |
| **Lexer rejects** | If a token starts with a digit where a name is expected, lexer emits an error immediately | `45` → lexer sees `45` as a *number literal*, not an identifier → `SyntaxError` |
| **Parsing** | Parser checks the token stream against JS grammar: `var` + `identifier` + `=` + `expression` | `var siba k` → parser sees `identifier` then hits `k` with no operator → `SyntaxError` |
| **Scope binding** | Parser registers each identifier in its scope (global, function, block) | `a`, `$`, `_a`, `Name`, `name` → all registered in global scope |
| **Runtime access** | When `console.log(a)` executes, the engine looks up `a` in the scope chain | Finds `a = 10`, prints `10` |

---

## 3. Identifier Anatomy

```
 ┌──────────┐     ┌─────────────────────┐
 │  1st char │     │  Rest of identifier  │
 │           │     │                      │
 │  a-z      │     │  a-z                 │
 │  A-Z      │     │  A-Z                 │
 │  _        │     │  0-9                 │
 │  $        │     │  _                   │
 │           │     │  $                   │
 └──────────┘     └─────────────────────┘

        ↓
    ┌───────────────────┐
    │  $siba_k_123Name  │  ✅ valid
    │  ^                │
    │  └─ starts with $ │
    └───────────────────┘

        ↓
    ┌───────────────────┐
    │  1siba            │  ❌ invalid
    │  ^                │
    │  └─ starts with 1 │
    └───────────────────┘
```

---

## 4. Pipeline — How an Identifier Travels Through JS Engine

```
Source: var siba_k = "hello";
                 ↓
      ┌─────────────────────┐
      │  LEXER              │
      │  [var] [siba_k] [=] │──> token stream
      │  ["]hello["] [;]    │
      └─────────────────────┘
                 ↓
      ┌─────────────────────┐
      │  PARSER             │
      │  VariableDeclaration│──> AST node
      │  ├─ kind: var       │
      │  ├─ id: siba_k      │  (identifier name → string)
      │  └─ init: "hello"   │
      └─────────────────────┘
                 ↓
      ┌─────────────────────┐
      │  SCOPE ANALYSIS     │
      │  siba_k → global    │──> scope chain updated
      └─────────────────────┘
                 ↓
      ┌─────────────────────┐
      │  EXECUTION          │
      │  siba_k = "hello"   │──> memory slot assigned
      │  console.log(siba_k)│──> lookup → "hello"
      └─────────────────────┘
```

---

## 5. Naming Conventions (not rules, but *should*s)

| Style | Pattern | Example | When |
|---|---|---|---|
| **camelCase** | `firstSecondThird` | `userName`, `getData()` | JS/TS variables & functions |
| **PascalCase** | `FirstSecondThird` | `UserProfile`, `App` | Classes / constructors / React components |
| **snake_case** | `first_second_third` | `user_name`, `MAX_SIZE` | Python vars, constants |
| **kebab-case** | `first-second-third` | `app-config` | CSS classes, file names, CLI flags |
| **UPPER_SNAKE** | `FIRST_SECOND` | `API_KEY`, `PI` | Constants (by convention) |
| **`_` prefix** | `_private` | `_internalVar` | Convention for "private" (not enforced) |
| **`$` prefix** | `$element` | `$btn`, `$container` | jQuery / DOM references |

---

## 6. TL;DR

| Rule | Meaning | Bad | Good |
|---|---|---|---|
| **Start char** | `a-z`, `A-Z`, `_`, `$` only | `1name` | `name1` |
| **Body chars** | Add digits `0-9` | `my var` | `myVar` |
| **Case-sensitive** | `A` ≠ `a` | `Name` / `name` are two vars | Pick one convention |
| **No reserved words** | Can't shadow language keywords | `var return = 5` | `var result = 5` |
| **No spaces** | Must be one continuous token | `first name` | `firstName` |
