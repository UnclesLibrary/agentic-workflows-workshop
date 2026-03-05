# Jekyll Local Preview

This devcontainer provides a complete Ruby/Jekyll environment for previewing the GitHub Pages site locally.

## 🚀 Quick Start

1. **Open in DevContainer**
   - VS Code will prompt you to "Reopen in Container" (or use Command Palette: "Dev Containers: Reopen in Container")
   - Wait for the container to build and dependencies to install

2. **Start Jekyll Server**
   - Press **F5** (or click Run → Start Debugging)
   - Your browser will automatically open to http://localhost:4000

3. **Make Changes**
   - Edit any markdown files in `docs/`
   - Jekyll will auto-reload with live preview (except `_config.yml` requires restart)

## 🛑 Stop Server

Press `Ctrl+C` in the terminal

## 📦 What's Included

- Ruby 3.2
- Jekyll and GitHub Pages gems
- Git & GitHub CLI
- Markdown VS Code extensions
- Port forwarding for local preview

## 💡 Tips

- Changes to markdown files auto-reload
- Changes to `_config.yml` require server restart
- The container has its own isolated Ruby environment
- All Ruby gems are installed inside the container only
