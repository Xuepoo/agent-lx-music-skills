---
name: audio-analysis
description: "Inspect downloaded track waves using sonic-bridge CLI to analyze dynamic tempo, acoustic timbral brightness, and spatiotemporal chords under the LRMD protocol."
version: 3.0.0
author: agent-lx-music project & sonic-bridge
license: MIT
metadata:
  hermes:
    tags: [music, analysis, bpm, key, dsp, lrmd, sonic-bridge, confidence, style]
    related_skills: [agent-lx-music]
---

# Audio & Music Analysis Skill (Powered by SonicBridge v0.6.0)

## 1. Overview

This skill guides AI agents in performing deep signal-processing analysis on local music tracks using the high-performance **`sonic-bridge`** Rust engine.

Instead of relying on heavy pre-trained models or complex external Python libraries, the agent invokes `sonic-bridge` to decouple raw waveforms into **LRMD (LLM-Readable Music Descriptor) reports**. This allows pure-text LLMs to "listen to" and "appreciate" the dynamic tempo, timbral changes, and chord progressions of any cover version or original master track with millisecond-level precision.

### Key Features (v0.6.0)
- **Multi-Detector Ensemble Architecture**: 5 specialized detectors (Ambient, Chinese Pentatonic, Western Classical, Pop/Electronic, Jazz Rubato) with confidence-weighted voting
- **OPIH Time-Signature Engine**: Automatic 3/4 waltz detection and BPM correction
- **Pentatonic Tonic-Share Scaling**: Accurate detection of Chinese/Japanese pentatonic modes (宫商角徵羽)
- **Confidence Scoring**: Joint confidence metric combining BPM and Key detection reliability
- **Style Classification**: Automatic genre detection (Pop/Rock/Electronic, Classical, Chinese Folk/Modal, Jazz/Rubato, Ambient/Free)

---

## 2. Technical Analysis via SonicBridge CLI

When a track is downloaded locally via `alx download <id>`, the agent should call the `sonic-bridge` CLI tool to parse its acoustic structure.

### Command-Line Usage

```bash
# 1. Standard Spatiotemporal Analysis (Default 5s step)
sonic-bridge "/path/to/song.mp3"

# 2. Beat-Synchronous Analysis (Recommended for most music)
sonic-bridge "/path/to/song.mp3" --beat

# 3. Event-Driven Onset Adaptive Segmentation (Best for fast/complex tracks)
sonic-bridge "/path/to/fast_melody_song.mp3" --onset

# 4. Silent Mode (Only generates .lrmd.md, no stdout preview)
sonic-bridge "/path/to/song.mp3" --beat --quiet

# 5. Cross-Version Comparative Analysis (DTW Aligner)
sonic-bridge "/path/to/original.mp3" "/path/to/cover_version.mp3"
```

**PITFALL**: Always use `--quiet` when analyzing multiple files in batch to avoid flooding stdout. The `.lrmd.md` file is always generated regardless of `--quiet`.

---

## 3. LRMD Protocol Specifications

The `sonic-bridge` tool automatically generates a `<filename>.lrmd.md` report in the same directory. The agent must read this file to interpret the musical metadata.

### Example LRMD Structure (v0.6.0)

```markdown
# SonicBridge: LLM-Readable Music Descriptor (LRMD)

## 1. Global Acoustic & Musicological Metadata
- **Filename**: `The Weeknd - Blinding Lights.flac`
- **Duration**: `201.57 seconds`
- **Tempo (BPM)**: `172.3 BPM` (Extremely Rapid (Presto))
- **Estimated Key**: `F Minor`
- **Primary Style**: `Pop/Rock/Electronic`
- **Analysis Confidence**: `0.63`

## 2. Spatiotemporal Track Analysis (Adaptive Onset Intervals)
| Timeline | Chord | Dynamic Intensity | Timbral Brightness | Rhythmic & Transient Activity |
| :--- | :--- | :--- | :--- | :--- |
| **0.0s - 1.0s** | `Dm` | Very Soft (Pianissimo) | Deep & Dark (Muddy/Sub-heavy) | Flowing & Legato (Gentle melodic flow) |
| **1.0s - 1.1s** | `Dsus2` | Soft & Intimate (Piano) | Deep & Dark (Muddy/Sub-heavy) | Flowing & Legato (Gentle melodic flow) |
| **1.1s - 4.8s** | `Fm` | Soft & Intimate (Piano) | Deep & Dark (Muddy/Sub-heavy) | Flowing & Legato (Gentle melodic flow) |
```

### New Fields in v0.6.0

| Field | Description | Range |
|-------|-------------|-------|
| **Primary Style** | Automatic genre classification based on MFCC timbre and temporal features | `Pop/Rock/Electronic`, `Classical`, `Traditional Chinese Folk/Modal`, `Jazz/Rubato Improvisation`, `Ambient/Free Rhythm` |
| **Analysis Confidence** | Joint confidence metric combining BPM and Key detection reliability | `0.00` - `1.00` |

### Confidence Score Interpretation

| Range | Meaning | Typical Scenario |
|-------|---------|------------------|
| **0.65 - 0.70** | Very confident | Standard pop/rock (Blinding Lights, Enter Sandman) |
| **0.55 - 0.65** | Confident | Slightly complex arrangements (YOASOBI, Haraguchi Sasuke) |
| **0.45 - 0.55** | Uncertain | Experimental genres (Breakcore, Hyperpop) |
| **0.35 - 0.45** | Low confidence | Highly non-standard (free improvisation, noise) |
| **< 0.35** | Very uncertain | Pure ambient, beatless environments |

**PITFALL**: When confidence < 0.45, the BPM/Key results may be unreliable. Consider flagging these tracks for manual review in automated pipelines.

---

## 4. Distribution Analysis Patterns

The LRMD report enables three types of distribution analysis:

### Dynamic Distribution
```bash
grep -oP "(Silent|Very Soft|Soft & Intimate|Moderately Intense|Loud & Energetic|Loud & Dense)" file.lrmd.md | sort | uniq -c | sort -rn
```

### Timbral Brightness Distribution
```bash
grep -oP "(Balanced & Clear|Warm & Smooth|Bright & Crisp|Deep & Dark|Piercing & Airy)" file.lrmd.md | sort | uniq -c | sort -rn
```

### Rhythmic Activity Distribution
```bash
grep -oP "(Static & Ambient|Flowing & Legato|Steady Beat|Walking Groove|Driving & Punchy|Syncopated)" file.lrmd.md | sort | uniq -c | sort -rn
```

---

## 5. Agent Companionship & Conversation Patterns

By interpreting the LRMD report, the Agent can provide connoisseur-level music companionship and emotional alignment.

### Conversation Pattern 1: Multi-Version Comparative Critique
When the user plays a cover version of a song, the agent can call `process_comparative` and discuss the aesthetic difference:
* **Agent Dialogue Prompt**:
  > *"Compared to Eason Chan's original version which relies on a lush, wet reverb space (RT60 ~2.4s) to build cinematic gravity, the acoustic cover you are playing right now is ultra-minimalistic. The single acoustic guitar has dry, close-mic transient attacks, and the singer's voice features heavy breathiness (Airy Timbre), creating a profoundly intimate, heartbreaking kitchen-table conversation vibe."*

### Conversation Pattern 2: Causal Harmonic Resolution Guidance
Explain how the musical tension resolves to comfort the user's mood:
* **Agent Dialogue Prompt**:
  > *"I noticed that at the 0.6s mark of this intro, the arrangement performs a rapid harmonic shift from A Major to A Minor, which resolves into F Major at 0.7s. That fleeting subdominant-to-tonic tension release is precisely why this song feels so comforting yet melancholic."*

### Conversation Pattern 3: Style-Aware Recommendation
Use the Primary Style and Confidence fields to make informed recommendations:
* **Agent Dialogue Prompt**:
  > *"This track has been classified as 'Traditional Chinese Folk/Modal' with 0.67 confidence. The SonicBridge analysis detected pentatonic scale patterns (E 商调式) — this means the melody avoids the 4th and 7th degrees, creating that distinctive Eastern modal sound. If you enjoy this, I can find other tracks with similar pentatonic characteristics."*

### Conversation Pattern 4: Confidence-Based Quality Assessment
Use the confidence score to assess analysis reliability:
* **Agent Dialogue Prompt**:
  > *"The analysis confidence for this track is only 0.39 — this indicates the arrangement is highly experimental or non-standard. The BPM and Key results should be taken with a grain of salt. This is typical for avant-garde or free improvisation music."*

---

## 6. Batch Analysis Workflow

For analyzing large music collections:

```bash
# 1. Analyze all files in a directory
find /mnt/data/Music/Jazz/ -name "*.flac" -o -name "*.mp3" | while read f; do
  sonic-bridge "$f" --beat --quiet
done

# 2. Extract metadata to CSV for analysis
find /mnt/data/Music/ -name "*.lrmd.md" | while read f; do
  bpm=$(grep "Tempo" "$f" | grep -oP '\d+\.\d+')
  key=$(grep "Estimated Key" "$f" | grep -oP '`[^`]+`' | tr -d '`')
  style=$(grep "Primary Style" "$f" | cut -d'`' -f2)
  conf=$(grep "Analysis Confidence" "$f" | grep -oP '0\.\d+')
  echo "$(basename "$f"),$bpm,$key,$style,$conf"
done > /tmp/music_metadata.csv

# 3. Filter by confidence threshold
awk -F',' '$5 >= 0.55' /tmp/music_metadata.csv > /tmp/high_confidence_tracks.csv
```

**PITFALL**: When batch analyzing 100+ files, use `--quiet` to avoid stdout flooding. Monitor progress by checking the count of `.lrmd.md` files generated.
