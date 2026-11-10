# InfiniteLeaf alpha

## Download the latest alpha (0.2.0-alpha.8)

- **[Apple Silicon Macs (M1 or later)](https://github.com/rodelcr/infiniteleaf-alpha/releases/download/v0.2.0-alpha.8/InfiniteLeaf-0.2.0-alpha.8-aarch64.dmg)**
- [Intel Macs](https://github.com/rodelcr/infiniteleaf-alpha/releases/download/v0.2.0-alpha.8/InfiniteLeaf-0.2.0-alpha.8-x86_64.dmg)

Which Mac do I have? Apple menu ▸ About This Mac: "Chip: Apple M…" is Apple Silicon.
Install steps and what to try: [tester notes](ALPHA_NOTES-0.2.0-alpha.8.md).
All releases: [Releases](https://github.com/rodelcr/infiniteleaf-alpha/releases).
Connect to Overleaf: [Overleaf guide](OVERLEAF.md). Connect to Zotero: [Zotero guide](ZOTERO.md).

## Key features
InfiniteLeaf is a local, Overleaf-like LaTeX editor: your files stay in a folder on
your disk, and it compiles with your own TeX install.

- **Overleaf sync**: open a project from Overleaf, bring coauthors' edits in, and send yours,
  automatically every few seconds if you want.
- **Overleaf comments and review**: comments and suggestions beside the text, a new comment from a
  selection, reply/resolve/accept, and actions made offline are sent when you reconnect.
- **History with Overleaf**: Overleaf's versions and labels next to your own, labels on any earlier
  version (also on Overleaf when the version matches exactly), compare with an Overleaf version.
- **Projects and editing**
  - Overleaf-style keymap (⌘-b, ⌘-i, ⌘-/, ⌘-d, ⌘-Shift-l go to line).
  - Autocomplete for commands, environments, packages, labels, files, citations and your own
    macros (⌘-Space or Ctrl-Space), and an Outline panel.
  - Math preview on hover.
  - Find/replace (⌘-f) and project-wide search (⌘-Shift-f).
- **Compile and PDF**
  - ⌘+Enter compiles with latexmk. ⌘+S saves, then compiles.
  - Log pane with plain-language hints and quick-fixes, plus Code Check for unclosed environments.
  - SyncTeX both ways: ⌘+⌥+J (source to PDF), double-click in the PDF (PDF to source).
  - A detachable PDF window for a second monitor.
- **History**
  - A central git repository keeps automatic snapshots of your project.
  - "Compare as PDF" (latexdiff) between two versions.
- **Zotero**
  - Zotero panel: search, Cite, add to `.bib` without duplicates, `.bib` hygiene checks.
  - `\cite{` completion from your `.bib` and from Zotero.
- **Safety and storage**
  - Exact, atomic saves; a "changed on disk" banner instead of silent overwrites.

## Report a bug
In the app: the bug icon at the bottom of the left sidebar. Or [open an issue](https://github.com/rodelcr/infiniteleaf-alpha/issues/new?labels=bug).
