# Calorie & Macro Tracker

An AI-powered nutrition tracker built on Claude. Log meals by typing or sending photos, get instant calorie and macro breakdowns, and save everything to Notion or local files - all through natural conversation.

## Features

- **Natural language logging** - just type what you ate, no forms or apps
- **Photo analysis** - send a photo of your meal and get an estimate
- **Auto macro calculation** - personalized targets based on your weight, height, and goals
- **Two storage options** - Notion database or local markdown files
- **Automatic food database** - builds up as you log, no manual entry
- **Multi-language** - choose your language during onboarding

---

## Two Ways to Use It

| | Claude Code (CLI) | Claude Projects (chat) |
|---|---|---|
| Setup | Clone repo, run `claude .` | Paste prompt into Project Instructions |
| Memory | Auto-saved to files | Upload profile to Project Knowledge |
| Local file storage | Yes | No |
| Notion auto-save | Yes (with MCP) | Yes (via Connections) |
| Photo analysis | Yes | Yes |
| Best for | Developers, power users | Everyone else |

---

## Method 1: Claude Code (CLI)

Full automation - Claude reads and writes files, saves to Notion automatically, and remembers your profile across sessions.

### Prerequisites

- [Claude Code](https://claude.ai/code) installed (`npm install -g @anthropic-ai/claude-code`)
- A Claude account (Pro plan recommended)
- Notion account (optional)

### Setup

```bash
git clone https://github.com/YOUR_USERNAME/diet-tracker.git
cd diet-tracker
claude .
```

Onboarding starts automatically on the first message.

### Notion setup (optional)

Add the Notion MCP server to Claude Code. Edit `~/.claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-notion"],
      "env": {
        "NOTION_API_KEY": "your_integration_token"
      }
    }
  }
}
```

Get your integration token at [notion.so/my-integrations](https://www.notion.so/my-integrations). Share your Notion pages with the integration after creating it.

During onboarding, Claude will find or create the required databases automatically:
- **Food Log** - daily entries with meal breakdowns
- **Weight Tracker** - weight history with BMI
- **Food Database** - your personal food library

### How memory works in Claude Code

Your profile is saved to Claude Code's local memory and loaded silently at the start of every session. You never need to re-enter your parameters.

---

## Method 2: Claude Projects (web or desktop chat)

No installation required. Works directly in the Claude chat interface.

### Setup

**Step 1 - Create a project**

Go to [claude.ai](https://claude.ai) and create a new Project.

**Step 2 - Add the system prompt**

Open **Project Instructions** and paste the entire contents of [`CLAUDE.md`](./CLAUDE.md) from this repository.

**Step 3 - Start your first chat**

Open a new chat inside the project. Onboarding starts automatically.

**Step 4 - Save your profile to Project Knowledge**

After onboarding, Claude will show your profile as a formatted block. Copy it and:

1. Save it as `profile.md` on your computer
2. Go to your Project settings
3. Upload `profile.md` to **Project Knowledge**

Claude will read your profile from Knowledge at the start of every chat - no need to re-enter anything.

> When your weight or targets change, update `profile.md` and re-upload it to Project Knowledge.

### Storage in Claude Projects

**Notion (recommended for Projects)**

Claude Projects supports Notion natively via **Connections** - no MCP or API keys needed.

1. Open your project settings
2. Go to **Connections**
3. Click **Add connection** and select **Notion**
4. Authorize access to your workspace

Once connected, Claude can read and write to your Notion workspace directly. During onboarding, it will search for existing databases and create any that are missing.

**Local files**

Not available in Claude Projects - Claude does not have access to your file system in chat mode.

---

## Onboarding Flow

The same onboarding runs regardless of which method you use.

**Language** - choose English, Russian, or any other language. Claude uses it for all responses.

**Personal parameters** - Claude asks for:
- Current weight, height, target weight, age, sex
- Training frequency
- Daily tea/coffee with sugar (gets added automatically to daily totals)

Claude calculates your calorie limit and macro targets using the Mifflin-St Jeor formula (TDEE - 500 kcal deficit) and shows them for your confirmation. You can adjust any value.

**Storage** - choose Notion or local files (local files only available in Claude Code).

---

## Daily Usage

Just tell Claude what you ate:

> "Oatmeal 80g dry with a banana and 2 eggs"

> "Had a grilled chicken salad at a restaurant"

Or send a photo of your plate.

Claude replies with the breakdown and running daily totals after every entry.

### Commands

Phrase these however feels natural in your language:

| Intent | What happens |
|--------|--------------|
| "total" / "summary" | Full breakdown of everything logged today |
| "new day" / "reset" | Start a fresh day |
| "save" / "log it" | Save today's entry to storage |
| "weighed 85 kg" | Log a weight entry |
| "settings" | View or edit your profile |
| "meal plan" | Get a meal plan based on your food history |

---

## Privacy

Your data stays in your own Notion workspace or local files. Claude Code's memory files and the `.diet/` folder are excluded from git via `.gitignore` and never committed to this repository.
