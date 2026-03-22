# 🚨 AI Rescue Mission — Flipkart Crisis Management Classroom Game

A fully self-contained, single-file web application for running a classroom crisis management game using OpenAI's GPT API.

---

## 🎯 Project Overview

**AI Rescue Mission** is an interactive classroom game where teams are assigned a Flipkart crisis scenario, craft a prompt for ChatGPT, receive 5 AI-generated actions, select their best 3, and get automatically scored by AI. The host (teacher) can monitor all teams on a live leaderboard.

---

## 📁 Files

```
index.html   ← The entire application (single self-contained file)
README.md    ← This file
```

---

## ✅ Completed Features

### 🏠 Screen 1 — Join Game
- Dropdown selector: Team 1 through Team 10 (no free-text entry)
- Each team has a pre-assigned Flipkart crisis scenario
- Scenario preview card shown when team is selected
- Two role buttons: **Join as Team** and **Join as Host**
- Host requires password: `host123`
- Smooth animated entry transitions

### 🎮 Screen 2 — Game Screen (Team View)
- Crisis scenario displayed prominently (team name + full description)
- ⏱️ **5-minute countdown timer** (circular SVG progress ring)
  - Turns red when under 60 seconds
  - Locks all inputs when time expires
- 🔑 **OpenAI API key** input (saved to localStorage, pre-filled on return)
- ✍️ **Prompt input** (max 800 characters, with character counter)
- 🚀 "Get AI Actions" button calling GPT-4o-mini
- Loading spinner while fetching
- **Exactly 5 action cards** displayed with staggered animation
- Checkbox selection — **enforced limit of exactly 3**
  - Disabled cards once 3 selected; uncheck to re-select
- ✅ Submit button only enabled with exactly 3 selected
- 📊 **Auto-scoring** via second OpenAI call after submission
- Score breakdown with animated progress bars
- AI feedback text shown after scoring
- **One-time submission** enforced via localStorage
- "Already Submitted" view if team revisits

### 🎓 Screen 3 — Host Dashboard
- Password: `host123`
- **Live leaderboard** sorted by total score (highest first)
- 🥇🥈🥉 Medal badges for top 3 teams
- Stats panel: Teams submitted, Total teams, Avg score, Top score
- Completion progress bar
- Per-team collapsible details:
  - Team prompt
  - All 5 AI actions (with ✅ marker on selected ones)
  - Score breakdown (mini bar charts per criterion)
  - AI feedback text
- Color coding: 🟢 8-10 | 🟠 5-7 | 🔴 0-4
- 🔄 Auto-refresh every 10 seconds
- 🗑️ "Reset" button to clear all submissions (with confirmation)
- 🖨️ Print-ready layout

### Scoring Criteria (Total: 10 marks)
| Criterion | Marks |
|---|---|
| Prompt Quality | 2 |
| Relevance of 5 Actions | 2 |
| Selection of Best 3 | 3 |
| Prioritization | 2 |
| Clarity | 1 |
| **Total** | **10** |

---

## 👥 Team Scenarios

| Team | Crisis |
|------|--------|
| Team 1 | Website Crash (IT Operations) |
| Team 2 | Payment Failure Crisis (Payment Systems) |
| Team 3 | Delivery Delays (Logistics) |
| Team 4 | Wrong Product Delivered (Order Fulfillment) |
| Team 5 | App Failure (Mobile App Team) |
| Team 6 | Fake Reviews Issue (Trust & Safety) |
| Team 7 | Inventory Mismatch (Inventory Management) |
| Team 8 | Data Security Risk (Cybersecurity) |
| Team 9 | Seller Visibility Issue (Platform Management) |
| Team 10 | Website Slowdown (Performance Optimization) |

---

## 🚀 How to Run

### Option 1 — Open Directly
Just open `index.html` in any modern browser. No server, no build tools needed.

### Option 2 — Live Server (VS Code)
1. Install the "Live Server" extension in VS Code
2. Right-click `index.html` → "Open with Live Server"

### Option 3 — Simple HTTP Server
```bash
# Python
python -m http.server 8080

# Node.js
npx serve .
```

---

## 🔑 OpenAI API Key Setup

1. Go to [platform.openai.com](https://platform.openai.com)
2. Create an account and navigate to **API Keys**
3. Create a new secret key (starts with `sk-`)
4. On the game screen, paste it into the 🔑 API Key field and click **Save**
5. The key is stored in your browser's `localStorage` only — never transmitted anywhere except directly to OpenAI

> **Note:** The app uses `gpt-4o-mini` model. Ensure your API key has access to this model and sufficient credits.

---

## 🎓 How to Run the Classroom Game

### Setup (Teacher/Host)
1. Open `index.html` in a browser on your display/projector
2. Click "Join as Host" → enter password `host123`
3. Keep the Host Dashboard open to monitor teams

### For Each Team
1. Open `index.html` on their device
2. Select their team number from the dropdown
3. Read the scenario, then click **"Join as Team"**
4. Enter the shared OpenAI API key
5. Write a thoughtful prompt describing their crisis approach
6. Click **"Get AI Actions"** and wait for 5 actions to appear
7. Carefully select the **3 best actions**
8. Click **"Submit My 3 Actions"** before the 5-minute timer ends

### During the Game
- Teams have **5 minutes** on the clock
- Each team can only submit **once**
- Host can see results appear in real-time on the dashboard
- Dashboard auto-refreshes every 10 seconds

---

## 💾 Data Storage

All data is stored in the browser's `localStorage`:

| Key | Contents |
|-----|----------|
| `openai_api_key` | Encrypted API key |
| `rescue_team_1` … `rescue_team_10` | Team submissions |

### Submission Data Structure
```json
{
  "teamNum": 1,
  "teamName": "Team 1",
  "scenarioTitle": "Website Crash",
  "scenarioDesc": "Full scenario text...",
  "prompt": "Team's typed prompt",
  "allActions": ["Action 1", "Action 2", "Action 3", "Action 4", "Action 5"],
  "selectedActions": ["Action 1", "Action 3", "Action 5"],
  "selectedIndices": [0, 2, 4],
  "scores": {
    "promptQuality": 2,
    "relevanceOf5Actions": 2,
    "selectionOfBest3": 3,
    "prioritization": 2,
    "clarity": 1,
    "totalScore": 10,
    "feedback": "Excellent crisis management approach..."
  },
  "timestamp": 1703000000000
}
```

---

## 🛠️ Technical Stack

- **Frontend:** Vanilla HTML5 + CSS3 + JavaScript (ES6+)
- **Fonts:** Google Fonts — Poppins
- **AI:** OpenAI Chat Completions API (`gpt-4o-mini`)
- **Storage:** Browser localStorage
- **No backend, no build tools, no dependencies**

---

## ⚠️ Known Constraints

- All participants must use the same OpenAI API key (or each have their own)
- Data is per-browser — host must be on the same browser/device as teams, OR teams can share results via screenshots
- For a multi-device classroom setup, all devices need access to the same localStorage — open in the same browser or use a shared device
- Each team should only have **one active browser tab** to avoid timer conflicts

---

## 🔮 Recommended Next Steps

1. **Multi-device sync** — Replace localStorage with a real-time backend (Firebase, Supabase) for true cross-device leaderboard
2. **Teacher API key management** — Host sets the API key once, teams don't need it
3. **More scenarios** — Add 10+ more Flipkart crisis categories
4. **Replay mode** — Host can replay submissions with commentary
5. **Team name customization** — Allow custom team names alongside team numbers
6. **Export to PDF/CSV** — Download full results as a spreadsheet
