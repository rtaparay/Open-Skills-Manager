# 🌐 Open Skills Manager
> **The Open Agent Skills Ecosystem**

Explore, install, and manage procedural skill repositories across VS Code and its most popular AI-powered forks. Search a massive cloud catalog of **~58,000+ skills** (powered by [claude-plugins.dev](https://claude-plugins.dev/)) and equip your AI agents with real procedural knowledge with a single command.

![Open Skills Manager Preview](https://raw.githubusercontent.com/rtaparay/Open-Skills-Manager/refs/heads/main/resources/image.png)

---

## ✨ Features

* 📦 **Repository Management**: Add, remove, and switch branches of skill repositories effortlessly.
* ⚡ **One-Click Installation**: Install skills directly into the active IDE's skills directory.
* ☁️ **Cloud Skills Search (~58K)**: Search the cloud catalog and install with one click or simply press Enter.
* 🔄 **VS Code Ecosystem Support**: Works natively with VS Code and major AI-first forks like Cursor, Windsurf, Trae, and Antigravity.
* 📂 **Active Skills Directory**: The local skills group clearly displays which workspace directory is currently active.

---

## 🚀 Usage

1. Open the **Agent Skills** panel in the Activity Bar. ![icon](https://raw.githubusercontent.com/rtaparay/AgentSkillsManager/refs/heads/main/resources/skills-icon.png)
2. Click **+** to add a skill repository (e.g., `https://github.com/anthropics/skills`).
3. Expand the repository to browse available skills.
4. Check the skills you want, then click **Install**.
5. Click the search icon to search cloud skills, then press **Enter** (or click **Install**) to download and deploy.

---

## 🤖 Supported Editors (VS Code Based)

Skills can be installed automatically to any of these supported VS Code-based environments. Open Skills Manager detects your active IDE or allows you to specify it:

| Editor | `--editor` | Project Path | Global Path |
|-------|-----------|--------------|-------------|
| **VS Code** | `vscode` | `.github/skills/` | `~/.vscode/skills/` |
| **Antigravity** | `antigravity` | `.agent/skills/` | `~/.gemini/antigravity/skills/` |
| **CodeBuddy** | `codebuddy` | `.codebuddy/skills/` | `~/.codebuddy/skills/` |
| **Cursor** | `cursor` | `.cursor/skills/` | `~/.cursor/skills/` |
| **Qoder** | `qoder` | `.qoder/skills/` | `~/.qoder/skills/` |
| **Trae** | `trae` | `.trae/skills/` | `~/.trae/skills/` |
| **Windsurf** | `windsurf` | `.windsurf/skills/` | `~/.codeium/windsurf/skills/` |

---

## 📚 Skill Collections

Preset repositories bundled by default to get you started immediately:

| Repository | Description |
|------------|-------------|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Anthropic skills collection |
| [openai/skills](https://github.com/openai/skills) | Official OpenAI skills catalog |
| [skillcreatorai/Ai-Agent-Skills](https://github.com/skillcreatorai/Ai-Agent-Skills) | Community skills collection |
| [obra/superpowers](https://github.com/obra/superpowers) | Superpowers skill collection |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | Curated awesome-claude-skills collection |

For more repositories, check out the [awesome-agent-skills](https://github.com/heilcheng/awesome-agent-skills) list.

---

## 🛠️ Installation & Build

To build and install the extension locally, run the following commands in your terminal:

```bash
# 1. Ensure you have the correct Node version
nvm install

# 2. Install dependencies
npm install

# 3. Package the extension
npx vsce package

# 4. Install the generated .vsix file

You can install the resulting file in VS Code by running:

# VSCode
code --install-extension Open-Skills-Manager-0.1.0.vsix

# Antigravity
antigravity --install-extension  Open-Skills-Manager-0.1.0.vsix

# Cursor
cursor --install-extension  Open-Skills-Manager-0.1.0.vsix

# Kiro
kiro --install-extension  Open-Skills-Manager-0.1.0.vsix

# Trae
trae --install-extension  Open-Skills-Manager-0.1.0.vsix

# Windsurf
windsurf --install-extension  Open-Skills-Manager-0.1.0.vsix

```