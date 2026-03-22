# QR'S BROWSER COMPILER
 
A multi-language code runner that runs entirely in the browser — no server, no backend, no setup.
 
---
 
## What is it?
 
A lightweight in-browser IDE that lets you write and run code in multiple languages directly in your browser tab. It uses real language runtimes and transpilers loaded via CDN — not simulated execution.
 
---
 
## Supported Languages
 
| Language | Runtime | Hello World |
|----------|---------|-------------|
| JavaScript | Native browser V8 engine | `console.log("Hello!")` |
| TypeScript | TypeScript compiler (transpile to JS) | `const msg: string = "Hello!"; console.log(msg);` |
| Lua | Fengari (Lua 5.3 in WASM) | `print("Hello!")` |
| Ruby | Opal (Ruby to JS compiler) | `puts "Hello!"` |
| Markdown | marked.js | `# Hello Markdown` |
 
---
 
## How it works
 
```
User writes code
      │
      ▼
Language selected
      │
      ├── JavaScript → eval() with console.log capture
      │
      ├── TypeScript → ts.transpileModule() → eval()
      │
      ├── Lua        → fengari.load() with print capture
      │
      ├── Ruby       → Opal.eval()
      │
      └── Markdown   → marked.parse() → rendered HTML
```
 
### Console capture
 
For JS/TS/Lua/Ruby the app intercepts `console.log` to capture output:
 
```javascript
let originalConsole = console.log;
console.log = (...args) => logs.push(args.join(''));
// run code
console.log = originalConsole; // restore
```
 
This means `console.log`, `print` and `puts` all appear in the output box instead of the browser console.
 
---
 
## Features
 
- **No setup required** — open in browser and start coding
- **Download your code** — saves with the correct file extension per language
- **Boilerplate per language** — switches to a hello world example when you change language
- **Separate output rendering** — code languages show plain text output, Markdown renders as HTML
- **Real runtimes** — not simulated, actual language engines running in the browser
 
---
 
## Tech Stack
 
- **Language:** JavaScript
- **Framework:** Alpine.js
- **Styling:** Tailwind CSS
- **Runtimes:**
  - [Fengari](https://fengari.io/) — Lua in WebAssembly
  - [Opal](https://opalrb.com/) — Ruby to JavaScript compiler
  - [TypeScript](https://www.typescriptlang.org/) — TypeScript compiler
  - [marked](https://marked.js.org/) — Markdown parser
 
---
 
## Project Structure
 
```
index.html      Everything — UI, logic, runtime loading
```
 
Single file application. No build step. No npm. Open in any browser.
 
---
 
## Usage
 
1. Open `index.html` in your browser
2. Select a language from the dropdown
3. Write your code
4. Click **Run**
5. See output below
6. Optionally name and download your file
 
---
 
## File Extensions on Download
 
| Language | Extension |
|----------|-----------|
| JavaScript | .js |
| TypeScript | .ts |
| Lua | .lua |
| Ruby | .rb |
| Markdown | .md |
 
---
 
## Project Status
 
| Feature | Status |
|---------|--------|
| JavaScript execution | ✅ Working |
| TypeScript transpilation | ✅ Working |
| Lua execution | ✅ Working |
| Ruby execution | ✅ Working |
| Markdown rendering | ✅ Working |
| Console capture | ✅ Working |
| File download | ✅ Working |
| Error handling | 🔄 In progress |
| Syntax highlighting | 📋 Planned |
| More languages | 📋 Planned |
 
---
 
## Planned Languages
 
- Python (Pyodide)
- C / C++ (Emscripten)
- PHP (php-wasm)
- Brainfuck
- Lisp
 
---
 
## What I Learned
 
- How to intercept and capture `console.log` output
- How TypeScript transpilation works in the browser
- How WebAssembly enables running non-JS languages in the browser
- How Lua and Ruby runtimes can be embedded via CDN
- Building a single-file application with multiple runtime dependencies
 
---
 
## Related Projects
 
- [Athena](../Athena) — AI assistant also built with Alpine.js and Tailwind
- [IDE](../IDE) — Desktop version of a multi-language code runner built in C#
 
---
 
## Author
 
**Quidon Roethof** — Software Developer, Netherlands
 
*Built to understand how code actually runs — and to prove that a browser can execute far more than just JavaScript.*
