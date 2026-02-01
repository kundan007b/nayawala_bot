# 🛠️ Complete Setup Guide - Kids Video Pipeline

This guide walks you through setting up the n8n Kids Video Pipeline from scratch.

**Your n8n Instance:** https://n8n.kbhaskar.tech

---

## 📋 Part 1: Prerequisites

Your n8n is already hosted! Skip to Part 2.

If you need to restart n8n locally:

#### Option A: Docker (Recommended)
```bash
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n n8nio/n8n
```

#### Option B: npm (Node.js 18+)
```bash
npm install -g n8n
n8n start
```

---

## 📋 Part 2: Get API Keys

### 2.1 Google Gemini API (FREE)
1. Go to [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Sign in with Google
3. Click "Create API Key"
4. Copy the key (starts with `AIza...`)

### 2.2 Create Google Sheet
1. Go to [sheets.google.com](https://sheets.google.com)
2. Create a new spreadsheet named "Kids Video Pipeline"
3. In Row 1, add these headers:
   ```
   ID | Title | Summary | Characters | Moral | Origin | Difficulty | Status | Created_At
   ```
4. Copy the Sheet ID from the URL:
   ```
   https://docs.google.com/spreadsheets/d/[THIS_IS_YOUR_SHEET_ID]/edit
   ```

### 2.3 ElevenLabs API (Optional - for voice)
1. Sign up at [elevenlabs.io](https://elevenlabs.io)
2. Go to Profile → API Key
3. Copy your API key

### 2.4 Creatomate API (Optional - for video)
1. Sign up at [creatomate.com](https://creatomate.com)
2. Go to Settings → API
3. Copy your API key

---

## 📋 Part 3: Configure n8n

### 3.1 Set Environment Variables

In n8n, go to **Settings → Variables** and add:

| Variable Name | Value |
|---------------|-------|
| `GOOGLE_GEMINI_API_KEY` | Your Gemini API key |
| `GOOGLE_SHEET_ID` | Your Google Sheet ID |
| `ELEVENLABS_API_KEY` | (Optional) ElevenLabs key |
| `CREATOMATE_API_KEY` | (Optional) Creatomate key |

### 3.2 Set Up Google Sheets Credential

1. In n8n, go to **Settings → Credentials**
2. Click **+ Add Credential**
3. Search for "Google Sheets"
4. Choose "OAuth2" method
5. Follow the OAuth flow to connect your Google account

---

## 📋 Part 4: Import the Workflow

### 4.1 Import Workflow JSON

1. In n8n, click the **☰ Menu** (top-left)
2. Click **Import from File**
3. Select: `d:\n8nbot\kids_video_pipeline_complete.json`
4. Click **Import**

### 4.2 Update Credential References

After import, you'll see some nodes with ⚠️ warnings:
1. Click on **"Save to Google Sheets"** node
2. Select your Google Sheets credential from the dropdown
3. Repeat for any other Google Sheets nodes

---

## 📋 Part 5: Test the Workflow

### 5.1 Test Topic Generation

1. Click **"Start Pipeline"** node
2. Click **Test step** (or press T)
3. In the input data, paste:
   ```json
   {
     "mode": "generate_topics",
     "topic_request": "5 popular fairy tales",
     "story_origin": "European",
     "target_count": 5
   }
   ```
4. Click **Execute Workflow**
5. Check: Stories should appear in your Google Sheet!

### 5.2 Test Script Generation

1. Copy a story ID from your Google Sheet (e.g., `story_1738435500000_0`)
2. Click **"Start Pipeline"** node
3. Set input:
   ```json
   {
     "mode": "generate_script",
     "story_id": "YOUR_STORY_ID_HERE",
     "narrator": "mira"
   }
   ```
4. Execute and check the output!

---

## 🔧 Troubleshooting

### "Sheet not found" Error
- Check GOOGLE_SHEET_ID is correct
- Ensure sheet name is exactly "Story Pool"

### "API Key invalid" Error
- Verify GOOGLE_GEMINI_API_KEY is set in Variables
- Check there are no extra spaces in the key

### "No stories found" Error
- Try a more specific topic_request
- Reduce target_count to 5

---

## ✅ You're Ready!

Once you see stories in your Google Sheet and scripts generating, the pipeline is working!

**Next steps:**
- Add ElevenLabs for voice generation
- Add Creatomate for video rendering
- Schedule automatic runs
