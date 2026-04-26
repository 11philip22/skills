# CLI Reference

## Command

Install the published package with:

```bash
npm install -g hero-generator-bin
```

Run the published command with:

```bash
hero-generator [options]
```

The command writes a PNG to disk and prints the output path on success.
It generates a new banner file; it does not edit an existing PNG in place.

## Options

- `--name <text>`: Project name. Default: `Project Title`
- `--subtitle <text>`: Subtitle or tagline. Default: `Short project tagline`
- `--description <text>`: Longer project summary. Default: `A brief description of your project and what it does.`
- `--tags <csv>`: Comma-separated tags. Empty entries are discarded.
- `--accent <preset-or-hex>`: One of `ORANGE`, `CYAN`, `LIME`, `VIOLET`, `RED`, `AMBER`, `ROSE`, `ICE`, or a `#RRGGBB` hex color.
- `--bg <style>`: One of `NONE`, `DOTS`, `GRID`, `SCAN`, `WAVE`, `VOID`, `ZEBRA`.
- `--mode <dark|light>`: Color mode.
- `--seed <value>`: Seed for deterministic procedural backgrounds.
- `--out <path>`: Output PNG path. If omitted, the filename becomes `<normalized-name>-hero-banner.png`.

## Derived Behavior

- The default accent is `ORANGE`.
- The default background is `WAVE`.
- The default mode is `dark`.
- Tag parsing trims whitespace and removes blank items.
- Output filenames are lowercased, spaces become hyphens, and an empty name falls back to `banner-hero-banner.png`.
- Invalid accent, background, or mode values throw an error and cause a non-zero exit.

## Help

Show the built-in help text with:

```bash
hero-generator --help
```
