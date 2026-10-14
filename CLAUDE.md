# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

A personal collection of standalone HTML slide presentations ("Slide Deck Hub"), each built on reveal.js and served as static files (e.g. via GitHub Pages). There is no build system, package manager, or test suite — every presentation is a single self-contained `index.html`.

## Architecture

- `index.html` (repo root) — the hub/portal page. A static grid of cards, each linking to a presentation subfolder (e.g. `./test/`). New presentations are added by duplicating a `<a class="card">` block in `.menu-container` and pointing it at the new subfolder.
- Each presentation lives in its own subfolder (e.g. `test/`, `winwin/`) with its own `index.html`. Presentations use the reveal.js framework: a `<div class="reveal"><div class="slides">` wrapper containing one `<section>` per slide.
- Supporting assets for a presentation (images, data files like `winwin/games.txt`) live alongside that presentation's `index.html` in the same subfolder.
- No shared CSS/JS between presentations — each `index.html` pulls its own reveal.js stylesheet/script links and is otherwise self-contained.

## Known issue: broken CDN links

In `test/index.html`, the reveal.js `<link>`/`<script>` tags point to bare `https://cloudflare.com` instead of real reveal.js CDN URLs (e.g. `https://cdnjs.cloudflare.com/ajax/libs/reveal.js/<version>/reveal.min.css` and `.../reveal.min.js`). This was introduced by a past edit that mislabeled the change as a "FIX" in commit `5237ec6`/`bedcebf`. When touching a presentation that doesn't render, check for this before assuming the slide content itself is wrong — restore proper reveal.js CDN URLs (css theme + core js, plus `Reveal.initialize()`).

## Working on presentations

- To add a new presentation: create a new subfolder with its own `index.html` using the reveal.js structure, then add a card to the root `index.html` linking to `./<folder>/`.
- To edit slides: each `<section>` in `.slides` is one slide; edit content directly in HTML.
- To preview: open the HTML file directly in a browser, or serve the repo root with any static file server (there's no dev server script in this repo).
- `winwin/` is in-progress work (untracked) with Hebrew/RTL content for sports-matchup slides driven loosely by `games.txt`; treat its content as a draft when editing.
