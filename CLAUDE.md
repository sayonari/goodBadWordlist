# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a multilingual word filtering system for speech recognition subtitling, specifically designed for jimakuChan (音声認識字幕ちゃん). The repository maintains curated lists of inappropriate words (BadList.txt) and exception words (GoodList.txt) across 20+ languages.

## Architecture

- **Language-based directory structure**: Each language has its own directory (ja/, en/, zh-CN/, etc.) containing two files:
  - `BadList.txt`: Words to be censored/replaced with asterisks
  - `GoodList.txt`: Exception words that should not be censored (prevents false positives)

- **Filtering logic**: The system replaces bad words with `***` but preserves good words even if they contain substrings from the bad list
  - Example: "ASMR" contains "SM" (bad word) but is preserved because it's in GoodList.txt
  - Example: "タイマンコラボ" contains "マンコ" (bad word) but is preserved as "タイマンコラボ"

## Supported Languages

ar, de, en, es, fr, id, it, ja, ko, nl, pl, pt, ru, so, sv, th, tr, uk, vi, zh-CN, zh-TW

## Word List Management

- Words in BadList.txt should be one per line
- Words in GoodList.txt should be one per line  
- GoodList.txt takes precedence over BadList.txt for substring matching
- Some BadList.txt files may be empty (like en/BadList.txt)
- Focus on context-appropriate filtering for streaming/subtitling use cases

## Integration

This word list system integrates with:
- jimakuChan service: https://sayonari.github.io/jimakuChan/
- Main project: https://github.com/sayonari/jimakuChan/