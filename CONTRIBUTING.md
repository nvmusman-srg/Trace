# Contributing to Trace

Thanks for your interest. This is a small, beginner-friendly project — if it's your first time contributing to open source, this is a good place to start.

## Setup

There's no build step. Fork the repo, clone it, and open `index.html` in a browser (or serve it with `python3 -m http.server`). Make your change, refresh, done.

## Ways to help

Some ideas, from easy to harder:

- **Add more metadata fields.** The known-tag map lives in `index.html` (`KNOWN`). Add a friendly label and group for a tag that isn't covered yet.
- **Improve PDF parsing.** The current PDF reader scans for the Info dictionary and XMP. It could handle more edge cases.
- **Vendor the libraries** so the app ships fully offline out of the box (see the README).
- **Translations.** The interface copy is all in `index.html` and could be localised.
- **Design and accessibility.** Polish the UI, improve keyboard navigation, or test with a screen reader.
- **Docs.** Add a screenshot or a short demo GIF to the README.

## Guidelines

- Keep it dependency-light. The whole point is a single file that just works.
- Keep it privacy-first. No feature should send a user's file or data off their device.
- Match the existing code style (plain vanilla JS, no framework).
- One focused change per pull request, with a short description of what and why.

## Reporting issues

Open an issue describing what you expected, what happened, your browser, and the file type involved (don't upload a real personal file — a description is enough).
