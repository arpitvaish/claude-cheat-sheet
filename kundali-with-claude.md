# 🔮 Get Your Kundali (Birth Chart) Using Claude API

> **You:** "Can Claude read my kundali?"
> **Claude:** "Give me your birth details and watch me go 🪐"

Vedic astrology. Planetary positions. Doshas. Dashas. Sounds complex — and it is.

But here's the thing: once you have the raw birth chart data, **Claude is surprisingly good at interpreting it**. This guide shows you how to build a script that calculates planetary positions from birth details and feeds them to Claude for a full Vedic kundali reading.

No astrologer subscription. No sketchy websites. Just Python + Claude API.

---

## 🧠 How This Works

```
Birth Details (date/time/place)
         ↓
   kerykeion (Python lib)
         ↓
  Planetary Positions + Houses
         ↓
      Claude API
         ↓
  Full Kundali Interpretation ✨
```

**kerykeion** is a free Python library that computes:
- Planetary positions (Lagna, Moon, Sun, all 9 grahas)
- House cusps (Rashi chart, Navamsa)
- Ascendant (Lagna)

**Claude** takes that raw data and interprets:
- Personality (Lagna + Moon sign)
- Life path, career, relationships
- Doshas (Mangal dosha, Kaal Sarp, etc.)
- Current Dasha/Antardasha
- Remedies and strengths

---

## 📋 Prerequisites

```bash
pip install kerykeion anthropic
```

You also need an **Anthropic API key** → get it at console.anthropic.com

---

## 🚀 The Script

Save as `kundali.py`:

```python
import anthropic
from kerykeion import AstrologicalSubject, KerykeionChartSVG
import json

def get_birth_chart(name: str, year: int, month: int, day: int,
                    hour: int, minute: int, city: str, nation: str) -> dict:
    """Calculate planetary positions using kerykeion."""
    subject = AstrologicalSubject(
        name=name,
        year=year,
        month=month,
        day=day,
        hour=hour,
        minute=minute,
        city=city,
        nation=nation,
        zodiac_type="Sidereal",   # Vedic uses sidereal, not tropical
        sidereal_mode="LAHIRI"    # Lahiri ayanamsa — standard in India
    )

    planets = {
        "Sun":     {"sign": subject.sun.sign,     "degree": round(subject.sun.abs_pos, 2),     "house": subject.sun.house},
        "Moon":    {"sign": subject.moon.sign,    "degree": round(subject.moon.abs_pos, 2),    "house": subject.moon.house},
        "Mercury": {"sign": subject.mercury.sign, "degree": round(subject.mercury.abs_pos, 2), "house": subject.mercury.house},
        "Venus":   {"sign": subject.venus.sign,   "degree": round(subject.venus.abs_pos, 2),   "house": subject.venus.house},
        "Mars":    {"sign": subject.mars.sign,    "degree": round(subject.mars.abs_pos, 2),    "house": subject.mars.house},
        "Jupiter": {"sign": subject.jupiter.sign, "degree": round(subject.jupiter.abs_pos, 2), "house": subject.jupiter.house},
        "Saturn":  {"sign": subject.saturn.sign,  "degree": round(subject.saturn.abs_pos, 2),  "house": subject.saturn.house},
        "Uranus":  {"sign": subject.uranus.sign,  "degree": round(subject.uranus.abs_pos, 2),  "house": subject.uranus.house},
        "Neptune": {"sign": subject.neptune.sign, "degree": round(subject.neptune.abs_pos, 2), "house": subject.neptune.house},
    }

    return {
        "name": name,
        "birth_details": f"{day}/{month}/{year} {hour:02d}:{minute:02d}, {city}, {nation}",
        "ascendant": {"sign": subject.first_house.sign, "degree": round(subject.first_house.abs_pos, 2)},
        "planets": planets,
        "houses": {
            f"House {i+1}": getattr(subject, f"{['first','second','third','fourth','fifth','sixth','seventh','eighth','ninth','tenth','eleventh','twelfth'][i]}_house").sign
            for i in range(12)
        }
    }


def get_kundali_reading(chart: dict) -> str:
    """Send birth chart to Claude for Vedic interpretation."""
    client = anthropic.Anthropic()

    prompt = f"""You are an expert Vedic astrologer with deep knowledge of Jyotish shastra.

Analyze this birth chart and provide a comprehensive kundali reading:

{json.dumps(chart, indent=2)}

Please provide:

1. **Lagna (Ascendant) Analysis** — personality, physical traits, life approach
2. **Moon Sign (Rashi)** — emotional nature, mind, mother relationship
3. **Sun Sign** — soul purpose, father, authority
4. **Key Planetary Positions** — highlight any exalted, debilitated, or strongly placed planets
5. **House Analysis** — focus on 1st, 4th, 7th, 10th (Kendra houses) and any occupied houses
6. **Dosha Check** — Mangal Dosha, Kaal Sarp Yog, Guru Chandal Yog (if present)
7. **Strengths & Challenges** — based on planetary dignity and aspects
8. **Career & Purpose** — 10th house, 6th house, strong planets
9. **Relationships** — 7th house lord and Venus placement
10. **Remedies** — practical Vedic remedies for weak or afflicted planets

Use Sanskrit terms where appropriate (Lagna, Rashi, Graha, etc.) but explain them clearly.
Be specific to this chart — not generic astrology copy-paste."""

    message = client.messages.create(
        model="claude-opus-4-8",
        max_tokens=4096,
        messages=[{"role": "user", "content": prompt}]
    )

    return message.content[0].text


def main():
    print("🔮 Kundali Generator with Claude\n")
    print("Enter birth details:")

    name   = input("Name: ")
    day    = int(input("Day (DD): "))
    month  = int(input("Month (MM): "))
    year   = int(input("Year (YYYY): "))
    hour   = int(input("Hour (24h format, e.g. 14 for 2pm): "))
    minute = int(input("Minute: "))
    city   = input("Birth city (e.g. Mumbai): ")
    nation = input("Country code (e.g. IN): ")

    print("\n⏳ Calculating birth chart...")
    chart = get_birth_chart(name, year, month, day, hour, minute, city, nation)

    print("\n📊 Birth Chart Summary:")
    print(f"  Ascendant (Lagna): {chart['ascendant']['sign']} ({chart['ascendant']['degree']}°)")
    print(f"  Moon: {chart['planets']['Moon']['sign']} in House {chart['planets']['Moon']['house']}")
    print(f"  Sun:  {chart['planets']['Sun']['sign']} in House {chart['planets']['Sun']['house']}")

    print("\n🪐 Sending to Claude for Vedic interpretation...\n")
    reading = get_kundali_reading(chart)

    print("=" * 60)
    print(reading)
    print("=" * 60)

    # Save to file
    output_file = f"kundali_{name.lower().replace(' ', '_')}.txt"
    with open(output_file, "w") as f:
        f.write(f"KUNDALI REPORT — {name}\n")
        f.write(f"Birth: {chart['birth_details']}\n")
        f.write("=" * 60 + "\n\n")
        f.write(reading)
    print(f"\n💾 Saved to {output_file}")


if __name__ == "__main__":
    main()
```

---

## ▶️ Run It

```bash
export ANTHROPIC_API_KEY="your-key-here"
python kundali.py
```

Sample input:
```
Name: Arjun Sharma
Day: 15
Month: 8
Year: 1990
Hour: 6
Minute: 30
Birth city: Delhi
Country code: IN
```

---

## 📊 Sample Output Structure

Claude will return something like:

```
1. LAGNA ANALYSIS
   Your Gemini ascendant (Mithuna Lagna) makes you...

2. MOON SIGN — Scorpio (Vrishchika)
   Moon in Scorpio in the 6th house indicates...

3. KEY PLANETARY POSITIONS
   ✅ Jupiter exalted in Cancer (4th house) — exceptional...
   ⚠️  Saturn in Aries (11th house) — delayed but...

4. MANGAL DOSHA
   Mars in 7th house confirms Mangal Dosha. Remedy...

...and so on for all 10 sections
```

---

## ⚡ Bonus: Ask Follow-up Questions

Want to dig deeper? Extend the script with a chat loop:

```python
def kundali_chat(chart: dict):
    """Interactive kundali Q&A with Claude."""
    client = anthropic.Anthropic()
    messages = []

    # Prime Claude with the chart
    system = f"""You are an expert Vedic astrologer. The user's birth chart is:
{json.dumps(chart, indent=2)}
Answer all questions strictly based on Vedic Jyotish principles using this chart."""

    print("\n💬 Ask Claude anything about your kundali (type 'quit' to exit)\n")

    while True:
        question = input("You: ").strip()
        if question.lower() in ("quit", "exit", "q"):
            break

        messages.append({"role": "user", "content": question})

        response = client.messages.create(
            model="claude-sonnet-4-6",   # Sonnet is fine for follow-ups (cheaper)
            max_tokens=1024,
            system=system,
            messages=messages
        )

        answer = response.content[0].text
        messages.append({"role": "assistant", "content": answer})

        print(f"\nClaude: {answer}\n")
```

Example questions you can ask:
- *"When will my career peak based on current dashas?"*
- *"Is this a good time to get married?"*
- *"What does my 8th house say about inheritance?"*
- *"Which gemstone should I wear?"*

---

## 🔧 Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| `City not found` | kerykeion needs exact city name | Try nearby major city |
| `AttributeError: house` | Older kerykeion version | `pip install --upgrade kerykeion` |
| `Invalid API key` | Wrong env var | Check `echo $ANTHROPIC_API_KEY` |
| Tropical signs showing | Wrong zodiac type | Ensure `zodiac_type="Sidereal"` and `sidereal_mode="LAHIRI"` |
| Generic reading | Prompt too vague | Use the full prompt in the script — don't shorten it |

---

## 🎯 Quick Reference Card

```
┌──────────────────────────────────────────────────┐
│         KUNDALI WITH CLAUDE — CHEAT SHEET        │
├──────────────────────────────────────────────────┤
│  Library:  kerykeion (planet positions)          │
│  Model:    claude-opus-4-8 (full reading)        │
│            claude-sonnet-4-6 (follow-ups)        │
│  Zodiac:   Sidereal + Lahiri ayanamsa            │
├──────────────────────────────────────────────────┤
│  KEY PARAMS:                                     │
│  zodiac_type = "Sidereal"   ← must for Vedic     │
│  sidereal_mode = "LAHIRI"   ← Indian standard    │
│  max_tokens = 4096          ← full reading       │
├──────────────────────────────────────────────────┤
│  ASK CLAUDE ABOUT:                               │
│  Lagna, Moon, Doshas, Dashas                     │
│  Career, Marriage, Remedies                      │
└──────────────────────────────────────────────────┘
```

---

## 💬 Final Thoughts

This isn't replacing your family pandit. But for a first-pass reading, exploring your chart, or understanding what all those planetary positions mean?

Claude is genuinely impressive here. Feed it a well-structured chart with the right prompt and it gives you **specific, chart-aware interpretations** — not the copy-paste horoscope garbage you find online.

The Lahiri + Sidereal combo is what makes this **actually Vedic**, not just Western astrology in disguise. That one setting change matters more than anything else in this guide.

---

*Found this helpful? Drop a ⭐ on the repo.*

**→ More guides:** [arpitvaish/claude-cheat-sheet](https://github.com/arpitvaish/claude-cheat-sheet)
