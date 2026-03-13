# Obsidian Theme — Project Context

## What this is
A personal fork of [Primary for Obsidian](https://github.com/primary-theme/obsidian) by Cecilia May (GPL-3.0).
Goals: fix bugs, maintain compatibility with latest Obsidian, and add personal stylistic tweaks.
Not intended for public release.

## Key files
- `src/scss/` — Sass source files, organized by category (editor, components, core plugins, etc.)
- `src/scss/index.scss` — main entry point that imports all partials
- `src/css/style-settings.css` — Style Settings plugin configuration (user-facing options)
- `theme.css` — compiled output used by Obsidian (do not edit directly)
- `Primary.css` — identical to theme.css, used for the Obsidian theme store
- `.env` — sets `OBSIDIAN_PATH` for hot-reload (gitignored)

## Build system
Uses Grunt + Dart Sass (via grunt-contrib-sass).

**One-shot build** (no vault needed):
```
npx grunt sass:unminified sass:minified cssmin concat_css
```

**Watch mode with hot-reload** (requires `.env` with `OBSIDIAN_PATH`):
```
export $(cat .env | xargs) && npx grunt
```
The watch task compiles on save and copies `theme.css` to the vault automatically.
Obsidian does not need to be restarted — it picks up CSS changes live.

Note: `OBSIDIAN_PATH` must be exported *before* grunt starts — the copy destination is
evaluated at startup, so `grunt-env` loading it mid-run is too late.

PATH note: node@22 is keg-only. Ensure it's in `~/.zshrc` (it is, as of initial setup):
```
export PATH="/opt/homebrew/opt/node@22/bin:$PATH"
```

## Scss structure
```
src/scss/
  index.scss               ← imports everything
  40_editor/               ← headings, code, tables, lists, links, tags, callouts, etc.
  50_core-plugins/         ← bookmarks, file explorer, graph, search, canvas
  60_community-plugins/    ← calendar, kanban, style-settings
  30_components/           ← color inputs, progress bars, etc.
```

## User preferences
- Font: SN Pro (custom, not bundled with theme)
- Appreciates the "whimsy" of Primary — don't strip personality when fixing bugs
- Minimal plugin philosophy — avoid adding complexity
- Tone should be lively but wise; approachable and friendly.

## Git setup
- `origin` remote → MariusMasalar/obsidian-theme (private fork, push changes here)
- `upstream` remote → primary-theme/obsidian (original repo, pull upstream fixes from here)

## Workflow
1. Edit `.scss` files in `src/scss/`
2. Run build (or let watch mode do it)
3. Test in Obsidian
4. Commit working changes with descriptive messages
