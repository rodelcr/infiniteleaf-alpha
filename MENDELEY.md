# Using your Mendeley library in InfiniteLeaf

<!-- Written by Claude, 2026-11-10 (alpha.10); the owner allowed Claude-written guides.
     Sources: docs/superpowers/notes/2026-11-10-mendeley-findings.md, NOTES_library_file_2026-11-10.md. -->

## Connect (alpha.11)
<!-- Written by Claude, 2026-11-11 (alpha.11). Sources: docs/superpowers/notes/2026-11-11-mendeley-elsevier-flow-findings.md,
     NOTES_mendeley_live_2026-11-11.md. -->

The easiest way: connect your Mendeley account and InfiniteLeaf keeps a copy of your library up to date by itself.

1. InfiniteLeaf ▸ Settings… ▸ **Connections** ▸ **Mendeley** ▸ **Connect**.
2. Your browser opens Mendeley's sign-in. Sign in with your Elsevier account (the one you use for Mendeley; signing in
   through your institution works too).
3. The browser says "InfiniteLeaf is connected to Mendeley. You can close this tab." Close it.
4. The card shows `Connected · 1,234 references · updated just now` once your library has been read (a large library
   can take a minute).

Then your references show in the **Zotero** panel's search (labelled **Mendeley**) and in `\cite{` completion (a
**Mendeley** section). Citing one adds its entry to your project's `.bib`, as for Zotero. InfiniteLeaf checks Mendeley
for changes every minute.

- **Read only.** InfiniteLeaf only reads your library. It never adds, changes or deletes anything in Mendeley. (Mendeley
  has a single permission level, so the sign-in itself would allow changes; InfiniteLeaf does not use it.)
- **Your own library.** Group libraries are not included yet.
- **Citation keys** are Mendeley's own (`citation_key`). A reference without one gets `AuthorYear` (`Smith2020`,
  then `Smith2020a`, …), and keeps it. Keys can differ from those in a `.bib` you exported by hand.
- **Where it is kept.** The sign-in is kept in your system keychain. If there is none (some Linux setups), you can keep
  it for this session only. Your library copy is a file in InfiniteLeaf's own data folder.
- **Disconnect…** removes the sign-in and the library copy from this computer. InfiniteLeaf stays listed in your
  Elsevier account's connected apps until you remove it there.

If something is off:
- **"Port 8585 … is in use"**: another program uses the port the sign-in comes back to. Close it and click Connect again.
- **"Mendeley has not accepted the new sign-in yet; trying again"**: normal for a minute or two right after a
  first Connect; InfiniteLeaf retries by itself.
- **"The sign-in has expired"**: click Connect and sign in again.
- **"Mendeley asked us to slow down"**: nothing to do; InfiniteLeaf tries again at the time shown.
- **"Mendeley is not available in this build"**: use a BibTeX library file instead (below).

## Or: a BibTeX library file

Mendeley Reference Manager has no way for another app on your computer to read your library, and it cannot keep a
`.bib` file up to date by itself. So InfiniteLeaf works from a **BibTeX file you export from Mendeley**. It reads
that file (it never changes it) and reads it again whenever you export a new copy over it.

The same works for any `.bib` file: JabRef, BibDesk, or an export from another reference manager.

## Set up
1. **Export from Mendeley Reference Manager.** Select all your references, then **Export ▸ BibTeX (.bib)**. Save the
   file somewhere you will keep it, for example `Documents/mendeley.bib`. (Mendeley exports metadata only; your PDFs
   stay in Mendeley.)
2. **Choose it in InfiniteLeaf.** InfiniteLeaf ▸ Settings… ▸ **Connections** ▸ **Mendeley** ▸ **BibTeX library file** ▸
   **Choose library file…**, and pick the file.
3. **Check:** the card shows how many entries it found and when the file was last updated, for example
   `1,234 entries · file updated just now`. If some entries could not be read, it says how many were skipped.

## Use it
- **Search:** open the **Zotero** panel (left rail). Its search box searches your library file too, also when Zotero
  is not installed or not running. Results from the file are labeled **Library file**. **Cite** inserts the key at
  the cursor.
- **`\cite{` completion:** type `\cite{` and a few letters. Keys from your project's `.bib` come first, then Zotero (if
  you use it), then **Library file**.
- **Adding to your project's `.bib`:** when you cite a key that is not in the project's `.bib` yet, InfiniteLeaf adds
  that entry at the end of the `.bib` your document names (`\bibliography{…}` or `\addbibresource{…}`). Nothing already
  in it changes. If the paper is already there (same DOI, or same title and year), it is not added twice and the
  citation uses the key you already have.
- **Citation keys stay Mendeley's.** The key is exactly what Mendeley exported (often `AuthorYear`, like `Smith2020`),
  and the entry is copied as exported.

## Keep it current
Mendeley does not update the file for you. After you add references in Mendeley, **export again to the same file**.
InfiniteLeaf notices the new copy within a few seconds; the card's count and date change.

If you move or delete the file, the card says so. Export it to the same place again, or choose the new location.

**Remove** on the card stops using the file. The file itself is left alone.

## What does not work yet
- The library file is read only when you export it again; the live connection (above) keeps itself current.
- Mendeley's keys can repeat (two `Smith2020` papers). Pick the one you want from the search; both are listed.
- The compile log's "Add from Zotero" fix does not look in the library file.
- One library file at a time, for all your projects.

## If something is off
- **"is not UTF-8 text":** the file uses an older text encoding. Export again, or convert the file to UTF-8 (most
  text editors can save as UTF-8).
- **Many entries skipped:** those entries have keys that a `.bib` cannot use (spaces, braces) or are cut off. Fix
  the key in Mendeley and export again.
- **Search finds nothing:** check the card's status line first; then check that the file you chose is the one you
  exported to.
