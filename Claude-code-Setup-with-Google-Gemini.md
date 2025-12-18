# Claude Code Setup with Google Gemini for Free
---

# Prerequisites
- **Node.js v18 or later**
---

## 🔑 Step1: Generate Your Google API Key

1. Visit: [https://aistudio.google.com](https://aistudio.google.com)
2. Select **Get API Key**
3. Click **Create API Key**
4. Copy the key (looks like: ```AIzaSy...............```)
---

## 🚀 Step 2: Install Required CLI Tools

Open PowerShell (Run as Administrator):

```powershell
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
```

This installs both Claude Code and the router globally.

---

## 📁 Step 3: Create Required Configuration Directories

Run the following in a normal PowerShell window:

```powershell
mkdir $HOME/.claude-code-router
mkdir $HOME/.claude
```

---

## ⚙️ Step 4: Create the Router Configuration File

Since Windows does not support `cat << EOF` syntax, create the configuration file using Notepad:

```powershell
notepad $HOME/.claude-code-router/config.json
```

Paste the following JSON configuration exactly as shown:

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-2.5-flash",
        "gemini-2.0-flash"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "gemini,gemini-2.5-flash",
    "think": "gemini,gemini-2.5-flash",
    "longContext": "gemini,gemini-2.5-flash",
    "longContextThreshold": 60000
  }
}
```

Save and close Notepad once done.

---

## 🔑 Step 5: Configure Your Environment Variable (API Key)

Run PowerShell as Administrator:

```powershell
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'YOUR_API_KEY_HERE', 'User')
```

### Verify the Key

Close PowerShell → open a new window → run:

```powershell
echo $env:GOOGLE_API_KEY
```

If the key appears, the environment variable is configured correctly.

---

## ▶️ Step 6: Validate Installation

Run the following commands:

```powershell
claude --version
ccr version
echo $env:GOOGLE_API_KEY
```

If all commands return output without errors, the setup is successful.

---

### 🎯 Step 6: Start the Router (Terminal 1)

```powershell
ccr start
```

Wait until you see:

```
✔ Service started successfully
```

### Use Claude Code (Terminal 2)

Navigate to your project:

```powershell
cd your-project-folder
ccr code
```

## 🔍 Step 7: Quick Test

Run:

```powershell
ccr code
```

Then type:

```
hi
```

If Claude responds, your Claude Code + Gemini setup is fully operational.

