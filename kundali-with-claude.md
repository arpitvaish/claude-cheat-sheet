# 🔮 Get Your Kundali Reading Using Claude (No Libraries Needed)

> **You:** "Can Claude read my kundali?"
> **Claude:** "Paste your chart data and watch me go 🪐"

Vedic astrology. Planetary positions. Doshas. Dashas. Sounds like you need a special app or a pandit on speed dial.

For interpretation? You don't. Claude is excellent at reading a kundali.
For *calculation*? You do need a tool. Claude cannot reliably compute planetary positions from birth details — it doesn't have access to a live ephemeris, so degrees and house placements come out wrong.

> ⚠️ **Important:** Do NOT ask Claude to calculate your birth chart from scratch. It will give you incorrect planetary positions. Always generate the chart using a dedicated tool first, then bring it to Claude for interpretation.

The workflow that actually works: **generate chart → paste to Claude → get reading.**

---

## 🧠 How It Works

```
Step 1: Generate your chart on AstroSage / Jagannatha Hora (free)
           ↓
Step 2: Paste chart data into Claude
           ↓
Step 3: Claude interprets it as a Vedic astrologer
           ↓
        Full kundali reading ✨
```

No paid apps. No astrologer subscription. Claude does the hard interpretive work — you just need the raw chart data first.

---

## 📋 What You Need

- Your **birth date** (day, month, year)
- Your **birth time** (as accurate as possible — even approximate helps)
- Your **birth city**

That's it.

> ⚠️ **Birth time matters a lot.** Even 30 minutes off can shift your Lagna (ascendant). If you don't know the exact time, use your best guess and mention it to Claude.

---

## 🎯 Step 1 — Generate Your Chart (Takes 2 Minutes)

Claude cannot calculate planetary positions accurately — it lacks a live ephemeris. Use one of these free tools:

| Tool | Link | Notes |
|------|------|-------|
| **AstroSage** | astrosage.com/free-kundli | Online, Lahiri default, easiest |
| **Jagannatha Hora** | free desktop software | Most accurate, used by serious astrologers |
| **AstroVed** | astroved.com | Online, good UI |

**Settings to use:**
- Ayanamsa: **Lahiri** (also called Chitrapaksha)
- Chart style: **North Indian** or **South Indian** — doesn't matter, just copy the data

Once generated, copy the planet positions (sign + house for each graha).

---

## 🔮 Step 2 — Paste Chart to Claude and Ask for Interpretation

Once you have your chart data from AstroSage/Jagannatha Hora, paste it and use this prompt:

```
Now give me a full Vedic kundali reading based on this chart. Cover:

1. Lagna (Ascendant) — personality, appearance, how I approach life
2. Moon Sign (Rashi) — emotions, mind, instincts
3. Sun Sign — soul purpose, ego, father
4. Career & Purpose — 10th house, strongest planets
5. Relationships & Marriage — 7th house, Venus placement
6. Wealth & Prosperity — 2nd and 11th house
7. Doshas — any present and what they mean practically
8. Current Life Phase — which Mahadasha/Antardasha I'm likely in
9. Strengths to lean into
10. Practical remedies for weak or afflicted planets

Be specific to my chart. Use Sanskrit terms but explain them simply.
```

---

## 💬 Then Just Ask Anything

After the reading, Claude remembers your chart in the same conversation. Ask freely:

- *"Is this a good year for me to change jobs?"*
- *"What does my 8th house tell you about transformation in my life?"*
- *"Which gemstone suits me and why?"*
- *"When is a good time window for marriage based on my dashas?"*
- *"Why do I always struggle with [X]? What in my chart explains it?"*

Claude will answer **from your specific chart** — not generic sun-sign astrology.

---

## ⚡ One-Shot Mega Prompt (Paste Chart + Get Full Reading)

Have your chart data ready from AstroSage/Jagannatha Hora? Use this single prompt:

```
You are an expert Vedic astrologer. Here is my birth chart (generated using Lahiri ayanamsa):

[Paste your chart data here — Lagna, all graha positions with signs and houses]

Give me a full kundali reading covering:
1. Lagna analysis
2. Moon sign and emotional nature
3. Career and purpose (10th house)
4. Relationships and marriage (7th house)
5. Wealth indicators
6. Doshas and their real-world effects
7. Current Mahadasha/Antardasha and what it means for this phase of life
8. Key strengths and challenges
9. Practical remedies

Be specific to this chart. Use Sanskrit terms with simple explanations.
```

---

## 🎯 Quick Reference Card

```
┌──────────────────────────────────────────────────┐
│      KUNDALI WITH CLAUDE — CHEAT SHEET           │
├──────────────────────────────────────────────────┤
│  Need: Date + Time + City of birth               │
│  Ayanamsa: Lahiri (always specify this)          │
│  Zodiac: Sidereal (not tropical/Western)         │
├──────────────────────────────────────────────────┤
│  PROMPT ORDER:                                   │
│  1. Ask Claude to calculate the chart            │
│  2. Ask Claude to interpret it                   │
│  3. Ask follow-up questions freely               │
├──────────────────────────────────────────────────┤
│  KEY TOPICS TO ASK ABOUT:                        │
│  Lagna, Rashi, Dashas, Doshas                    │
│  Career, Marriage, Wealth, Remedies              │
└──────────────────────────────────────────────────┘
```

---

## 💬 Final Thoughts

Claude isn't replacing your family pandit. But for understanding your own chart, exploring what the planets say about your life, or just satisfying that 2am curiosity?

It's genuinely good. The key is **always mentioning Lahiri ayanamsa and sidereal zodiac** — without that, Claude defaults to Western tropical astrology, which gives completely different signs and houses.

One line. Huge difference.

---

*Found this helpful? Drop a ⭐ on the repo.*

**→ More guides:** [arpitvaish/claude-cheat-sheet](https://github.com/arpitvaish/claude-cheat-sheet)
