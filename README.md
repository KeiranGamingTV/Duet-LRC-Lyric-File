# Duet-LRC-Lyric-File
A karaoke-style modified .LRC file that allows two or more singers to be notated and shown on lyrics screens for apps.

---

# Introduction
Standard LRC files are excellent for basic time-synchronized lyrics, but they inherently struggle with multi-singer tracks, duets, or choral arrangements. Developers and creators typically resort to clunky workarounds—like repeating timestamps, hardcoding names into text lines, or maintaining separate files.

**Duet LRC (.dlrc)** resolves this limitation by introducing a native, lightweight multi-singer notation directly beside standard timestamp structures. It remains backward-compatible with the foundational layout of traditional LRC, ensuring an incredibly low barrier to entry for developer adoption.

# Key Features & Design Philosophy
- **Native Singer Assignment:** Explicitly tag lines to individual vocalists or combined duets using explicit numerical identifiers.
- **Strict Predictability:** Every line follows a strict layout constraint, making parsing simple and deterministic.
- **Minimalist Syntax:** Keeps file sizes lightweight, clean, and highly human-readable.
- **Familiar Foundation:** Standard metadata fields are preserved, so legacy parsers can still extract song information.

---

# Core Guidelines & Rules
To ensure a .dlrc file parses perfectly, the format enforces the following strict rules:
1. **Mandatory Timestamps:** Every lyric line requires exactly one timestamp, just like a normal synced .lrc file.
2. **Mandatory Singer Notation:** Every lyric line must explicitly include either `{1}`, `{2`, or `{B}` immediately following the timestamp.
3. **No Multi-Timestamp Lines:** One lyric line cannot contain multiple timestamps (word-by-word mid-line syncing or repeating time tags on the same line are not supported).
4. **Metadata Support:** All standard metadata lines from traditional .lrc files (such as `[ar:]`, `[al:]`, `[ti:]`, and `[offset:]`) remain fully supported at the head of the file.

---

# File Syntax Layout
## Line-Level Singer Notation
To assign a line of lyrics, place the singer token bracket immediately following the timestamp bracket with no spaces, followed by the text of the lyric.
- `[mm:ss.xx]{1}` Indicates Singer 1 performs the line.
- `[mm:ss.xx]{2}` Indicates Singer 2 performs the line.
- `[mm:ss.xx]{B}` Indicates Both singers perform the line simultaneously.

---

# Comprehensive File Example (sample.dlrc)

```
[ti: Song Title]
[ar: Song Artist]
[al: Album Title]
[length: 3:35]

[00:10.15]{1} Singer 1 sings this line.
[00:15.40]{2} Singer 2 sings this line.
[00:20.80]{B} Both singers sing this line.
```

---

# Project Roadmap & Implementation Status
- **Specification Guidelines:** Complete and frozen for community evaluation.
- **App Implementation:** Successfully integrated into a custom, private offline music player app to prove parsing accuracy and operational proof of concept.
- **Upcoming Features:** I am planning to expand support to include distinct color coding identifiers soon to natively support tracks with more than two singers.
- **Parser/Reference Tooling:** In Development. I am currently looking for contributors to help build standalone open-source parser libraries in languages like JavaScript/TypeScript, Python, and Rust based on these strict guidelines.
