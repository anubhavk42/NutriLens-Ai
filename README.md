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

Most people don't actually know what they're eating — whether that's a packaged product picked up while shopping or a home-cooked meal on their plate. That gap leads to worse choices: buying the wrong packaged product when a better one was sitting next to it, or eating something without realizing what it's doing to a specific health goal. The apps that already solve this exist, but they're priced high enough that the people who'd benefit most from casual, daily use often don't bother subscribing.

## Who it's for

- **Primary:** People in India who want to make better food decisions in the moment — while grocery shopping (packaged products) or while eating (home-cooked meals) — without paying premium prices for it.
- **Secondary:** People with a specific health goal (weight loss, muscle gain, general health) who want the same food scored differently depending on that goal.
- **Explicitly not for:** People who need lab-grade macro precision (competitive athletes, clinical nutrition management) — camera-based AI estimation trades precision for speed, and this app is built for the speed side of that trade.

## The key decision

The bet: **instant nutrition insight — for anything, packaged or home-cooked — is only valuable if it's cheap enough to use casually, every day, without a spending decision attached to it.** So the app is priced at roughly **half of what comparable nutrition-tracking apps charge**, on the belief that lowering the cost barrier matters as much as lowering the friction barrier. A tool this useful shouldn't be gated behind a premium subscription most people won't commit to.

## The trade-off

The hard choice was pricing at half of what competitors charge, instead of matching the market rate like every other nutrition-tracking app. The alternative rejected: price it like everyone else, protect margin from day one, and compete purely on features.

What that cost: it's a bet on volume over margin, made before the app has real usage data to confirm it works. Every scan still has a real, ongoing cost behind it, so pricing this low only pays off if enough people actually use it — if adoption stays small, the economics don't hold up as comfortably as they would at scale. It's an intentional bet, not a proven one yet.

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
