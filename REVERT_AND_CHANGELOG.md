# Portfolio Revert & Changelog Guide

This document records the design, animation, and structural modifications made to `dist/index.html` and provides step-by-step instructions to adjust or revert any specific feature.

---

## 1. Summary of Changes

### 🎬 1.1 Preloader: Expansive Full-Page 3D Video (6.5s) & Slide-Up Curtain Pull
- **Expansive Full-Page Canvas:** Sized up to `min(92vw, 920px)` with `mix-blend-mode: multiply` so the 3D character and wooden desk take up the full screen seamlessly on the white page.
- **6.5-Second Video & Percentage Sync:**
  - Progress percentage synchronizes over **6.5 seconds**, allowing the full animation sequence to finish naturally.
- **3.25-Second (50%) Name Slide-In From Left:**
  - `HARMAN PAPNEJA -26` on the bottom-left remains hidden for the first 3.25 seconds, then glides in smoothly from the left (`translateX(-54px)` -> `translateX(0)`).
- **500ms Hold at 100% & Slide-Up Curtain Exit:**
  - Holds at 100% for 500ms once the video completes, then slides the entire white curtain UP (`transform: translateY(-100%)`), revealing the Hero home page.

### 🎴 1.2 Hero Screen: Crystal-Clear Zero-Blur Scroll
- **Zero-Blur Scroll:** Text, 3D character, action buttons, and all 5 bottom stat pills remain 100% sharp and readable at all times as Page 2 overlaps over it like an elevated card.

### 🎴 1.3 Page 2 (About Section): Interactive Focus-Zoom Card Animation & Symmetrical Layout
- **Focus-Zoom Interactive Animation:**
  - When the cursor hovers over **any card/bracket** on Page 2 ("Not demos. Production systems."):
    - The **hovered card zooms IN / gets larger** (`transform: scale(1.065) translateY(-5px); z-index: 15;`) with an elevated 3D drop shadow and subtle crimson accent border.
    - All other non-hovered cards simultaneously **zoom OUT / scale down** (`transform: scale(0.95); opacity: 0.62; filter: blur(0.2px);`), creating a dynamic focus-spotlight animation.
- **Equal Margins & Height Balance:** Left column sidebar matches the exact height of the 6 capability cards on the right.
- **GrainLoop Side Project:** Framed cleanly as *⚡ Nights & Weekends R&D* while emphasizing full-time AI role availability.

### 🔴 1.4 "Work That Shipped" Timeline Automated Corner Dot Animation
- **Corner Fly-in:** Red indicator dots swoop in from the top-left corner (`@keyframes dotFlyIn`) with an elastic spring landing when scrolled into view.
- **Continuous Radar Ping:** Dots emit an automated pulsing radar ripple (`@keyframes dotRadarPing`).

### ✨ 1.5 Contact Page ("Open to the next hard problem")
- Original clean layout with ambient breathing watermark and responsive contact actions.

### 🤖 1.6 LangGraph Career Assistant Chatbot
- **Backend Architecture (`chatbot_server.py`):**
  - Built using **LangGraph `StateGraph`** with three connected nodes:
    1. `guardrail_router_node`: Inspects incoming query intent; routes career queries to `career_agent_node` and code/trivia/injection queries to `refusal_node`.
    2. `career_agent_node`: Grounded on verified resume data and portfolio metrics using Groq (`qwen/qwen3.8-27b`).
    3. `refusal_node`: Enforces standardized polite refusal without generating any code or off-topic information.
  - Endpoints: `POST /api/chat`, `GET /api/health` on port `8001`.
- **Frontend UI (`dist/index.html`):**
  - Bottom-right floating trigger pill with mascot avatar and live green pulse dot.
  - Glassmorphic modal window with quick prompt pills, typing indicator, auto-scroll, and markdown rendering.
- **Automated E2E Testing (`test_chatbot_e2e.py`):**
  - Full suite testing health check, production system metrics, education (9.48 CGPA), contact info, code-generation refusal, trivia refusal, injection defense, and multi-turn memory.

### 💬 1.7 High-Resolution Avatar & Recurring Speech Cloud Tooltip
- **Dedicated Crisp Avatar (`assets/character-avatar.jpg`):** Generated a 1:1 close-up headshot of the 3D character smiling with studio lighting, centered and rendered with high-definition clarity in the circular avatar badge.
- **Recurring Speech Cloud Tooltip (`#chatbotCloud`):**
  - Appears smoothly above the floating button every **10 seconds** for **3 seconds**, saying *"Ask Harman's professional experience!"* with subtle sparkle animation and bobbing float.
  - Auto-hides after 3 seconds and is suppressed when the chat window is active.
  - Clicking the cloud immediately opens the chatbot window.

### 💭 1.8 Preloader Speech Bubble Top-Right Corner Placement
- **Top-Right Alignment (`.pre-speech-bubble`):**
  - Repositioned the greeting bubble (*"👋 Hi, I am Harman, welcome to my portfolio!"*) to the **top-right corner** (`top: 14px; right: 28px;`) of the 3D character animation frame.
  - Custom slanted pointer tail (`left: 28px;`) pointing naturally toward the 3D character on the left.
  - Smooth vertical float micro-animation (`@keyframes bubbleFloatRight`).

### 📱 1.9 Mobile Skills Visibility & Responsive Optimization
- **Ambient Floating Orbital Chips on Mobile (`.orbit-chip`):**
  - Removed desktop-only mouse restriction (`display: none` in media query) so the skill badges around Harman's 3D character are **always active, glowing, and floating** on mobile devices.
  - Distinct mobile orbital layout (`@keyframes mobileOrbitBob`) with staggered animation timing and glassmorphic contrast.
- **Hero Mobile Skills Strip (`.hero-mobile-skills`):**
  - Added a responsive quick-access skill badge cluster below the action buttons (*⚡ LangGraph • 🧠 Agentic AI • 📊 RAG Systems • 🚀 FastAPI • 🛡️ Guardrails • 🗄️ Vector DBs • 🐍 Python / Pydantic*).
- **Responsive Stat Strip & Card Grids:**
  - Stat pills wrap gracefully without vertical bloat, and all capability cards, timelines, and skills groups stack with optimal mobile touch padding.

---

## 2. How to Revert or Adjust Specific Features

### How to adjust Page 2 Focus-Zoom Animation
In `dist/index.html` inside `<style>`, find `.about-pillars-grid:hover .cap-card` and `.about-pillars-grid .cap-card:hover`:
```css
/* Zoom-out value for other cards */
.about-pillars-grid:hover .cap-card {
  transform: scale(0.95);
  opacity: 0.62;
}

/* Zoom-in value for hovered card */
.about-pillars-grid .cap-card:hover {
  transform: scale(1.065) translateY(-5px);
}
```

---

### How to adjust Preloader Video Size
In `dist/index.html` inside `<style>`, find `.pre-character-wrap` and change `width: min(92vw, 920px);`:
- For medium size: `width: min(58vw, 560px);`
- For compact size: `width: min(44vw, 420px);`

---

### How to adjust Preloader Speed
In `dist/index.html` inside `<script>`, find `fallbackDuration = 6500;` and change `6500` to any millisecond value.
