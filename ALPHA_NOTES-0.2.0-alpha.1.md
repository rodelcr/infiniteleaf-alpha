# InfiniteLeaf 0.2.0-alpha.1: tester notes

## 1. Definition
InfiniteLeaf is a local, Overleaf-like LaTeX editor: your files stay in a folder on
your disk, and it compiles with your own TeX install. This is the first internal alpha, unsigned,for a small group of colleagues. Expect rough edges, and please report them. These instructions are mostly written by Claude.

**Downloads** (from the prerelease on the private `infiniteleaf-alpha` GitHub repo):

| File | For |
|---|---|
| `InfiniteLeaf-0.2.0-alpha.1-aarch64.dmg` | Apple Silicon Macs (M1 or later) |
| `InfiniteLeaf-0.2.0-alpha.1-x86_64.dmg` | Intel Macs (only if this release lists it) |
| `SHA256SUMS` | checksums; verify with `shasum -a 256 -c SHA256SUMS` in the download folder |
| `ALPHA_NOTES-0.2.0-alpha.1.md` | this file |

What is in this alpha:
- **Projects and editing**
  - Open a folder, file tree, tabs, autosave, CodeMirror editor.
  - Overleaf-style keymap (Mod-b, Mod-i, Mod-/, Mod-d, Mod-Shift-l go to line).
  - Multi-cursor (Mod-Alt-Up / Mod-Alt-Down, Mod-Alt-Right / Mod-Alt-Left for the next / previous
    occurrence) and column selection (Alt-drag).
  - LaTeX and `.bib` syntax highlighting, and section folding.
  - Autocomplete for commands, environments, packages, labels, files, citations and your own
    macros (Mod-Space or Ctrl-Space), and an Outline panel.
  - Math preview on hover.
  - Local spell check (suggest-only, en-US / en-GB) and an optional LanguageTool grammar check (off by default).
  - Find/replace (Mod-f) and project-wide search (Mod-Shift-f).
  - Word count (texcount) for the project and for a selection (Mod-Shift-c).
  - Paste a screenshot into a `.tex` file: it lands in `figures/` with an `\includegraphics` stub.
  - Figure freshness badges in the file tree.
  - Symbols panel: find a symbol by command, keyword or Unicode character, or draw it.
  - Themes: six built-in themes (light and dark), a theme editor, VS Code theme import and a
    theme builder (from colours or an image). The theme picker is the gear at the bottom of the left rail.
- **Compile and PDF**
  - Mod+Enter compiles with latexmk. Mod+S saves, then compiles.
  - **Automatic engine choice.** A `% !TEX program = …` line in the first 20 lines of the main
    file wins; otherwise a compiler you picked; otherwise the preamble decides (for example
    `fontspec` → XeLaTeX, `luacode` → LuaLaTeX); otherwise pdfLaTeX. The Recompile menu shows the
    decision and why.
  - **Runaway compiles are stopped.** A log over 50 MB, a log growing over 20 MB in 10 s, or a run
    longer than the time limit (default 10 min; Recompile ▾ → "Stop compile after") stops the
    compile. The log keeps the first error, and the banner offers "Allow longer".
  - Log pane with plain-language hints and quick-fixes, plus Code Check for unclosed environments.
  - Checks panel (page limit, anonymization) and "Export for submission" (zip plus a test compile).
  - PDF viewer with zoom and fit, and an optional dark PDF display.
  - SyncTeX both ways: Mod+Alt+J (source to PDF), double-click in the PDF (PDF to source),
    Mod+Alt+Shift+J or the ← button (PDF reading position to source). PDF-to-source now lands
    on the right line at every zoom level and display scaling. The editor's file bar has a
    **→ Show in PDF** button.
  - A detachable PDF window for a second monitor. Its toolbar has → and ← sync buttons too.
- **History**
  - A central git repository keeps automatic snapshots of your project.
  - Timeline, labelled versions, diffs, restore a file or the whole project.
  - "Compare as PDF" (latexdiff) between two versions.
  - Optional remote (git URL or GitHub token) with a sync indicator and a conflict view.
- **Zotero**
  - Zotero panel: search, Cite, add to `.bib` without duplicates, `.bib` hygiene checks.
  - `\cite{` completion from your `.bib` and from Zotero.
  - A read-only mirror of your Zotero libraries (`library.bib`, refreshed about every minute
    while Zotero is running). When Zotero is closed, search and `\cite{` completion use it (the
    panel says "Search library mirror").
  - "Different details" notes when your `.bib` entry differs from Zotero's. Updates are
    suggest-only: one entry per click, only the fields you tick, citekeys never changed.
- **Agents (MCP)**
  - A small MCP server on `127.0.0.1` lets an agent such as Claude Code read the app's state
    and open files, compile or show a spot in the PDF. Agents cannot edit your text or push.
  - It is **on by default**. The first launch shows a one-time notice, and the **MCP** chip in
    the top bar turns it off at any time. Each launch uses a new access token.
- **App log**
  - Errors, failed commands and error dialogs go to `~/Library/Logs/app.infiniteleaf.desktop/infiniteleaf.log`,
    with your home folder and project path redacted. Attaching it to a bug report helps.
- **Safety and storage**
  - Exact, atomic saves; a "changed on disk" banner instead of silent overwrites.
  - **Recovery of unsaved text.** Text the editor is holding (a failed save, or the "changed on
    disk" hold) is journaled to the app data folder. After a crash or force quit, the editor
    offers "Restore into editor" or "Discard".
  - One running copy of the app at a time; a second launch focuses the first window.
  - **Project settings and the word list now live in `.infiniteleaf/`** inside the project
    (`settings.json`, `words.txt`), so they are kept in History and carried by
    "Add to InfiniteLeaf". An older project's `.lo/settings.json` and `.lo/words.txt` are copied
    over once. `.lo/` keeps only build output and machine-local state.
  - A project in a cloud-synced folder (iCloud Drive, Google Drive, Dropbox, OneDrive) gets a
    notice, and the central History repository is refused there.

## 2. Before you start
**Required**
- **macOS**, Apple Silicon or Intel. Pick the matching download:
  - Apple Silicon (M1 or later): `InfiniteLeaf-0.2.0-alpha.1-aarch64.dmg`.
  - Intel: `InfiniteLeaf-0.2.0-alpha.1-x86_64.dmg`, if this release has one.
  - Not sure? Apple menu ▸ About This Mac: "Chip: Apple M..." means Apple Silicon, "Processor: Intel..." means Intel.
- **MacTeX or BasicTeX**, with `latexmk` and `synctex`.
  - MacTeX installs into `/Library/TeX/texbin`, which the app finds even when launched from Finder.
  - BasicTeX is smaller but you must add packages yourself (`sudo tlmgr install latexmk <packages>`).
  - Check in Terminal: `latexmk -v` and `synctex help` should each print a version or usage text.
    If the app says "TeX not found", it names the missing tool.
- **git**, version 2.25 or newer (2.39.1 or newer recommended). Needed for History.
  - Check: `git --version`. If macOS offers to install the Command Line Tools, accept.
- **A GitHub account with access to the private `infiniteleaf-alpha` repository**, to download
  releases and to file bug reports (section 8).

**Optional**
- **Zotero 7 or newer**: unlocks the citation panel and Zotero `\cite{` completion.
  - Zotero ▸ Settings ▸ Advanced: turn on "Allow other applications on this computer to communicate with Zotero".
  - Keep Zotero running while you write.
  - Check: the Zotero panel in InfiniteLeaf shows a connected status. Or, with Zotero open, `http://127.0.0.1:23119/api/users/0/items/top?limit=1` in a browser returns JSON (a 403 means the setting above is off).
  - If Zotero is closed, the panel says so; `.bib` keys still complete and search uses the library mirror.
- **Better BibTeX for Zotero**: stable citekeys and the Zotero picker (Mod-Alt-c).
  - Download the `.xpi` from the Better BibTeX releases page, then Zotero ▸ Tools ▸ Plugins ▸ "Install Plugin From File...", then restart Zotero.
  - Check: Mod-Alt-c in a `.tex` file opens Zotero's picker. Without it, the shortcut focuses the panel search box.
- **latexdiff**: unlocks "Compare as PDF" between two versions in History.
  - Check: `latexdiff --version`. It ships with MacTeX. With BasicTeX: `sudo tlmgr install latexdiff`.
- **texcount**: exact word counts.
  - Check: `texcount -v`. It ships with MacTeX. Without it you get an approximate count labelled "approx.".
- **A LanguageTool server**: grammar checking, local only. Turn it on from the Spelling menu in
  the status bar ("Grammar (LanguageTool)").
  - Start: `java -cp languagetool-server.jar org.languagetool.server.HTTPServer --port 8081` (needs Java).
  - Check: `curl http://localhost:8081/v2/languages` returns JSON. Only a loopback address is accepted.

## 3. Installing
1. Open `InfiniteLeaf-0.2.0-alpha.1-<arch>.dmg` and drag **InfiniteLeaf** to **Applications**.
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

## 4. First run
1. **Use a COPY of a paper, not your only copy.** This is an alpha. Copy the project folder
   somewhere new and open that.
2. Choose "Open folder". The file tree appears and the main `.tex` file is detected.
3. **Compile** with Mod+Enter. The PDF appears on the right. Open Logs if there are warnings.
4. **Try SyncTeX.** Put the cursor on a line and press Mod+Alt+J. Then double-click a word in the PDF.
   - If you copied a folder that already had a `.lo/build`, compile once first. Otherwise sync says "outside the project".
5. **History (optional).** On first launch a setup dialog offers a central folder for snapshots.
   - Accept the suggested location or choose your own. "Not now" is fine; you can set it up later.
   - Avoid cloud-synced folders (iCloud Drive, Google Drive, Dropbox, OneDrive) for the central
     folder; the app refuses them. Two machines syncing a git repository underneath git can corrupt it.
   - Then use "Add to InfiniteLeaf" on your project copy. The original folder is left untouched.
6. If you want, set a page limit or main file in `.infiniteleaf/settings.json` (see section 7), then reopen the project.

## 5. Please try
Each item: action, then what you should see. Tell us if anything differs.
1. **Compile.** Open a copy of your paper, press Mod+Enter. The PDF appears; the header shows the Logs count and a page-count chip.
2. **Error markers.** Add `\foo` on an empty line and compile. Only `\foo` is underlined and has a gutter marker; Logs ▸ Errors shows "Undefined control sequence" with a hint. Removing it and recompiling clears the marker.
3. **Click a log entry.** Clicking `main.tex:<line>` in Logs opens that file at that line.
4. **Code Check.** Type `\begin{equation}` with no `\end`. It is flagged before compiling; the quick-fix inserts only `\end{equation}`, and Cmd+Z undoes it in one step.
5. **Forward SyncTeX.** Open a file, put the cursor on a line, press Mod+Alt+J. The PDF scrolls to it and a yellow box fades over about 2 s.
6. **Inverse SyncTeX.** Double-click a paragraph in the PDF. The editor opens the right source file at that line.
7. **Zoom.** Use the toolbar -/+, the percent menu (Fit page, Fit width), Mod+= / Mod+- / Mod+0 over the PDF, or pinch. Pages stay sharp after you stop, and your place is kept after a recompile.
8. **Detached PDF window.** Click Detach. A PDF window opens and the editor takes the full width. Recompile: the window reloads and keeps its page. Quit and relaunch: the window comes back at the same size and position (the app starts attached).
9. **Export for submission.** Recompile menu ▸ "Export for submission...". The report shows a successful test compile and the page count. An undefined `\cite` key makes the export refuse and list the key.
10. **Paste a screenshot.** Copy a screenshot, paste on an empty line in a `.tex` file. `figures/pasted-<date-time>.png` is created and an `\includegraphics` line is inserted.
11. **Find and project search.** Mod-f with a regex such as `a(\d)` replaced by `b$1`; Mod-Shift-f for project-wide search. Clicking a hit selects the exact match.
12. **Word count.** Select a paragraph, press Mod-Shift-c. A tooltip shows the printed-word count.
13. **History.** After "Add to InfiniteLeaf", edit and wait about 3 minutes for an `autosave` entry. Label a version "Draft 1", click it to see the diff, restore one file (confirm dialog; open tabs reload).
14. **Quit with unsaved edits.** Type something and press Cmd+Q right away. Nothing is lost; with a detached PDF window, both windows close.
15. **Zotero.** With Zotero running and the API enabled, type `\cite{` plus a few letters. Your `.bib` keys appear first, then Zotero items. Picking one appends exactly one entry to the `.bib`; the diff is only added lines at the end. Recompile: no undefined citations.
16. **Themes.** Open the theme picker, edit a theme, change a colour. The live preview updates; Cancel restores your theme. PDF pages are never recoloured.
17. **Engine choice.** In a copy of a paper that uses `fontspec`, compile without a `% !TEX program` line. The Recompile menu says XeLaTeX was chosen from the preamble.
18. **Symbols.** Open the Symbols panel from the left rail, draw an integral sign or search "alpha", and insert it.
19. **MCP switch.** On first launch a one-time notice explains the MCP server. Click the **MCP on** chip in the top bar, switch it off (the chip says **MCP off**), then on again.

## 6. Known gaps and limitations
**Not in this alpha**
- **Nothing is sent to Overleaf.** There is no Overleaf sync yet. Your project stays local; the History remote is a plain git remote you choose.
- No terminal dock and no review of agent edits inside the app (the Terminal entry in the left
  rail is a placeholder). Agents connect from outside through MCP (section 1) and cannot edit your text.
- No auto-update (download releases by hand).
- macOS only. No Windows or Linux builds.
- No Developer ID signature or notarization (ad-hoc signature only).
- There is no Help menu; "Report a bug…" is the bug icon in the left rail and a link on the start screen.

**Rough edges we already know about**
- Nothing in this build has been clicked through by a person on the final binary. The automated tests pass; the click-through is what you are doing now.
- A project copied with its `.lo/build` folder gives "outside the project" on PDF-to-source sync until you recompile.
- Settings in `.infiniteleaf/settings.json` are read when a project opens; after editing the file on disk, reopen the project. A corrupt or newer-version settings file is set aside as `settings.corrupt-<ms>.json` / `settings.newer-<ms>.json` with a notice, not overwritten.
- The central repository ignores some build-leftover patterns (`*.log`, `*.out`, `*.aux`, `*.toc`...) at every depth, and a project's own `.gitignore` is honoured. A data file named `chain.out` or a `*.pdf` ignore rule would be left out of history. The History panel lists open files that are ignored.
- Opening a folder that is already a git repository adds `.lo/` and `.infiniteleaf/` to its `.git/info/exclude` (its tracked `.gitignore` is not changed). Still, do not open an Overleaf git-bridge clone or a collaborator's repository directly.
- Custom themes, dictionaries, taught symbols and preferences stay on this machine; there is no export.
- Closing the app when files changed on disk or a sync is pending can take a few seconds.
- The "changed on disk" banner (Keep mine / Load disk version) appears if history or sync rewrites a file you are editing. The text you were holding is journaled for recovery until you choose.
- A file with thousands of unclosed `{` switches the editor to basic highlighting ("Large or unusual file: using basic highlighting").
- Detached PDF window: the app starts attached; a "no match" toast can cover the file bar for up to 4 s; there are no clickable PDF links.
- "Compare as PDF" and remote sync need git, latexdiff and a working network or reachable remote as appropriate.

## 7. Your data
- **Saves are exact and atomic.** What you see in the editor is written byte for byte; InfiniteLeaf never reformats your files. A save writes a temp file and renames it into place.
- **Where things live**
  - Your project: the folder you opened, unchanged apart from two hidden folders:
    - `.infiniteleaf/`: project settings (`settings.json`: main file, compiler, page limit,
      anonymous mode, spelling) and the word list (`words.txt`). Kept in History.
    - `.lo/`: build output (`.lo/build/`), figure sources and other machine-local state. Not kept in History.
  - History: a central git repository in the folder you chose in the setup dialog (the suggested one is `InfiniteLeaf` in your home folder). It holds a copy of each project you add, with its history. Your original folder is not modified by "Add to InfiniteLeaf".
  - App settings, themes, dictionaries, symbols, recent projects, recovered unsaved text, the
    Zotero mirror and the MCP session file (`mcp/session.json`, readable only by you, new each
    launch): `~/Library/Application Support/app.infiniteleaf.desktop/` (see section 9).
  - The app log: `~/Library/Logs/app.infiniteleaf.desktop/` (paths redacted; 5 MB × 3 files).
  - A GitHub token, if you connect one, is stored in the macOS Keychain (service `infiniteleaf`), never in a file.
  - Display preferences (theme choice, layout, PDF zoom) are in the app's web storage on this Mac.
- **Nothing leaves your machine** except a bug report you choose to submit, and calls to a remote you set up yourself. Zotero and LanguageTool are reached only on the loopback address, and the MCP server listens only on `127.0.0.1` (turn it off with the MCP chip). There is **no telemetry** and no update check.
- Still: it is an alpha. Work on a copy.

## 8. Reporting bugs
- Click the **bug icon** at the bottom of the left rail, or "Report a bug..." on the start screen.
- A dialog shows a **preview of exactly what will be sent**:
  - app version, macOS version and chip, and the versions of latexmk, pdflatex, xelatex, lualatex, synctex, texcount and git (versions only, no paths);
  - your summary and description.
  - Paths are redacted: your home folder shows as `~`, the project root as relative, user names as `<user>`.
  - Two boxes are **off by default** because they can reveal paper content: the tail of the compile log, and the open file's name. Tick them only if you are comfortable.
- "Open GitHub issue" launches a **prefilled issue on the private `infiniteleaf-alpha` repository** in your browser. Nothing is sent until you press Submit there. "Copy report" puts the Markdown on your clipboard instead.
- You need a **GitHub account with access to `infiniteleaf-alpha`** (the dialog names the exact repository). You will be added as a collaborator; if the issue page shows 404, ask to be added.
- Long reports (over about 7,500 bytes) are truncated in the URL: the full report is copied to your clipboard first, then the browser opens. Paste it into the issue.

## 9. Uninstalling
Quit the app, then:
1. Delete `/Applications/InfiniteLeaf.app`.
2. App data (all optional; delete to reset):
   - `~/Library/Application Support/app.infiniteleaf.desktop/`. On macOS the app's config and
     data folders are the same folder. It holds `central.json`, `recents.json`, `themes/`,
     `pdf-window.json`, `agent-policy.json`, `dictionaries/`, `symbols/`, `zotero/` (the mirror),
     `mcp/` and `recovery/` (recovered unsaved text).
   - App log: `~/Library/Logs/app.infiniteleaf.desktop/`.
   - Web storage (theme, layout, zoom): most likely `~/Library/WebKit/app.infiniteleaf.desktop/`. Not yet confirmed on a release build.
3. Keychain: if you connected GitHub, open Keychain Access and delete the entry with service `infiniteleaf`.
4. Your history: the central repository folder you chose (suggested name `InfiniteLeaf` in your home folder) is **not** removed automatically. Delete it only if you do not want the history.
5. Inside each project you opened: the hidden `.lo/` folder can be deleted; it only holds build output and machine-local state. `.infiniteleaf/` holds the project's settings and word list; delete it only if you want those gone.
