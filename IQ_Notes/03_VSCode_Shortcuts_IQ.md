# VS Code Shortcuts — IQ Breakdown

## 1. The Big Picture

**Keyboard shortcuts** are key combinations that trigger editor actions without reaching for the mouse. VS Code maps the same action to different keys depending on your OS.

| Shortcut category | What it does | Why it matters |
|---|---|---|
| **Editor navigation** | Move cursor, jump lines, scroll | Stay in the flow — no mouse |
| **Selection & editing** | Select, cut, copy, paste, multi-cursor | Transform code faster |
| **Find & replace** | Search file, search project, regex | Navigate codebases of any size |
| **Code intelligence** | Go to definition, peek, rename | Understand and refactor |
| **Terminal / Tabs** | Open terminal, switch tabs, split | Keep everything in one window |
| **File management** | Open file, save, close, explorer | Organize without mousing |

---

## 2. Walkthrough — Editing `01_HelloWorld.js` With and Without Shortcuts

```javascript
// 01_chapter_Javascript/01_HelloWorld.js
console.log("Hello The Testing Academy!");
```

### Without shortcuts (all mouse)

| Task | Mouse path | Time |
|---|---|---|
| Open the file | Click File → Open → navigate → click | ~4 seconds |
| Select `"Hello The Testing Academy!"` | Double-click, drag selection | ~1 second |
| Copy the string | Right-click → Copy | ~1 second |
| Duplicate the line | Click line number, Copy, click below, Paste | ~3 seconds |
| Open terminal | Terminal → New Terminal | ~2 seconds |
| **Total** | **~11 seconds** | |

### With shortcuts (keyboard only)

| Task | Shortcut (Win/Lin) | Shortcut (macOS) | Time |
|---|---|---|---|
| Quick open file | `Ctrl+P` → type `Hello` → Enter | `Cmd+P` → type `Hello` → Enter | ~1 second |
| Select inside quotes | `Ctrl+Shift+→` (word select) | `Cmd+Shift+→` | ~0.3 seconds |
| Copy selection | `Ctrl+C` | `Cmd+C` | ~0.2 seconds |
| Duplicate line | `Alt+Shift+↓` | `Option+Shift+↓` | ~0.2 seconds |
| Open integrated terminal | `` Ctrl+` `` | `` Ctrl+` `` | ~0.5 seconds |
| **Total** | **~2.2 seconds** | | |

> Shortcuts are **~5x faster** once muscle memory kicks in.

---

## 3. Shortcut Reference Table

### 3a. Editor & Navigation

| Action | Windows / Linux | macOS |
|---|---|---|
| Quick open file | `Ctrl+P` | `Cmd+P` |
| Command palette | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| Open recently opened | `Ctrl+R` | `Cmd+R` |
| Go to line | `Ctrl+G` | `Ctrl+G` |
| Go to symbol | `Ctrl+Shift+O` | `Cmd+Shift+O` |
| Toggle sidebar | `Ctrl+B` | `Cmd+B` |
| Toggle terminal | `` Ctrl+` `` | `` Ctrl+` `` |
| Close tab | `Ctrl+W` | `Cmd+W` |
| Reopen closed tab | `Ctrl+Shift+T` | `Cmd+Shift+T` |
| Switch tabs (left/right) | `Ctrl+Tab` / `Ctrl+Shift+Tab` | `Cmd+Shift+]` / `Cmd+Shift+[` |
| Open settings | `Ctrl+,` | `Cmd+,` |

### 3b. Selection & Editing

| Action | Windows / Linux | macOS |
|---|---|---|
| Cut line | `Ctrl+X` (empty selection) | `Cmd+X` (empty selection) |
| Copy line | `Ctrl+C` (empty selection) | `Cmd+C` (empty selection) |
| Move line up/down | `Alt+↑` / `Alt+↓` | `Option+↑` / `Option+↓` |
| Duplicate line | `Alt+Shift+↓` | `Option+Shift+↓` |
| Insert cursor above | `Ctrl+Alt+↑` | `Cmd+Option+↑` |
| Insert cursor below | `Ctrl+Alt+↓` | `Cmd+Option+↓` |
| Select current line | `Ctrl+L` | `Cmd+L` |
| Indent / outdent | `Tab` / `Shift+Tab` | `Tab` / `Shift+Tab` |
| Comment line | `Ctrl+/` | `Cmd+/` |
| Block comment | `Shift+Alt+A` | `Shift+Option+A` |
| Format document | `Shift+Alt+F` | `Shift+Option+F` |
| Undo / redo | `Ctrl+Z` / `Ctrl+Shift+Z` | `Cmd+Z` / `Cmd+Shift+Z` |

### 3c. Multi-Cursor Magic

| Action | Windows / Linux | macOS |
|---|---|---|
| Add cursor at click | `Alt+Click` | `Option+Click` |
| Select all occurrences | `Ctrl+Shift+L` | `Cmd+Shift+L` |
| Select next occurrence | `Ctrl+D` | `Cmd+D` |
| Undo last cursor | `Ctrl+U` | `Cmd+U` |
| Box select (column mode) | `Shift+Alt+drag` | `Shift+Option+drag` |

### 3d. Find & Replace

| Action | Windows / Linux | macOS |
|---|---|---|
| Find in file | `Ctrl+F` | `Cmd+F` |
| Find in project | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| Replace in file | `Ctrl+H` | `Cmd+Option+F` |
| Find next / previous | `F3` / `Shift+F3` | `Cmd+G` / `Cmd+Shift+G` |
| Toggle regex in find | `Alt+R` | `Cmd+Option+R` |
| Toggle case-sensitive | `Alt+C` | `Cmd+Option+C` |
| Toggle whole word | `Alt+W` | `Cmd+Option+W` |

### 3e. Code Intelligence (Language Server)

| Action | Windows / Linux | macOS |
|---|---|---|
| Go to definition | `F12` | `F12` |
| Peek definition | `Alt+F12` | `Option+F12` |
| Go to references | `Shift+F12` | `Shift+F12` |
| Rename symbol | `F2` | `F2` |
| Quick fix / lightbulb | `Ctrl+.` | `Cmd+.` |
| Trigger suggestion | `Ctrl+Space` | `Ctrl+Space` |
| Parameter hints | `Ctrl+Shift+Space` | `Cmd+Shift+Space` |
| Toggle breadcrumbs | `Ctrl+Shift+.` | `Cmd+Shift+.` |

### 3f. Debugging

| Action | Windows / Linux | macOS |
|---|---|---|
| Start / continue | `F5` | `F5` |
| Step over | `F10` | `F10` |
| Step into | `F11` | `F11` |
| Step out | `Shift+F11` | `Shift+F11` |
| Toggle breakpoint | `F9` | `F9` |
| Stop debugger | `Shift+F5` | `Shift+F5` |

### 3g. Split Editor & Layout

| Action | Windows / Linux | macOS |
|---|---|---|
| Split editor | `Ctrl+\` | `Cmd+\` |
| Focus editor group (1-4) | `Ctrl+1` / `Ctrl+2` / `Ctrl+3` | `Cmd+1` / `Cmd+2` / `Cmd+3` |
| Move editor to next group | `Ctrl+Alt+→` | `Ctrl+Option+→` |
| Close editor group | `Ctrl+W` | `Cmd+W` |
| Toggle Zen mode | `Ctrl+K Z` | `Cmd+K Z` |

---

## 4. Pipeline — From Keypress to Editor Action

```
Physically:
┌──────────┐    ┌──────────────┐    ┌──────────────┐
│  Finger   │───>│   Keyboard   │───>│     OS       │
│  presses  │    │  sends HID   │    │  translates  │
│  Ctrl+P   │    │   scancode   │    │  to keycode  │
└──────────┘    └──────────────┘    └──────┬───────┘
                                           ↓
VS Code:
┌──────────────────────────────────────────────────────────────────┐
│  Keybinding Service                                               │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │  Looks up keycode in active keybindings.json                 │ │
│  │  Matches: "ctrl+p" → "workbench.action.quickOpen"           │ │
│  │  Checks:  (when clause matches?) e.g. !editorHasSelection   │ │
│  └──────────────────────────────────────────────────────────────┘ │
│                              ↓                                    │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │  Dispatches command                                           │ │
│  │  workbench.action.quickOpen  →  shows Quick Pick input box   │ │
│  └──────────────────────────────────────────────────────────────┘ │
│                              ↓                                    │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │  User types file name (fuzzy matched)                        │ │
│  │  "hello" → matches 01_HelloWorld.js                         │ │
│  │  Enter → opens file in active editor group                   │ │
│  └──────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

---

## 5. Customizing Shortcuts

Your shortcuts live in `keybindings.json`. Open it with:

| Action | Windows / Linux | macOS |
|---|---|---|
| Open keyboard shortcuts UI | `Ctrl+K Ctrl+S` | `Cmd+K Cmd+S` |
| Open `keybindings.json` directly | `Ctrl+Shift+P` → "Open Keyboard Shortcuts (JSON)" | same |

### Example — Re-map duplicate line to `Ctrl+D` (instead of default find-next)

```json
// keybindings.json
[
    {
        "key": "ctrl+d",
        "command": "editor.action.copyLinesDownAction",
        "when": "editorTextFocus && !editorReadonly"
    }
]
```

This overrides the default `Ctrl+D` (Add Selection To Next Find Match) with `Copy Line Down`.

---

## 6. TL;DR

| What | Best shortcut to learn first | Win/Lin | macOS |
|---|---|---|---|
| **Open any file** | Quick Open | `Ctrl+P` | `Cmd+P` |
| **Run any command** | Command Palette | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| **Edit multiple spots** | Multi-cursor | `Alt+Click` | `Option+Click` |
| **Find across files** | Search in project | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| **Jump to definition** | Go to definition | `F12` | `F12` |
| **Format code** | Format document | `Shift+Alt+F` | `Shift+Option+F` |
| **Sidebar toggle** | Hide/show sidebar | `Ctrl+B` | `Cmd+B` |
| **Terminal** | Integrated terminal | `` Ctrl+` `` | `` Ctrl+` `` |

> Rule of thumb: If you find yourself reaching for the mouse, there's probably a shortcut for it.
