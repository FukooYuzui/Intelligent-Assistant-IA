# 智能助教IA：Intelligent Assistant

An Obsidian desktop plugin for studying with question banks or AI-generated questions, handwriting in Excalidraw, and reviewing work with the locally signed-in Codex CLI. The plugin supports mathematics and other subjects through subject, textbook, and chapter filters. Interface language: Chinese.

Current version: **0.1.17**. This repository contains the installable plugin files and small example banks. It does not include textbook scans, imported question banks, handwriting, study history, or account data.

## What it does

- Choose questions from a JSON/Markdown bank or generate original practice questions with a separate answer check.
- Work on an Excalidraw board with a fixed question panel above it. Submit the current board for visual review without navigating away.
- Ask follow-up questions about a review, or request a recheck of the frozen original submission.
- Practice sequentially, randomly, or with due reviews; filter by subject, textbook, chapter, and difficulty.
- Store drawings under `CMC学习/练习/<科目>/<日期>/` and reopen the original drawing when the same question returns.

AI feedback is a study aid; inspect results against the original textbook where accuracy matters.

## Requirements

- Obsidian desktop 1.7.2 or later
- Excalidraw Obsidian plugin, using Markdown drawing files
- Official [Codex CLI](https://developers.openai.com/codex/cli/) installed and signed in with an account that can use Codex

No API key is required. The plugin runs the local Codex CLI and needs network access for AI features.

## Install

1. Close Obsidian after saving your open drawings.
2. Copy `main.js`, `manifest.json`, and `styles.css` into `<your vault>/.obsidian/plugins/cmc-codex-trainer/`. Create that folder if necessary. For an update, keep the existing `data.json` and vault study files.
3. Reopen Obsidian. In **Settings → Community plugins**, enable Excalidraw and **智能助教IA：Intelligent Assistant**.
4. Open the 智能助教IA learning panel from the ribbon or command palette. Check the Codex login status. If Obsidian cannot find Codex, set its full executable path in plugin settings.

The repository root is the plugin folder. Keep the internal directory and manifest ID `cmc-codex-trainer`: this stable identifier preserves existing Obsidian installations and study data. The display name and GitHub repository are **智能助教IA：Intelligent Assistant**.

## Add questions

Use **粘贴题库** to paste JSON directly, or place a `.json` file in the Obsidian vault and choose **导入文件**. For multiple subjects, use JSON with `subject`, `textbook`, `topic`, and a nonempty `statement`. A minimal example is in [`examples/question-bank.json`](examples/question-bank.json). If a question refers to `sourceImages` or `answerImages`, copy those image files into the vault at exactly the paths listed in JSON before starting a drawing. The example bank does not require textbook images.

The file import merges by stable question `id`: matching IDs are updated, other questions are kept. Existing practice sessions retain their saved question snapshots. The plugin does not automatically extract questions from a PDF or build a browsable chapter index from the imported JSON.

## Privacy and data

Your question bank, sessions, reviews, and settings live in the vault's `.obsidian/plugins/cmc-codex-trainer/data.json`; drawings and submissions live in the vault. Back up both before moving vaults or reinstalling. Never commit `data.json` or your vault to this repository. Submitting work sends the selected question, reference material, and submitted drawing through the locally authenticated Codex CLI for AI review.

## Release contents

`main.js` is the bundled Obsidian entry point, `manifest.json` declares plugin compatibility, `styles.css` styles the panel, and `examples/` contains small sample banks. This snapshot is distributed as installable JavaScript; original modular TypeScript source is not part of this release.

Licensed under MIT; see [LICENSE](LICENSE).
