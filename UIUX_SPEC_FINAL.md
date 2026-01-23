# UI/UX Specification - Aura Food MVP
## Consolidated Engineering-Ready Design Specification

*Version 1.0 - MVP Edition (7-Day Sprint)*
*Last Updated: January 2025*

---

## 1. Product UX Summary (MVP)

Aura Food enables international students and young professionals to confidently order from unfamiliar restaurant menus in under 90 seconds. Users capture a menu photo, select mood vibes, and receive 3-5 AI-powered dish recommendations with clear reasoning. The entire flow—from confusion to decision—takes less time than asking a waiter for recommendations, while building trust through transparency and celebration moments.

---

## 2. Target Users & Context

### Primary Scenarios
1. **Lunch Rush Alex** - Thai restaurant, 10 minutes to order, 50+ unfamiliar items, mild social pressure
2. **Group Dinner Sam** - Coordinating for 4 friends with different preferences, budget conscious
3. **First Visit Chen** - New to Mexican cuisine, doesn't recognize most dish names, dietary restrictions

### Core Constraints
- **Language anxiety**: Non-native speakers need simple, clear instructions
- **Time pressure**: Peak hours require sub-90-second decisions
- **Trust barrier**: First-time users skeptical of AI recommendations
- **Cognitive load**: Unfamiliar ingredients and preparation methods

---

## 3. Information Architecture

### MVP Navigation Model
```
Linear Flow (Not Tabs)
├── Screen 1: Capture & Vibe
│   ├── State A: Camera/Upload
│   ├── State B: OCR Processing
│   └── State C: Vibe Selection
├── Screen 2: Plan Review
│   ├── Swipeable Cards
│   └── Progress Indicator
└── Screen 3: Success/Feedback
    ├── Celebration
    └── Quick Rating
```

### Screen Inventory (MVP)
1. **Onboarding** - Single preference screen (20 seconds max)
2. **Capture & Vibe** - Camera + mood selection
3. **Plan Review** - Swipeable recommendation cards
4. **Success** - Order confirmation + celebration
5. **Error Recovery** - OCR failure handling

### Post-MVP Screens
- Profile/Settings
- Order History
- Restaurant Browse
- Social Sharing

---

## 4. Core MVP User Flows

### Flow 1: First-Time User Journey
```
Entry: App Launch (first time)
1. Welcome screen with value prop (5 seconds)
2. Quick preferences: spice level + allergies (15 seconds)
3. Camera permission request
4. → Main capture flow

Success: Preferences saved, ready to order
Failure: Skip onboarding → limited personalization
Recovery: Can set preferences later in any flow
```

### Flow 2: Menu Capture to Recommendation
```
Entry: App open (returning user)
1. Camera viewfinder active (immediate)
2. Capture menu photo → OCR processing (3-5 seconds)
3. If OCR confidence <60% → Error recovery screen
4. Display extracted menu items for confirmation
5. Show 8 vibe bubbles based on context
6. User selects 1-3 vibes + party size
7. Generate recommendations (2-3 seconds loading)
8. Display 3-5 swipeable cards

Success: At least 1 dish selected
Failure: All dishes rejected → feedback form
Edge Case: OCR complete failure → manual restaurant search
```

### Flow 3: Swipe Decision Flow
```
Entry: Recommendation cards displayed
1. First card visible, next card peeking
2. Swipe right → Card turns green, flies right
3. Swipe left → Card turns red, flies left
4. Progress dots update
5. After last card → Success or feedback screen

Success: 1+ dishes approved → celebration
Failure: All rejected → "Let's try different vibes"
Undo: Shake device within 3 seconds
```

---

## 5. Screen-by-Screen Specifications

### Screen 1.1: Onboarding (First Launch Only)

**Purpose**: Build trust and collect minimal preferences in <20 seconds

**Layout**:
```
┌─────────────────────────┐
│    Status Bar (44px)    │
├─────────────────────────┤
│        (100px)          │
│      🍜 (80x80)         │ ← Gentle pulse animation
│     "Aura Food"         │ ← Fade in
│        (40px)           │
├─────────────────────────┤
│ "Order confidently      │ ← 24px Poppins SemiBold
│  in 90 seconds"         │   #2C3E50
│        (40px)           │
├─────────────────────────┤
│   Spice tolerance?      │ ← 16px label
│ [None][Mild][Hot]       │ ← Segmented control
│        (60px)           │   Required selection
├─────────────────────────┤
│     Allergies?          │
│ [None] [Select→]        │ ← Optional chips
│        (60px)           │
├─────────────────────────┤
│    [Let's eat!]         │ ← Primary CTA
│        (60px)           │   Disabled until spice
└─────────────────────────┘
```

**States**:
- Loading: Not applicable
- Error: Network failure → Continue without preferences
- Offline: Works offline, saves locally

**Microcopy**:
- Title: "Order confidently in 90 seconds" (7 words)
- CTA: "Let's eat!" (2 words)
- Skip: "Skip for now" (3 words)

### Screen 1.2: Capture & Vibe

**State A: Camera Capture**

```
┌─────────────────────────┐
│    Camera Viewfinder    │
│     (Full screen)       │
│                         │
│  ┌─────────────────┐   │ ← Guide overlay
│  │                 │   │   Dashed white border
│  │  Point at menu  │   │   Semi-transparent
│  │                 │   │
│  └─────────────────┘   │
│                         │
├─────────────────────────┤
│  [Gallery] [📸] [Tips]  │ ← Bottom bar (100px)
└─────────────────────────┘
```

**Camera Requirements**:
- Auto-focus on guide area
- Flash auto-detect in low light
- Min resolution: 1080p for OCR
- Max file size: 5MB
- Haptic: Light on capture

**State B: OCR Processing**

```
┌─────────────────────────┐
│                         │
│    "Reading menu..."    │ ← Pulsing dots animation
│      [········]         │   300ms per dot
│                         │
│   "Thai House Menu"     │ ← Restaurant name if detected
│                         │
└─────────────────────────┘
```

**State C: Vibe Selection**

```
┌─────────────────────────┐
│   Thai House • Thai 🌶️  │ ← Context header (40px)
├─────────────────────────┤
│  "What's your vibe?"    │ ← 20px Poppins Medium
│        (40px)           │
├─────────────────────────┤
│  ┌────┐ ┌────┐ ┌────┐  │ ← Vibe bubbles (80x80)
│  │ 😌 │ │ 🔥 │ │ 🥗 │  │   Rounded squares
│  │Safe│ │Bold│ │Light│ │   Breathe animation
│  └────┘ └────┘ └────┘  │
│                         │
│  ┌────┐ ┌────┐ ┌────┐  │
│  │ ⚡ │ │ 👥 │ │ 💰 │  │ ← Contextual vibes
│  │Fast│ │Share│ │Save│ │   Based on time/party
│  └────┘ └────┘ └────┘  │
│                         │
│  ┌────┐ ┌────┐         │
│  │ 💪 │ │ 🎉 │         │
│  │Fuel│ │Treat│        │
│  └────┘ └────┘         │
│        (280px)         │
├─────────────────────────┤
│ Party size: [-][2][+]  │ ← Stepper (44px)
│        (60px)           │
├─────────────────────────┤
│   [Get my plan →]       │ ← Primary CTA
│        (80px)           │   Enabled after 1 vibe
└─────────────────────────┘
```

**Vibe Behavior**:
- Max 3 selections
- First tap: Select (scale 0.95, border appears)
- Second tap: Deselect
- Auto-proceed after 3 selections + 1 second delay

### Screen 2: Plan Review (Swipeable Cards)

```
┌─────────────────────────┐
│  "Your comfort feast"   │ ← Dynamic header
│   4 dishes • $32-38     │   Based on vibes
│        (60px)           │
├─────────────────────────┤
│                         │
│  ╭───────────────────╮  │ ← Card 1 of 4
│  │   Pad Thai         │  │   Height: 400px
│  │       🍜           │  │   Border-radius: 20px
│  │                   │  │   Shadow: 0 8px 24px
│  │  "Mild and sweet,  │  │
│  │   perfect for      │  │ ← Story copy (16px)
│  │   first-timers"    │  │
│  │                   │  │
│  │  ─────────────    │  │
│  │  Why this?         │  │ ← Reasoning (14px)
│  │  You picked 'safe' │  │   Color: #7F8C8D
│  │  Most ordered dish │  │   Builds trust
│  │                   │  │
│  │  $12-14           │  │ ← Price estimate
│  ╰───────────────────╯  │
│                         │
│  ← Swipe for more →    │ ← Gesture hints
│                         │   Fade on interaction
│  ● ● ○ ○               │ ← Progress dots
└─────────────────────────┘
```

**Swipe Physics**:
```javascript
const swipeConfig = {
  threshold: screenWidth * 0.3,  // 117px on iPhone 14
  maxRotation: 15,                // degrees
  springBack: {
    tension: 40,
    friction: 10
  },
  exitAnimation: {
    duration: 300,
    easing: 'ease-out'
  },
  haptic: {
    onThreshold: 'light',
    onAccept: 'success',
    onReject: 'light'
  }
};
```

### Screen 3: Success State

```
┌─────────────────────────┐
│                         │
│      ✨ 🎉 ✨         │ ← Confetti (1.5s)
│                         │
│    "Perfect match!"     │ ← Success copy
│        (80px)           │
├─────────────────────────┤
│    Your order:          │
│  ✓ Pad Thai            │ ← Approved items
│  ✓ Spring Rolls        │   Animate in 100ms
│  ✓ Thai Tea            │   staggered
│                         │
│  Total: $28-32          │
│  Serves 2 people        │
│        (120px)          │
├─────────────────────────┤
│   How was this?         │ ← Feedback prompt
│     👍    👎           │   Large touch targets
│        (80px)           │
├─────────────────────────┤
│    [Order again]        │ ← Primary CTA
│   [Different vibes]     │ ← Secondary option
└─────────────────────────┘
```

### Screen 4: Error Recovery (OCR Failure)

```
┌─────────────────────────┐
│                         │
│        😅              │ ← Friendly emoji
│                         │
│ "Couldn't read that"    │ ← Simple message
│  "Try again?"          │
│        (120px)          │
├─────────────────────────┤
│   📸 Photo tips:        │
│  • Good lighting        │ ← Bulleted list
│  • Hold steady          │   14px Regular
│  • Full menu in frame   │
│        (100px)          │
├─────────────────────────┤
│    [Try again]          │ ← Primary action
│  [Search restaurant]    │ ← Alternative
└─────────────────────────┘
```

---

## 6. Component System

### VibeBubble Component

```typescript
interface VibeBubbleProps {
  emoji: string;          // Single emoji character
  label: string;          // 1-2 words max
  isSelected: boolean;
  isDisabled: boolean;
  onPress: () => void;
}

const styles = {
  container: {
    width: 80,
    height: 80,
    borderRadius: 16,      // Rounded square
    backgroundColor: '#FAFAF8',
    borderWidth: 2,
    borderColor: isSelected ? '#FF6B6B' : 'transparent',
    shadowColor: isSelected ? '#FF6B6B' : '#000',
    shadowOpacity: isSelected ? 0.3 : 0.1,
  },
  emoji: {
    fontSize: 32,
    marginBottom: 4,
  },
  label: {
    fontSize: 12,
    fontWeight: '600',
    color: '#2C3E50',
  }
};
```

### SwipeableCard Component

```typescript
interface DishCardProps {
  dish: {
    name: string;
    emoji: string;
    description: string;    // 10-15 words
    reasoning: string;      // Why recommended
    price: string;          // "$12-14"
  };
  onSwipeLeft: () => void;
  onSwipeRight: () => void;
}

const animations = {
  swipeRight: {
    overlay: 'rgba(76, 175, 80, 0.3)',  // Green
    icon: '💚',
    rotation: Animated.multiply(deltaX, 0.05),
    translateX: Animated.add(deltaX, 400),
  },
  swipeLeft: {
    overlay: 'rgba(244, 67, 54, 0.3)',  // Red
    icon: '❌',
    rotation: Animated.multiply(deltaX, -0.05),
    translateX: Animated.add(deltaX, -400),
  }
};
```

### Button Component

```typescript
type ButtonVariant = 'primary' | 'secondary' | 'ghost';
type ButtonSize = 'large' | 'medium' | 'small';

interface ButtonProps {
  label: string;
  variant: ButtonVariant;
  size: ButtonSize;
  onPress: () => void;
  isDisabled: boolean;
  isLoading: boolean;
}

const variants = {
  primary: {
    backgroundColor: '#FF6B6B',
    color: '#FFFFFF',
  },
  secondary: {
    backgroundColor: '#A8E6CF',
    color: '#2C3E50',
  },
  ghost: {
    backgroundColor: 'transparent',
    color: '#7F8C8D',
  }
};
```

### ProgressDots Component

```typescript
interface ProgressDotsProps {
  total: number;
  current: number;
}

const styles = {
  dot: {
    width: 8,
    height: 8,
    borderRadius: 4,
    marginHorizontal: 4,
    backgroundColor: '#D0D0D0',
  },
  activeDot: {
    width: 12,
    height: 12,
    borderRadius: 6,
    backgroundColor: '#FF6B6B',
    transform: [{ scale: 1.2 }],
  }
};
```

---

## 7. Interaction Patterns & Animations

### Core Gesture Vocabulary

| Gesture | Action | Visual Feedback | Haptic |
|---------|---------|-----------------|---------|
| Tap | Select/Toggle | Scale 0.95→1.0 (150ms) | Light |
| Swipe Right | Accept | Green glow + rotation | Success |
| Swipe Left | Reject | Red fade + rotation | Light |
| Long Press | Preview | Scale 1.05 + blur bg | Medium |
| Pull Down | Dismiss | Slide down + fade | None |
| Shake | Undo last action | Toast notification | Error |

### Animation Timing

```javascript
const timings = {
  instant: 100,      // Haptic feedback
  quick: 200,        // Button press
  normal: 300,       // Transitions
  smooth: 500,       // Page changes
  celebrate: 1500    // Confetti
};

const springs = {
  gentle: { tension: 120, friction: 14 },
  bouncy: { tension: 180, friction: 12 },
  snappy: { tension: 200, friction: 20 }
};
```

### Celebration Moments

```javascript
const celebrations = {
  firstOrder: {
    trigger: 'First successful plan',
    animation: 'confetti',
    duration: 1500,
    haptic: 'success_pattern'  // 3 vibrations
  },
  perfectMatch: {
    trigger: 'All cards accepted',
    animation: 'stars',
    sound: 'success.mp3'
  },
  quickDecision: {
    trigger: 'Under 30 seconds total',
    animation: 'lightning',
    badge: '⚡ Speed demon!'
  }
};
```

---

## 8. Microcopy Guidelines

### Principles for International Users
1. **Max 10 words per instruction**
2. **No idioms or cultural references**
3. **Active voice only**
4. **Present tense for actions**
5. **Positive framing for errors**

### Copy Templates

**Welcome**:
- ❌ "Let's get this party started!"
- ✅ "Order confidently in 90 seconds"

**Loading**:
- ❌ "Hang tight while we work our magic..."
- ✅ "Creating your plan..."

**Error**:
- ❌ "Oops! Something went wrong"
- ✅ "Let's try again"

**Success**:
- ❌ "Nailed it! You're all set!"
- ✅ "Perfect match!"

**Empty State**:
- ❌ "Nothing to see here"
- ✅ "Take a photo to start"

### Vibe Labels (Tested for Clarity)
- 😌 **Safe** - Not "Comfort" (ambiguous)
- 🔥 **Bold** - Not "Adventure" (unclear)
- 🥗 **Light** - Not "Healthy" (judgmental)
- ⚡ **Quick** - Not "Fast" (food quality concern)
- 👥 **Share** - Not "Group" (noun/verb confusion)
- 💰 **Budget** - Not "Cheap" (negative)
- 💪 **Fuel** - Not "Hearty" (unclear)
- 🎉 **Treat** - Not "Indulgent" (complex word)

---

## 9. Accessibility Requirements

### WCAG 2.1 AA Compliance
- **Touch targets**: Minimum 44x44pt
- **Color contrast**: 4.5:1 for normal text, 3:1 for large
- **Text size**: 14pt minimum, scalable to 200%
- **Focus indicators**: Visible keyboard navigation

### Screen Reader Support
```javascript
// Component example
<VibeBubble
  accessibilityLabel="Safe food vibe"
  accessibilityHint="Double tap to select safe, familiar dishes"
  accessibilityRole="button"
  accessibilityState={{ selected: isSelected }}
/>
```

### Reduced Motion
```javascript
// Respect system settings
const shouldAnimate = !AccessibilityInfo.isReduceMotionEnabled();

const cardAnimation = shouldAnimate
  ? { duration: 300, easing: 'spring' }
  : { duration: 0 };  // Instant transition
```

---

## 10. Analytics Hooks

### Required Instrumentation Events

```typescript
// MVP Critical Events
interface AnalyticsEvent {
  name: string;
  properties: Record<string, any>;
  timestamp: number;
}

const events = {
  // Onboarding
  'onboarding_started': {},
  'onboarding_completed': { duration_seconds: number },
  'onboarding_skipped': { step: string },

  // Capture
  'camera_opened': {},
  'photo_captured': { method: 'camera' | 'gallery' },
  'ocr_started': {},
  'ocr_completed': { confidence: number, duration_ms: number },
  'ocr_failed': { error_type: string },

  // Vibe Selection
  'vibe_selected': { vibe: string, selection_order: number },
  'party_size_set': { size: number },
  'plan_requested': { vibes: string[], party_size: number },

  // Recommendations
  'recommendations_shown': { count: number, generation_time_ms: number },
  'card_swiped': { dish: string, direction: 'left' | 'right', time_to_swipe_ms: number },
  'plan_completed': { accepted: number, rejected: number, total_time_seconds: number },

  // Feedback
  'feedback_given': { type: 'positive' | 'negative' },

  // Success Metrics
  'success_rate': { picked_any: boolean },  // Primary metric
  'time_to_decision': { seconds: number },  // Must be <90
};
```

---

## 11. Resolved Conflicts

### Conflicts Between Specs and Resolution

1. **Color System**
   - Spec 1: Coral/Mint/Gold (youthful, energetic)
   - Spec 2: Sage/Terracotta (mature, calm)
   - **Resolution**: Use Spec 1's palette for target demographic

2. **Navigation Model**
   - Spec 1: Gesture-first single flow
   - Spec 2: Tab-based navigation
   - **Resolution**: Linear flow per PRD requirement

3. **Onboarding Duration**
   - Spec 1: 2-tap magic (30+ seconds)
   - PRD: 20 seconds maximum
   - **Resolution**: Single preference screen, 20 seconds

4. **Vibe Count**
   - Spec 1 shows: 9 vibes in mockups
   - PRD specifies: 6-8 vibes
   - **Resolution**: Exactly 8 vibes for optimal choice

5. **Typography**
   - Spec 1: Multiple custom fonts
   - Spec 2: System fonts
   - **Resolution**: Poppins for headers (personality), System for body (performance)

---

## 12. Post-MVP Features (Not in 7-Day Sprint)

### Phase 2 (Weeks 3-4)
- User accounts and authentication
- Order history with reorder
- Multiple restaurant support
- Advanced dietary restrictions
- Social sharing ("My Aura order")

### Phase 3 (Weeks 5-8)
- Restaurant API integration
- Real-time menu updates
- Group ordering coordination
- Budget optimization algorithm
- Nutrition information display

### Phase 4 (Weeks 9-12)
- Personalized learning system
- Cross-restaurant preferences
- Delivery integration
- Payment processing
- Multi-language support

---

## 13. Implementation Checklist

### Day 1-2: Foundation
- [ ] Set up React Native project with TypeScript
- [ ] Implement navigation structure (3 screens)
- [ ] Create base component library
- [ ] Set up camera and gallery access
- [ ] Basic gesture system (swipes)

### Day 3-4: Core Features
- [ ] OCR integration with Google Vision
- [ ] Vibe selection logic
- [ ] LLM integration for recommendations
- [ ] Card swipe mechanics
- [ ] Local storage setup

### Day 5-6: Polish
- [ ] Animations and transitions
- [ ] Haptic feedback
- [ ] Error states and recovery
- [ ] Celebration moments
- [ ] Analytics instrumentation

### Day 7: Testing
- [ ] Device testing (iOS/Android)
- [ ] OCR accuracy validation
- [ ] Performance optimization
- [ ] Accessibility audit
- [ ] User testing with 10 participants

---

## Appendix A: Design Tokens

```javascript
export const tokens = {
  colors: {
    primary: '#FF6B6B',      // Coral
    secondary: '#A8E6CF',    // Mint
    accent: '#FFD93D',       // Gold
    background: '#FAFAF8',   // Warm white
    surface: '#F5F5F3',      // Soft gray
    text: {
      primary: '#2C3E50',
      secondary: '#7F8C8D',
      inverse: '#FFFFFF'
    },
    semantic: {
      success: '#4CAF50',
      error: '#F44336',
      warning: '#FF9800',
      info: '#2196F3'
    }
  },
  spacing: {
    xxs: 4,
    xs: 8,
    sm: 12,
    md: 16,
    lg: 24,
    xl: 32,
    xxl: 48,
    huge: 64
  },
  typography: {
    fontFamily: {
      display: 'Poppins',
      body: '-apple-system, BlinkMacSystemFont, "Segoe UI"'
    },
    sizes: {
      xxl: 32,  // Display
      xl: 24,   // Headers
      lg: 20,   // Subheaders
      md: 16,   // Body
      sm: 14,   // Caption
      xs: 12    // Micro
    }
  },
  shadows: {
    small: '0 2px 4px rgba(0,0,0,0.08)',
    medium: '0 4px 12px rgba(0,0,0,0.12)',
    large: '0 8px 24px rgba(0,0,0,0.16)',
    colored: '0 4px 12px rgba(255,107,107,0.3)'
  },
  radii: {
    small: 8,
    medium: 12,
    large: 16,
    xlarge: 20,
    round: 9999
  }
};
```

---

*This specification represents the consolidated, engineering-ready design for Aura Food MVP. It prioritizes clarity for international users, trust-building through transparency, and achievement of the 90-second promise.*