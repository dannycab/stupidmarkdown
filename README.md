# stupidmarkdown

stupidmarkdown is a minimal, cross-platform Markdown editor built with Svelte and Tauri. It features:

- Live Markdown preview
- System file access (open/save)
- Syntax highlighting
- Export to PDF, TeX, and Typst
- Minimal UI, keybinding-driven workflow
- No plugins or extensions

## Getting Started

1. Install dependencies:
   ```sh
   npm install --legacy-peer-deps
   ```
2. Start the app in development mode:
   ```sh
   npm run tauri dev
   ```

## Build

To build the app for distribution:
```sh
npm run tauri build
```

## Platforms
- macOS
- Linux

## Project Structure
- Frontend: Svelte (Vite)
- Backend: Tauri (Rust)

---

This project is in early development (version 0.0.1).
