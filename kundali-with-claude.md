# 🔮 Get Your Kundali Reading Using Claude (No Libraries Needed)

> **You:** "Can Claude read my kundali?"
> **Claude:** "Give me your birth details. I got this. 🪐"

Vedic astrology. Planetary positions. Doshas. Dashas. Sounds like you need a special app or a pandit on speed dial.

You don't. Just use **claude.ai** — it has web tools enabled, so it can look up real ephemeris data and calculate your chart accurately. Two prompts. That's the whole thing.

> ⚠️ **Use claude.ai (not the raw API).** claude.ai has web search and tools enabled — that's what lets it calculate accurate planetary positions. Without tools, Claude has no access to live ephemeris data and the chart will be wrong.

---

## 🧠 How It Works

```
Step 1: Claude calculates your birth chart (claude.ai with tools)
           ↓
Step 2: Claude interprets it as a Vedic astrologer
           ↓
        Full kundali reading ✨
```

No libraries. No apps. No code. Just two prompts on claude.ai.

---

## 📋 What You Need

- Your **birth date** (day, month, year)
- Your **birth time** (as accurate as possible — even approximate helps)
- Your **birth city**

That's it.

> ⚠️ **Birth time matters a lot.** Even 30 minutes off can shift your Lagna (ascendant). If you don't know the exact time, use your best guess and mention it to Claude.

---

## 🎯 Step 1 — Ask Claude to Calculate Your Chart

Use this prompt on **claude.ai**:

```
You are an expert Vedic astrologer. Using Jyotish principles with Lahiri ayanamsa (sidereal zodiac), calculate the birth chart for:

Name: [Your Name]
Date of Birth: [DD/MM/YYYY]
Time of Birth: [HH:MM, 24-hour format]
Place of Birth: [City, Country]

Please output the following as structured data:
- Ascendant (Lagna): sign and degree
- All 9 grahas (Sun, Moon, Mars, Mercury, Jupiter, Venus, Saturn, Rahu, Ketu): sign, house, and degree
- Which planets are exalted, debilitated, or in own sign
- Any major yogas present (Raj Yoga, Dhana Yoga, etc.)
- Any doshas present (Mangal Dosha, Kaal Sarp Yog, etc.)

Output this as a clean chart summary before any interpretation.
```

---

## 🔮 Step 2 — Ask Claude to Interpret It

Once Claude outputs the chart, follow up with:

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

## ⚡ One-Shot Mega Prompt (If You Want Everything at Once)

Don't want two steps? Combine them:

```
You are an expert Vedic astrologer. Using Jyotish principles with Lahiri ayanamsa (sidereal zodiac), do the following for this person:

Name: [Your Name]
Date of Birth: [DD/MM/YYYY]
Time of Birth: [HH:MM]
Place of Birth: [City, Country]

First, calculate and show the birth chart — Lagna, all 9 grahas with signs and houses, exaltations/debilitations, yogas, and doshas.

Then give a full kundali reading covering:
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
│  Use: claude.ai (tools enabled = accurate chart) │
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

It's genuinely good. Two things that matter most:

1. **Use claude.ai** — not the raw API. The web tools are what make the chart calculation accurate.
2. **Always say Lahiri ayanamsa + sidereal zodiac** — without that, Claude defaults to Western tropical astrology, which gives completely different signs and houses.

Two lines. Huge difference.

---

*Found this helpful? Drop a ⭐ on the repo.*

**→ More guides:** [arpitvaish/claude-cheat-sheet](https://github.com/arpitvaish/claude-cheat-sheet)
