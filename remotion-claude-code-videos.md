# 🎬 Make Videos With Code Using Remotion + Claude Code

> **Traditional video editor:** *opens Premiere Pro, waits 4 minutes to load*
> **You:** *already rendered your video*

What if you could make a polished, animated product video — synchronized music, transitions, custom branding — just by writing (or asking Claude to write) TypeScript?

That's Remotion. And with Claude Code driving it, you're basically a one-person motion graphics studio.

---

## 🤔 What Even Is Remotion?

Remotion = **React for video.**

Instead of dragging clips on a timeline, you write React components. Each component describes what's on screen at a given frame. Remotion renders those frames into an MP4.

```
React Component → Frame-by-Frame Renderer → MP4 File
```

**Why this beats AI video generators:**
- ✅ Pixel-perfect control
- ✅ Editable — change a variable, re-render
- ✅ Scriptable — generate 1000 variations from one template
- ❌ No "AI hallucinated a 6-fingered hand in my promo video"

**Real companies using it:** GitHub, SoundCloud, Musixmatch, Wistia

---

## ⚡ The Claude Code Superpower

Normal Remotion workflow: read 800 pages of docs, learn interpolation math, debug frame timing.

**With Claude Code:** describe what you want, get working video code in minutes.

```
You: "Make a 30-second product launch video with fade-in title, 
      animated stats counter, and smooth slide transitions"

Claude Code: *writes the whole thing*

You: *renders video*
```

---

## 📋 Prerequisites

| Tool | Why You Need It |
|------|----------------|
| Node.js 16+ | Remotion runs on it |
| Claude Code | The AI that writes your video code |
| A terminal | You live here now |

---

## 🚀 Setup in 60 Seconds

```bash
# Create new Remotion project
npx create-video@latest

# Follow the prompts — pick "Blank" to start fresh
# OR pick a template if you want a head start

cd my-video
npm install
npm run dev
```

Remotion Studio opens in your browser. This is your preview window — changes in code show up here in real time.

---

## 🧱 Core Concepts (The Only Ones You Actually Need)

### 1. Compositions — Your Video Blueprint

Every video starts with a composition. Think of it as the "canvas settings":

```tsx
// src/Root.tsx
import { Composition } from 'remotion';
import { MyVideo } from './MyVideo';

export const RemotionRoot = () => {
  return (
    <Composition
      id="MyVideo"
      component={MyVideo}
      durationInFrames={300}  // 10 seconds at 30fps
      fps={30}
      width={1920}
      height={1080}
    />
  );
};
```

### 2. `useCurrentFrame` — The Magic Hook

This is what makes everything animate. It returns the current frame number (0 to durationInFrames - 1):

```tsx
import { useCurrentFrame } from 'remotion';

export const MyVideo = () => {
  const frame = useCurrentFrame(); // 0, 1, 2, 3...

  return <div>Frame: {frame}</div>;
};
```

### 3. `interpolate` — Smooth Everything Out

Map frame numbers to any value range. This is how you create animations:

```tsx
import { useCurrentFrame, interpolate } from 'remotion';

export const FadeIn = () => {
  const frame = useCurrentFrame();

  // Fade from 0 to 1 over first 30 frames (1 second)
  const opacity = interpolate(frame, [0, 30], [0, 1], {
    extrapolateRight: 'clamp',
  });

  return <div style={{ opacity }}>Hello World</div>;
};
```

### 4. `spring` — Physics-Based Motion

Makes things feel alive instead of robotic:

```tsx
import { useCurrentFrame, useVideoConfig, spring } from 'remotion';

export const PopIn = () => {
  const frame = useCurrentFrame();
  const { fps } = useVideoConfig();

  const scale = spring({
    fps,
    frame,
    config: { damping: 10, stiffness: 100 },
  });

  return (
    <div style={{ transform: `scale(${scale})` }}>
      🚀 Launch!
    </div>
  );
};
```

### 5. `<Sequence>` — Timeline Control

Start things at specific times without math:

```tsx
import { Sequence } from 'remotion';

export const MyVideo = () => {
  return (
    <>
      {/* Starts at frame 0, runs for 60 frames */}
      <Sequence from={0} durationInFrames={60}>
        <Intro />
      </Sequence>

      {/* Starts at frame 60 */}
      <Sequence from={60} durationInFrames={90}>
        <MainContent />
      </Sequence>

      {/* Starts at frame 150 */}
      <Sequence from={150}>
        <Outro />
      </Sequence>
    </>
  );
};
```

### 6. `<AbsoluteFill>` — Full Canvas Layer

Fills the entire video canvas. Great for backgrounds and overlays:

```tsx
import { AbsoluteFill } from 'remotion';

export const Background = () => (
  <AbsoluteFill style={{ backgroundColor: '#0f0f0f' }}>
    {/* everything inside fills the screen */}
  </AbsoluteFill>
);
```

---

## 🤝 Claude Code Workflow (The Actual Power Move)

### Give Claude a video brief, not a code request

❌ "Write interpolate code for text animation"

✅ "Make a 15-second animated intro: dark background, company name slides in from left with spring animation at frame 0, tagline fades in at frame 45, then both elements scale up and fade out at frame 120"

Claude knows Remotion. Give it the creative brief and let it handle the implementation.

### Prompt templates that work:

**Product launch video:**
```
Create a Remotion component for a 30-second product launch video.
- 0-2s: Logo fade in with spring animation
- 2-6s: Product screenshot slides in from right
- 6-12s: 3 feature points appear one by one (stagger by 20 frames each)
- 12-28s: Demo screen recording plays (placeholder)
- 28-30s: CTA text + website URL fade in
Colors: #6366f1 (primary), white text, dark background
```

**Social media clip:**
```
Create a Remotion composition for a 15-second Instagram Reel (1080x1920):
- Animated text counter (0 → 10,000) over 8 seconds
- Background: gradient from #667eea to #764ba2
- Large bold number centered, label text below
- "Follow for more" slides up at frame 380
```

**Data visualization:**
```
Remotion component: animated bar chart
- 5 bars representing monthly revenue
- Bars grow from 0 to target height over 60 frames
- Stagger start times by 10 frames each
- Label and value appear above each bar when it reaches full height
```

---

## 🎬 Rendering Your Video

```bash
# Preview in browser (instant, use during development)
npm run dev

# Render to MP4 (the real deal)
npx remotion render src/index.ts MyVideo out/video.mp4

# Render with specific resolution
npx remotion render src/index.ts MyVideo out/video.mp4 --width=1920 --height=1080

# Render a still (great for thumbnails)
npx remotion still src/index.ts MyVideo out/thumbnail.png --frame=60
```

---

## 📐 Common Video Sizes

| Platform | Width | Height | FPS |
|----------|-------|--------|-----|
| YouTube / Landscape | 1920 | 1080 | 30 |
| Instagram Reel / TikTok | 1080 | 1920 | 30 |
| Instagram Square | 1080 | 1080 | 30 |
| Twitter / X | 1280 | 720 | 30 |
| LinkedIn | 1920 | 1080 | 30 |

Quick frame math:
```
frames = seconds × fps
30 seconds at 30fps = 900 frames
15 seconds at 30fps = 450 frames
```

---

## 🔥 Pro Tips

**1. Build sections as separate components**
Don't put everything in one file. `<Intro />`, `<MainSection />`, `<Outro />` — compose them with `<Sequence>`.

**2. Use props for variations**
```tsx
// Render 100 personalized videos by changing props
<Composition
  id="PersonalizedVideo"
  component={PersonalizedVideo}
  defaultProps={{ name: "World", accentColor: "#6366f1" }}
  ...
/>
```
Then render with: `npx remotion render ... --props='{"name":"Alice"}'`

**3. `extrapolateRight: 'clamp'`**
Always add this to `interpolate` calls unless you want your animation values going infinite.

**4. Frame = 0 is the first frame**
Obvious but easy to mess up when timing sequences. Last frame = `durationInFrames - 1`.

**5. Let Claude debug too**
If animation timing feels off, paste your component and say:
"The text appears too early and the fade-out overlaps with the next scene. Fix the Sequence from/durationInFrames values."

---

## 🚨 Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| Blank preview | Component not registered in Root.tsx | Add `<Composition>` in Root.tsx |
| Animation jumps | Missing `extrapolateRight: 'clamp'` | Add clamp to interpolate options |
| Video too short | Wrong `durationInFrames` | `seconds × fps = frames` |
| Sequence not showing | `from` frame > total duration | Check sequence timing math |
| Render hangs | Heavy component, no memoization | Wrap expensive calcs in `useMemo` |

---

## 🎯 Quick Reference Card

```
┌───────────────────────────────────────────────────┐
│         REMOTION + CLAUDE CODE CHEAT SHEET         │
├───────────────────────────────────────────────────┤
│  SETUP:                                            │
│  npx create-video@latest → npm run dev             │
├───────────────────────────────────────────────────┤
│  CORE HOOKS:                                       │
│  useCurrentFrame()     → current frame number      │
│  useVideoConfig()      → fps, width, height        │
│  interpolate(f,[a,b],[x,y]) → map frame to value   │
│  spring({fps, frame})  → physics animation         │
├───────────────────────────────────────────────────┤
│  CORE COMPONENTS:                                  │
│  <Composition>         → register your video       │
│  <AbsoluteFill>        → fullscreen layer           │
│  <Sequence from={60}>  → start at frame 60         │
├───────────────────────────────────────────────────┤
│  RENDER:                                           │
│  npx remotion render src/index.ts MyVideo out.mp4  │
├───────────────────────────────────────────────────┤
│  FRAME MATH:                                       │
│  frames = seconds × fps (usually 30)               │
└───────────────────────────────────────────────────┘
```

---

## 💬 Final Thoughts

The combo of Remotion + Claude Code basically eliminates the "I'm not a motion designer" excuse.

You describe what you want. Claude writes the components. Remotion renders the video. You ship.

For social content, product demos, personalized videos at scale — this workflow is genuinely faster than any traditional video tool.

**The 10-minute product launch video is real. Go make one.**

---

*Found this helpful? Drop a ⭐ and share with your dev friends who are still exporting from Canva.*

**→ More guides:** [arpitvaish/claude-cheat-sheet](https://github.com/arpitvaish/claude-cheat-sheet)
**→ Remotion docs:** remotion.dev/docs
