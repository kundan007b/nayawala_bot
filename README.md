# 🎬 Kids Video Pipeline - AI-Powered Children's Story Video Generator

An n8n-based automation pipeline that generates engaging 1-minute story videos for children, optimized for YouTube Shorts, Instagram Reels, and TikTok.

## 🌟 Features

- **AI-Powered Story Research** - Automatically finds and structures stories from various sources
- **Scene-by-Scene Script Generation** - Creates detailed video scripts with Google Gemini
- **Natural Voice Generation** - Child-friendly voices with ElevenLabs
- **AI Image Generation** - Colorful, engaging visuals with Pollinations.ai
- **Automated Video Assembly** - Professional video rendering with Creatomate
- **Multi-Platform SEO** - Optimized metadata for YouTube, Instagram, and TikTok
- **Human-in-the-Loop** - Preview and approve before generating assets
- **Recurring Characters** - Consistent characters across all videos

## 📁 Project Structure

```
d:\n8nbot\
├── workflows/                    # n8n workflow JSON files
│   ├── topic_pool_generator.json
│   ├── script_generator.json
│   ├── asset_generator.json
│   ├── video_assembler.json
│   ├── metadata_generator.json
│   └── master_pipeline.json
├── data/
│   ├── characters.json           # Character definitions
│   ├── scripts/                  # Generated scripts
│   ├── assets/                   # Voice & images per story
│   ├── metadata/                 # Platform metadata
│   └── videos/                   # Final rendered videos
├── templates/                    # Creatomate templates
├── .env.example                  # Environment config template
└── README.md
```

## 🚀 Quick Start

### 1. Prerequisites

- **n8n instance** (self-hosted or cloud)
- **API Keys** for:
  - Google Gemini (free tier available)
  - Gemini with Google Search grounding
  - ElevenLabs ($22/mo for 100 mins)
  - Creatomate ($12/mo for 100 videos)
- **Google Sheets** for story pool management
- **Slack** (optional) for notifications

### 2. Setup Steps

1. **Copy `.env.example` to `.env`** and fill in your API keys

2. **Create Google Sheet** with columns:
   - ID, Title, Summary, Characters, Moral, Origin, Difficulty, Status, Created At, Script URL, Video URL, Published

3. **Import workflows to n8n**:
   - Go to n8n → Settings → Import
   - Import each JSON file from `workflows/` folder

4. **Configure credentials in n8n**:
   - Google Sheets OAuth2
   - Google Gemini API
   - Slack API (optional)
   - Set environment variables

5. **Create Creatomate template** (see template guide below)

### 3. Usage

#### Generate Topic Pool
```json
{
  "mode": "generate_topics",
  "topic_request": "50 Panchatantra stories",
  "story_origin": "Indian",
  "target_count": 50
}
```

#### Generate Video for a Story
```json
{
  "mode": "full_pipeline",
  "story_id": "story_1234567890_0",
  "narrator": "mira"
}
```

## 🎭 Characters

| Character | Role | Voice Style |
|-----------|------|-------------|
| **Mira** | Main Narrator | Cheerful, young girl |
| **Bolo** | Comic Relief | Excited, playful parrot |
| **Dadu** | Wisdom Narrator | Gentle, wise owl |
| **Sunny** | Adventure Narrator | Brave, friendly elephant |

## 📊 Workflow Pipeline

```
Topic Request → Web Search → Story Pool
                              ↓
Story Selection → Script Generation → Approval
                                        ↓
Voice Generation ←→ Image Generation ←→ Music Selection
                              ↓
                    Video Assembly (Creatomate)
                              ↓
             SEO Metadata → Ready to Publish!
```

## 💰 Cost Estimate

| Service | Cost | Per Video |
|---------|------|-----------|
| Google Gemini | Free tier | ~$0 |
| ElevenLabs | $22/mo | ~$0.30 |
| Pollinations.ai | Free | $0 |
| Creatomate | $12/mo | ~$0.12 |
| **Total** | | **~$0.50-0.70** |

## 🔧 Customization

### Add New Character
Edit `data/characters.json` and add:
```json
{
  "id": "new_char",
  "name": "Character Name",
  "role": "narrator",
  "voice_id": "ElevenLabs_voice_id",
  "visual_style": "Description for image generation",
  "personality": "Character traits",
  "catchphrase": "Signature line"
}
```

### Change Video Style
Modify the `visual_style_guide` in `characters.json` to change:
- Art style
- Color palette
- Background style

## 📝 License

MIT License - Feel free to use and modify for your projects.

## 🤝 Support

For issues or questions, create a GitHub issue or reach out on the n8n community forum.
