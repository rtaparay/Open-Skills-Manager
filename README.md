# 🌐 Open Skills Manager
> **The Open Agent Skills Ecosystem**

Explore, install, and manage procedural skill repositories across multiple IDEs. Search a massive cloud catalog of **~58,000+ skills** (powered by [claude-plugins.dev](https://claude-plugins.dev/)) and equip your AI agents with real procedural knowledge with a single command.

![Open Skills Manager Preview](https://raw.githubusercontent.com/rtaparay/Open-Skills-Manager/refs/heads/main/resources/image.png)

---

## ✨ Features

* 📦 **Repository Management**: Add, remove, and switch branches of skill repositories effortlessly.
* ⚡ **One-Click Installation**: Install skills directly into the active IDE's skills directory.
* ☁️ **Cloud Skills Search (~58K)**: Search the cloud catalog and install with one click or simply press Enter.
* 🔄 **Multi-IDE Support**: Works natively with VS Code, Cursor, Trae, Antigravity, Qoder, Windsurf, and CodeBuddy.
* 📂 **Active Skills Directory**: The local skills group clearly displays which workspace directory is currently active.

---

## 🚀 Usage

1. Open the **Agent Skills** panel in the Activity Bar. ![icon](https://raw.githubusercontent.com/rtaparay/AgentSkillsManager/refs/heads/main/resources/skills-icon.png)
2. Click **+** to add a skill repository (e.g., `https://github.com/anthropics/skills`).
3. Expand the repository to browse available skills.
4. Check the skills you want, then click **Install**.
5. Click the search icon to search cloud skills, then press **Enter** (or click **Install**) to download and deploy.

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

## ⚙️ Configuration

Skills are automatically installed to the active skills directory in your workspace based on your current IDE:

* **VS Code**: `.github/skills`
* **Cursor**: `.cursor/skills`
* **Trae**: `.trae/skills`
* **Antigravity**: `.agent/skills`
* **Qoder**: `.qoder/skills`
* **Windsurf**: `.windsurf/skills`
* **CodeBuddy**: `.codebuddy/skills`

> **Note:** The extension also scans for skills in hidden directories inside repositories (e.g., `.curated`, `.experimental`).

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

# 4. Install the generated .vsix file (Example using Antigravity)
antigravity --install-extension Open-Skills-Manager-0.1.0.vsix