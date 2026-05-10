
# Calorie & Macro Tracker for Claude Code

An AI-powered nutrition tracker that runs inside [Claude Code](https://claude.ai/code). Log meals by typing or sending photos, get instant calorie and macro breakdowns, and save everything to Notion or local markdown files - all through natural conversation.

## Features

- **Natural language logging** - just type what you ate, no forms or apps
- **Photo analysis** - send a photo of your meal and get an estimate
- **Auto macro calculation** - personalized targets based on your weight, height, and goals
- **Two storage options** - Notion database or local markdown files
- **Automatic food database** - builds up as you log, no manual entry
- **Multi-language** - choose your language during setup

## Prerequisites

- [Claude Code](https://claude.ai/code) installed
- A Claude account (Pro plan recommended for photo analysis)
- Notion account (optional, for Notion storage)

## Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/diet-tracker.git
cd diet-tracker

# 2. Open Claude Code in the project folder
claude .

# 3. Start chatting - onboarding runs automatically
```

That's it. Claude will guide you through the rest.

## Onboarding

On first launch Claude will ask you to set up your profile in three steps:

**Step 1 - Language**
Choose English, Russian, or any other language. Claude will use it for all responses.

**Step 2 - Personal parameters**
- Current weight, height, target weight, age, sex
- Training frequency
- Daily tea/coffee with sugar (auto-added to daily totals)

Claude calculates your calorie limit and macro targets using the Mifflin-St Jeor formula (TDEE - 500 kcal deficit) and shows them for confirmation. You can adjust any value.

**Step 3 - Storage**
Choose where to save your data:

### Option A: Notion
Claude connects to your Notion workspace, searches for existing databases, and creates any that are missing:
- **Food Log** - daily entries with meal breakdowns
- **Weight Tracker** - weight history with BMI
- **Food Database** - your personal food library

To use Notion, add the Notion MCP server to Claude Code first:

```json
// Add to ~/.claude/claude_desktop_config.json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-notion"],
      "env": {
        "NOTION_API_KEY": "your_notion_integration_token"
      }
    }
  }
}
```

Get your integration token at [notion.so/my-integrations](https://www.notion.so/my-integrations). Make sure to share your Notion pages with the integration.

### Option B: Local files
Claude creates a `.diet/` folder in the project root with:
```
.diet/
  logs/         # daily food logs (one file per day)
  weight.md     # weight history
  foods.md      # food database
```

## Daily Usage

Just tell Claude what you ate:

> "Oatmeal 80g dry with a banana and 2 eggs"

> "Had a chicken salad at a restaurant"

Or send a photo of your meal.

Claude responds with the breakdown and running daily totals after every entry.

### Commands

| Say something like | What happens |
|--------------------|--------------|
| "total" / "summary" | Full breakdown of everything logged today |
| "new day" / "reset" | Start a fresh day |
| "save" / "log it" | Save today's entry to storage |
| "weighed 85 kg" | Log a weight entry |
| "settings" | View or edit your profile |
| "meal plan" | Get a meal plan based on your food history |

## How It Works

- Your personal profile (weight, targets, Notion IDs) is stored in Claude Code's memory and loaded automatically each session
- Every new food product is added to your food database automatically
- Branded products are looked up on the web for accurate nutrition data
- Fixed daily items (like your morning coffee) are added automatically based on your profile

## Privacy

Your personal data (weight, targets, food logs) is stored either in your own Notion workspace or in local files - never on any third-party server beyond Claude's standard conversation processing.

The `.diet/` folder and Claude's memory files are excluded from git via `.gitignore`.

## Updating Your Profile

Say "settings" at any time to see your current profile and change any value - weight, calorie target, macros, or storage mode.
