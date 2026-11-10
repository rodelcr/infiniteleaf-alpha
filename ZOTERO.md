# Connecting InfiniteLeaf to Zotero

<!-- Assembled 2026-11-10 from ALPHA_NOTES-0.2.0-alpha.8.md (verbatim; selection only).
     Sources: "What you get" = section 1 "Zotero" bullets; "Set up" = section 2 "Optional" Zotero and
     Better BibTeX bullets; "Try it" = section 5 item 15.
     "Where things are" written by Claude at Rodrigo's request (2026-11-10). -->



## What you get
- Zotero panel: search, Cite, add to `.bib` without duplicates, `.bib` hygiene checks.
- `\cite{` completion from your `.bib` and from Zotero.
- A read-only mirror of your Zotero libraries (`library.bib`, refreshed about every minute
  while Zotero is running). When Zotero is closed, search and `\cite{` completion use it (the
  panel says "Search library mirror").
- "Different details" notes when your `.bib` entry differs from Zotero's. Updates are
  suggest-only: one entry per click, only the fields you tick, citekeys never changed.

## Set up
- **Zotero 7 or newer**: unlocks the citation panel and Zotero `\cite{` completion.
  - Zotero ▸ Settings ▸ Advanced: turn on "Allow other applications on this computer to communicate with Zotero".
  - Keep Zotero running while you write.
  - Check: the Zotero panel in InfiniteLeaf shows a connected status. Or, with Zotero open, `http://127.0.0.1:23119/api/users/0/items/top?limit=1` in a browser returns JSON (a 403 means the setting above is off).
  - If Zotero is closed, the panel says so; `.bib` keys still complete and search uses the library mirror.
- **Better BibTeX for Zotero**: stable citekeys and the Zotero picker (⌘-⌥-c).
  - Download the `.xpi` from the Better BibTeX releases page, then Zotero ▸ Tools ▸ Plugins ▸ "Install Plugin From File...", then restart Zotero.
  - Check: ⌘-⌥-c in a `.tex` file opens Zotero's picker. Without it, the shortcut focuses the panel search box.

## Try it
**Zotero.** With Zotero running and the API enabled, type `\cite{` plus a few letters. Your `.bib` keys appear first, then Zotero items. Picking one appends exactly one entry to the `.bib`; the diff is only added lines at the end. Recompile: no undefined citations.

## Where things are
- **The Zotero panel** is the **Zotero** item on the left rail. Search there, then **Cite** inserts the
  key at the cursor. **Update library** refreshes the mirror now.
- **Which `.bib` gets the entry:** the one your document names in `\bibliography{…}` or
  `\addbibresource{…}`. Entries are only ever added at its end; nothing already in it changes.
- **Insert ▸ Cite from Zotero…** (⌘-⌥-c) opens Zotero's own picker when Better BibTeX is installed.
- **Nothing is written to Zotero.** InfiniteLeaf only reads from it, and only on this computer.
