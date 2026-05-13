# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Resume-Skill-Agent** — AI-powered resume material augmentation tool (browser extension/sidebar). Uses multi-agent collaboration to mine Git repositories and generate STAR-principle resume content matched to target job descriptions (JDs). Documentation is in Chinese (中文).

## Current Status

Early planning stage. Only the PRD exists at `doc/产品需求规格说明书 .md`. No source code, build system, or tests yet.

## Planned Architecture

Four core Agent Skills communicate via a **dialogue bus**:

1. **JD Mind Reader (JD 读心术)** — Job profile analysis: extract tech keywords, assess skill weights, identify company style
2. **Code Archaeologist (代码考古家)** — Git asset mining: identify high-complexity, high-performance, high-value modules
3. **STAR Translator (STAR 翻译官)** — Content construction: convert technical facts into business/technical value language, multi-version generation
4. **Dialogue Guide (对话引导员)** — Process control: manage human-in-the-loop interactions, context, and user confirmations

## Planned Business Flow

1. User pastes JD + provides Git repo address → 2. Agent collaboration (JD insights + code scanning) → 3. Dialogue: user selects/modifies highlights → 4. Output STAR description blocks for copy-paste

## Key Technical Decisions (from PRD)

- **Prompt strategy:** Three-stage filtering model (structure scan → deep archaeology → dialogue guidance)
- **Performance:** Code preprocessing to remove boilerplate, partial reading of high-potential code blocks only
- **Privacy:** No raw code storage, metadata only, one-click cache clearing
- **Export:** Markdown and plain text formats
