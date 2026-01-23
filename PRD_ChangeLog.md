# PRD Change Log

## Version 3.0 - Evidence-Safe MVP Edition
**Date:** January 2025
**Editor:** Claude Code with PM guidance

### Major Changes

#### 🎯 Removed Unverified Claims
- ❌ Removed: "272M international migrants, 40M students" (no source)
- ❌ Removed: "73% report menu anxiety" (no methodology)
- ❌ Removed: "85% reduction in decision time" (not measured)
- ❌ Removed: "75% order satisfaction by session 5" (speculative)
- ✅ Replaced with: Assumptions to validate via MVP testing

#### 📦 Clarified Real MVP Scope
- ✅ Real OCR via Google Cloud Vision API (not mock menus)
- ✅ Real LLM reasoning with GPT-4 (not static mappings)
- ✅ NO adaptive memory in v1.0 (collect feedback for v1.1)
- ✅ Clear 7-day sprint deliverables with team assignments

#### 🔄 Added Concrete UX Flow
- ✅ Added OCR error recovery screen with retry options
- ✅ Specified 5 clear states: Capture → Vibe → Recommendation → Confirmation → Feedback
- ✅ Defined error handling for each state
- ✅ No fallback to sample menus (real OCR only)

#### 🏗️ Technical Specifications
- ✅ Added complete data models (TypeScript interfaces)
- ✅ Added API contracts with request/response examples
- ✅ Added LLM structured output requirements
- ✅ Specified SQLite storage strategy
- ✅ Removed premature optimization (Redis, 99.9% uptime, etc.)

#### 🎭 Evidence-Based Features
- ✅ Added 8-vibe system based on mood-food correlation research
- ✅ Added testable metrics (40% recommendation acceptance)
- ✅ Added instrumentation events for tracking
- ✅ Added 10-user experiment design

#### 🍽️ Food Safety Requirements
- ✅ Added allergen handling strategy (text matching only)
- ✅ Added disclaimer requirements
- ✅ Added menu processing flow
- ✅ Clear scope: dine-in only, no ordering

#### 🚨 Risk Analysis
- ✅ Added MVP-specific risks (OCR failure, allergen hallucination)
- ✅ Added concrete mitigations
- ✅ Added blocking open questions

### What Was Kept
- ✅ User journey maps (valuable for understanding flow)
- ✅ Core hypothesis H1 (refined and clarified)
- ✅ Team structure and timeline
- ✅ Visual design system (needed for implementation)

### Why These Changes Matter

1. **Evidence-Safe**: No unverified market claims that could mislead stakeholders
2. **Executable**: Clear technical specs that developers can implement
3. **Testable**: Defined metrics and experiment to validate H1
4. **Realistic**: 7-day scope with real OCR/LLM but no complex features
5. **Safe**: Proper allergen handling and disclaimers

### Next Steps
1. Team review of technical specifications
2. Finalize OCR API choice (Google Vision vs AWS Textract)
3. Begin prompt engineering for LLM recommendations
4. Set up instrumentation for metrics tracking