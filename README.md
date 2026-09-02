# 🌳 Word Tree Generator

AI level generator for **Word Tree: Associations** — a single-file static web tool, no build step.

An AI engine generates the word-association tree content; the tool deterministically computes everything the game engine needs: node layout (matching the game's chip metrics and spacing), pre-filled word selection, move limits, camera framing, and tray order.

## Features

- Difficulty presets (Easy → Expert) controlling tree size, depth, and vocabulary
- Batch generation with cross-level word/theme exclusions and a persistent theme cooldown
- Live tree preview showing pre-filled vs. player-placed words
- **▶ Play Test** — runs generated levels in the actual embedded game engine
- **⬇ Download Playable HTML** — exports a standalone game file with your levels
- JSON export that pastes straight into the game's `LEVELS` array

## Usage

Open `index.html` in a browser (or deploy anywhere static, e.g. Netlify), paste your
API key, and generate. The key stays in your browser and is sent only to the AI
provider's API.

Engines: Frontier (most capable), Advanced (default), Standard, Lite.
