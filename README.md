# 🍜 Aura Food - Mood-Based Food Recommendations

> **Order confidently in 90 seconds** - Capture menu, select vibe, get AI-powered dish recommendations tailored to your mood!

[![React Native](https://img.shields.io/badge/React%20Native-TypeScript-blue.svg)](https://reactnative.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Python%203.8+-green.svg)](https://fastapi.tiangolo.com/)
[![GPT-4](https://img.shields.io/badge/AI-GPT--4-purple.svg)](https://openai.com/)
[![Status](https://img.shields.io/badge/Status-MVP%20Sprint-orange.svg)]()
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 🎯 Core Hypothesis (H1)

**Users will trust AI food recommendations based on their mood/context enough to follow at least one suggested dish.**

### Target Users
International students and young professionals (22-35) navigating unfamiliar restaurant menus in real-time dining situations.

### Problem We Solve
- 🌍 **Language Anxiety**: Non-native speakers struggling with menu terminology
- ⏱️ **Decision Fatigue**: 50+ unfamiliar items, 10 minutes to decide
- 🤔 **Trust Barrier**: Uncertainty about dish contents and spice levels
- 👥 **Group Coordination**: Managing different preferences and dietary needs

## ✨ The Aura Solution

**90-Second Promise**: From confusion to confident order in less time than asking a waiter.

### How It Works
1. 📸 **Capture** (10s) - Snap a photo of the menu
2. 🎭 **Vibe** (15s) - Select 1-3 mood bubbles + party size
3. 🍽️ **Plan** (5s) - Get 3-5 AI-powered dish recommendations
4. 👆 **Swipe** (10s) - Right to accept, left to skip
5. ✅ **Confirm** (5s) - Your personalized order ready!

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Python 3.8+
- Expo Go app (iOS/Android)
- API Keys: OpenAI GPT-4, Google Cloud Vision

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/aura-food-app.git
cd aura-food-app

# Frontend Setup (React Native + TypeScript)
cd mobile
npm install
cp .env.example .env  # Add your API keys
npx expo start

# Backend Setup (FastAPI + Python)
cd ../backend
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env  # Add API keys
uvicorn app.main:app --reload --port 8000

# Scan QR code in Expo Go to launch!
```

## 🎭 Vibe System (8 Core Moods)

| Vibe | Emoji | Intent | Example Dishes |
|------|-------|--------|----------------|
| **Comfort** | 😌 | Familiar, warm | Pad Thai, Pizza |
| **Adventure** | 🔥 | Try new things | Tom Yum, Mole |
| **Light** | 🥗 | Not heavy | Som Tam, Salads |
| **Quick** | ⚡ | Fast eating | Tacos, Panini |
| **Sharing** | 👥 | Group friendly | Nachos, Platters |
| **Budget** | 💰 | Under $15 | Rice bowls, Pasta |
| **Healthy** | 💪 | Nutritious | Grilled options |
| **Indulgent** | 🎉 | Treat yourself | Lasagna, Desserts |

## 🏗️ Architecture

```
┌─────────────────────────┐
│   React Native App      │
│   (TypeScript + Expo)   │
└───────────┬─────────────┘
            │ HTTPS/REST
┌───────────▼─────────────┐
│   FastAPI Backend       │
│   /api/v1/* endpoints   │
└───────────┬─────────────┘
            │
┌───────────▼─────────────┐
│   Services Layer        │
├─────────────────────────┤
│ • OCR (Google Vision)   │
│ • LLM (GPT-4)          │
│ • Storage (SQLite)      │
└─────────────────────────┘
```

### Tech Stack
- **Frontend:** React Native, TypeScript, Expo SDK 49
- **Backend:** FastAPI, Python 3.8+, Pydantic v2
- **AI/ML:** OpenAI GPT-4, Google Cloud Vision OCR
- **Database:** SQLite (MVP), PostgreSQL (Production)
- **State:** Zustand (Frontend), Session-based (Backend)

## 🎨 Design System

### Color Palette
```css
--coral-primary: #FF6B6B    /* CTAs, Energy */
--mint-fresh: #A8E6CF       /* Success states */
--golden-joy: #FFD93D       /* Celebrations */
--warm-white: #FAFAF8       /* Backgrounds */
--soft-black: #2C3E50       /* Text */
```

### Screen Flow
| Screen | Purpose | Duration |
|--------|---------|----------|
| **Camera Capture** | Menu photo with OCR | 10s |
| **Vibe Selection** | 8 mood bubbles + party size | 15s |
| **Swipe Cards** | 3-5 dish recommendations | 10s |
| **Success** | Order confirmation + celebration | 5s |

## 📂 Project Structure

```
aura-food-app/
├── mobile/                    # React Native Frontend
│   ├── App.tsx               # Entry point
│   ├── src/
│   │   ├── screens/          # Main app screens
│   │   │   ├── CaptureScreen.tsx
│   │   │   ├── VibeScreen.tsx
│   │   │   └── SwipeScreen.tsx
│   │   ├── components/       # Reusable components
│   │   │   ├── VibeBubble.tsx
│   │   │   ├── SwipeCard.tsx
│   │   │   └── ProgressDots.tsx
│   │   ├── services/         # API integration
│   │   └── store/           # Zustand state
│   └── package.json
│
├── backend/                  # FastAPI Backend
│   ├── app/
│   │   ├── main.py          # FastAPI app
│   │   ├── routers/         # API endpoints
│   │   ├── services/        # Business logic
│   │   │   ├── ocr_service.py
│   │   │   └── llm_service.py
│   │   └── models/          # Pydantic schemas
│   └── requirements.txt
│
└── docs/                     # Specifications
    ├── PRD_Complete.md      # Product requirements
    ├── API_SPEC_MVP.md      # API contracts
    └── UIUX_SPEC_FINAL.md   # Design specs
```

## 📊 MVP Development (7-Day Sprint)

### Sprint Timeline

| Day | Frontend (Wenxuan) | Backend (Kai) | Status |
|-----|-------------------|---------------|---------|
| **Day 1-2** | Setup React Native + TypeScript | FastAPI + SQLite setup | 🟡 Foundation |
| | Navigation structure | Session endpoints | |
| | Camera integration | OCR service setup | |
| **Day 3-4** | Vibe selection UI | LLM integration | 🔴 Core Features |
| | Swipe card mechanics | Recommendation engine | |
| | Local storage | Vibe → dish mapping | |
| **Day 5-6** | Animations & haptics | Error handling | 🔴 Polish |
| | Success celebrations | Rate limiting | |
| | Error recovery flows | Analytics tracking | |
| **Day 7** | Device testing | Integration tests | 🔴 Testing |
| | Performance tuning | API documentation | |
| | User testing (10 users) | Deployment prep | |

### Success Metrics (H1 Validation)
- ✅ **Primary:** ≥40% users pick at least 1 recommended dish
- ✅ **Time to decision:** <90 seconds
- ✅ **Completion rate:** >60% reach confirmation
- ✅ **Trust indicator:** >50% select ≥2 dishes

## 🧪 Testing

### Quick Test Flow
```bash
# Mobile
npm test

# Backend
pytest

# Manual Testing
# 1. Open app
# 2. Take photo of menu
# 3. Select vibes
# 4. Get recommendation
# 5. Rate experience
```

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development Setup
```bash
# Install pre-commit hooks
npm run setup-hooks

# Run linters
npm run lint

# Format code
npm run format
```

## 📝 API Documentation

### Core Endpoints (v1)

#### 1. POST /api/v1/sessions
Create a new session for the user journey
```json
// Request
{
  "device_id": "uuid-optional",
  "locale": "en-US",
  "timezone": "America/Los_Angeles"
}

// Response (201)
{
  "session_id": "uuid",
  "created_at": "2024-01-20T12:00:00Z",
  "expires_at": "2024-01-20T13:00:00Z"
}
```

#### 2. POST /api/v1/sessions/{session_id}/scan-menu
Upload menu photo for OCR processing
```json
// Request
{
  "image_base64": "base64_string"
}

// Response (200)
{
  "menu_id": "uuid",
  "confidence": 0.85,
  "menu_items": [
    {
      "name": "Pad Thai",
      "description": "Stir-fried rice noodles",
      "price_range": "$12-14"
    }
  ]
}
```

#### 3. POST /api/v1/sessions/{session_id}/recommendations
Get AI-powered dish recommendations
```json
// Request
{
  "vibe_id": "uuid",
  "menu_id": "uuid"
}

// Response (200)
{
  "recommendation_id": "uuid",
  "recommendations": [
    {
      "dish_name": "Pad Thai",
      "reasoning": "Mild and perfect for first-timers",
      "confidence": 0.89
    }
  ]
}
```

[Full API documentation →](./docs/API_SPEC_MVP.md)

## 🐛 Known Issues

- Camera permission prompt may appear twice on iOS
- Mock data only includes 3 restaurants
- Memory resets on app reinstall (use cloud storage in v2)

## 🚀 Deployment

### Mobile (Expo)
```bash
# Build for iOS
expo build:ios

# Build for Android
expo build:android

# Publish to Expo Go
expo publish
```

### Backend (Production)
```bash
# Using Docker
docker build -t vibe-food-api .
docker run -p 8000:8000 vibe-food-api

# Using Heroku
heroku create vibe-food-api
git push heroku main
```

## 📚 Resources

- [Product Requirements Document](./PRD.md)
- [Technical Specification](./TECHNICAL_SPEC.md)
- [Implementation Guide](./IMPLEMENTATION_GUIDE.md)
- [API Documentation](./docs/API.md)
- [Design System](./docs/DESIGN.md)

## 📄 License

MIT License - see [LICENSE](LICENSE) file

## 🙏 Acknowledgments

- OpenAI for GPT-4 API
- Google Cloud Vision for OCR
- Expo team for amazing mobile tools
- FastAPI for blazing fast backend
- You, for trying out our app!

## 📞 Contact & Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/vibe-food-app/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/vibe-food-app/discussions)
- **Email:** team@vibefood.app

---

<div align="center">

**Built with ❤️ in 7 days using TypeScript & Python**

*Making food ordering delightful for international students, everywhere*

[Demo](https://vibefood.app) | [Documentation](./docs) | [Contribute](CONTRIBUTING.md)

</div>