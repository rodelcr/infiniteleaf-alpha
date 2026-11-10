# InfiniteLeaf alpha

## Download the latest alpha (0.2.0-alpha.9)

- **[Apple Silicon Macs (M1 or later)](https://github.com/rodelcr/infiniteleaf-alpha/releases/download/v0.2.0-alpha.9/InfiniteLeaf-0.2.0-alpha.9-aarch64.dmg)**
- [Intel Macs](https://github.com/rodelcr/infiniteleaf-alpha/releases/download/v0.2.0-alpha.9/InfiniteLeaf-0.2.0-alpha.9-x86_64.dmg)

Which Mac do I have? Apple menu ▸ About This Mac: "Chip: Apple M…" is Apple Silicon.
Install steps and what to try: [tester notes](ALPHA_NOTES-0.2.0-alpha.9.md).
All releases: [Releases](https://github.com/rodelcr/infiniteleaf-alpha/releases).
Connect to Overleaf: [Overleaf guide](OVERLEAF.md). Connect to Zotero: [Zotero guide](ZOTERO.md).

## Install
**You need** macOS (Apple Silicon or Intel) and a TeX installation: [MacTeX](https://www.tug.org/mactex/)
is easiest. `git` is needed for version control; if macOS offers to install the Command Line Tools, accept.

1. Open the `.dmg` and drag **InfiniteLeaf** to **Applications**.
2. The app is not signed with an Apple Developer ID (it carries only an ad-hoc signature), so
   macOS blocks a normal double-click the first time. You only need to get past this once:
   - **macOS 14 and earlier:** right-click (or Control-click) the app ▸ **Open**, then **Open**
     again in the dialog.
   - **macOS 15 (Sequoia) and later:** the right-click route no longer offers Open. Double-click
     the app once and close the warning, then open System Settings ▸ Privacy & Security, scroll
     to the message about InfiniteLeaf and click **Open Anyway**. Confirm with your password.
3. **Fallback:** if macOS says the app is "damaged" or still "can't be opened", clear the
   quarantine flag in Terminal, then open it again:
   ```
   xattr -dr com.apple.quarantine /Applications/InfiniteLeaf.app
   ```
4. There is no auto-update in the alpha. To update, download the next release and replace the app.

**Try it on a copy of a paper first**, not your only copy: this is an alpha.

## Getting started
- **Open a project.** On the Projects screen: **Open folder…** for a local folder, **New project…**
  to start one, or **Open from Overleaf…** for an Overleaf project. ⌘+Enter compiles; the PDF
  appears on the right.
- **Sync with Overleaf** (comments included). You need an Overleaf plan with Git integration and a
  Git token from Overleaf (Account Settings ▸ Git integration). Step by step: [Overleaf guide](OVERLEAF.md).
- **See and answer Overleaf comments.** Comments are off until you turn them on: Settings (⌘,) ▸
  Connections ▸ Overleaf ▸ tick **Show Overleaf comments and suggestions** (and, to reply, resolve and
  accept, **Allow accepting, rejecting, resolving and replying…**). Then click **Review** in the file
  bar above the editor. In a narrow window it is under the **⋯** button (More file actions) at the
  right end of that bar; **Review** on the left rail opens the overview. Both stay hidden until
  comments are on (alpha.10 will show them always). Details: [Overleaf guide](OVERLEAF.md#comments-and-review).
- **Cite from Zotero.** Keep Zotero 7 running with "Allow other applications on this computer to
  communicate with Zotero" turned on (Zotero ▸ Settings ▸ Advanced), then type `\cite{` or use the
  **Zotero** panel on the left. Step by step: [Zotero guide](ZOTERO.md). Mendeley is planned for a
  later alpha.
- **Use an AI agent.** Click **Terminal** on the left (or press Ctrl+\`): a shell opens in the
  project folder, where you can run your own agent (Claude Code, Codex, Gemini CLI, …) on the
  project's files. To let the agent also see the app (open files, compile, show a spot in the PDF),
  use Settings ▸ Connections ▸ Agents ▸ **Connect**.
- **Several projects at once.** File ▸ **New Window** (⌘N) or **New Tab** (⌘T), or the **+** at the
  top right of the window.
- **Work offline with version control.** Everything works without a connection; see
  [How to establish version control for a project](#how-to-establish-version-control-for-a-project).
- **Draw a symbol.** Click **Symbols** on the left and draw the symbol you have in mind; the closest
  LaTeX commands appear below it, ready to insert. The recognition comes from
  [Detexify](https://detexify.kirelabs.org) by Daniel Kirsch.

More to try, and what you should see: [tester notes](ALPHA_NOTES-0.2.0-alpha.9.md).

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

## How to establish version control for a project
History is kept for projects in your InfiniteLeaf history folder (set up once with **Set up history…**). A project is in it when you:
- create it with **New project…**,
- open it with **Open from Overleaf…**, or
- add an existing folder with **File ▸ Add to InfiniteLeaf…**. This copies the folder in and leaves the original untouched; keep working in the copy.

## Report a bug
In the app: the bug icon at the bottom of the left sidebar. Or [open an issue](https://github.com/rodelcr/infiniteleaf-alpha/issues/new?labels=bug).
