# NutriLens AI 🥗
**See food differently.**

AI-powered nutrition tracking app built for India — scan any food, get instant insights tailored to your health goals.

🔗 **[Try it live](https://appetize.io/app/b_3jzdfw7qtgzhgjofjz4txabdqq)** — runs in your browser, no install needed

## 📱 Screenshots

<p align="center">
  <img src="screenshots/screenshot_2.jpeg" width="30%" />
  <img src="screenshots/screenshot_3.jpeg" width="30%" />
  <img src="screenshots/screenshot_5.jpeg" width="30%" />
</p>
<p align="center">
  <img src="screenshots/screenshot_6.jpeg" width="30%" />
  <img src="screenshots/screenshot_7.jpeg" width="30%" />
  <img src="screenshots/screenshot_8.jpeg" width="30%" />
</p>

## The problem

Most nutrition trackers assume the world eats packaged, barcoded, single-ingredient food — scan a barcode, get the label. That model breaks down for home-cooked and mixed meals, which is most of what people in India actually eat. The alternative most apps fall back on is manual search-and-log, which is slow enough that people quit within days. On top of that, a single "calories in" number rarely means the same thing to two different people — someone cutting weight and someone trying to gain muscle need the same plate scored differently.

## Who it's for

- **Primary:** People in India trying to build a consistent nutrition-tracking habit around home-cooked and mixed meals, without wrestling with a barcode-first database.
- **Secondary:** People with a specific health goal (weight loss, muscle gain, general health) who want the same food scored differently depending on that goal.
- **Explicitly not for:** People who need lab-grade macro precision (competitive athletes, clinical nutrition management) — camera-based AI estimation trades precision for speed, and this app is built for the speed side of that trade.

## The key decision

The bet: **a camera pointed at a plate is faster and more honest than a search bar**, especially for food that was never going to have a barcode in the first place. If logging a meal takes 10 seconds instead of 90, more meals actually get logged — and a tracker only creates value from meals it actually sees.

## The trade-off

The hard choice was going camera-first (Gemini 2.5 Flash vision) instead of a barcode/database-driven approach like MyFitnessPal. The alternative rejected: a large packaged-food barcode database, which is more precise for branded items but does nothing for a home-cooked thali.

What that cost: AI estimation is inherently less precise than a verified nutrition label, every scan depends on a network call (no offline logging), and mixed or visually ambiguous dishes carry real misidentification risk that a barcode scan would never have.

## What's in v1

- 📸 AI food scanner — instant nutrition breakdown via Gemini 2.5 Flash
- 🎯 Goal-based scoring — same food, different score based on your goal
- 🤖 NutriBot chat — ask anything, get personalized AI responses
- 📊 Insights dashboard — daily macros, trends, meal history
- ⚖️ Weight tracker — log and visualize progress
- 💧 Water & steps — built-in hydration and activity tracking
- 🏆 Achievements — gamified milestones

## What's deliberately not in v1

- **Barcode scanning** — deliberately skipped; it solves a problem (packaged food) that camera-based recognition already handles well enough, and adding both paths in v1 would split focus without a proven need yet.
- **Social features / community feed** — cut to avoid turning a personal tracking tool into a content platform before the core scanning loop is proven.
- **Wearable integration** — no Google Fit / wearable sync yet; steps and water are logged manually for now.
- **Offline mode** — every scan needs the Gemini API, so there's no offline fallback; accepted as a v1 constraint of the camera-first bet.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Kotlin |
| UI | Jetpack Compose |
| Camera | CameraX |
| AI | Gemini 2.5 Flash |
| Database | Room v3 |
| Architecture | MVVM |

## Setup

Add your Gemini API key to `local.properties`.

## How I would measure it

**North star: % of users who log at least one food scan per day, 7 days after signup.** The entire product bet is that camera-first logging is fast enough to become a daily habit — if that's not happening, the core hypothesis is wrong, not just a rough edge.

Supporting metrics:

- **Scan-to-log conversion rate** — what fraction of AI scans actually get saved as a logged meal vs. discarded. A low rate would mean the AI's estimates aren't trusted enough to act on.
- **Edit rate on AI-identified nutrition** — how often users manually correct what the AI detected. A rough proxy for recognition accuracy on real-world (especially mixed/Indian) meals.
- **7-day retention** — since the whole value proposition compounds over repeated daily use, not a single session.

## Known limits

An honest list of what's missing or unverified:

- AI food recognition accuracy on mixed or regional dishes hasn't been formally benchmarked — it's evaluated by hands-on use, not a measured accuracy rate.
- No offline mode — every scan requires network access and a live Gemini API call.
- No wearable/Google Fit integration — steps and water are self-reported.
- No automated tests.

## Development note

This project was built using AI-assisted development with [Claude Code](https://claude.com/claude-code), Anthropic's agentic coding tool.
