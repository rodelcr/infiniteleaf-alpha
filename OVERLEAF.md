# Connecting InfiniteLeaf to Overleaf

<!-- Assembled 2026-11-10 from ALPHA_NOTES-0.2.0-alpha.8.md (verbatim; selection only).
     Sources: "What you need" = section 1 bullets "Overleaf sync" / "Overleaf comments and review";
     steps 1-7 = section 4 "Automatic sync with Overleaf every few seconds" (step 2: "the **Overleaf** chip" corrected to "the sync button", 2026-11-10: the chip was merged into one sync button).
     "What you need", "Link a project" and "Turn comments on" written by Claude at Rodrigo's request
     (2026-11-10, "you can write what we need as overviews"), from the app's own labels; "Sync by hand" added 2026-11-10. -->

Open a project from Overleaf, bring coauthors' edits in, and send yours, automatically.

## What you need
- **An Overleaf plan with Git integration.** InfiniteLeaf syncs through Overleaf's Git bridge, which
  needs a paid Overleaf plan (or an institutional one that includes it).
- **An Overleaf Git token.** In Overleaf: Account Settings ▸ Git integration ▸ create a token, then
  copy it. InfiniteLeaf keeps it in the macOS Keychain, never in a file.
- **Your Overleaf sign-in.** The app asks you to sign in to overleaf.com once, in a window of its own,
  to read the project's name (and, if you turn them on, its comments).

## Link a project
Projects screen (or File) ▸ **Open from Overleaf…**. The dialog has four steps; each one unlocks when
the one before is done.
1. **Token.** Click **Add token…** and paste your Overleaf Git token.
2. **History repo.** Click **Set up history…** and choose a folder for InfiniteLeaf's history
   (`~/InfiniteLeaf` is suggested). Linked projects live there. Do not pick a folder inside iCloud
   Drive, Google Drive, Dropbox or OneDrive; the app refuses them.
3. **Project.** Paste the project's address from your browser (`https://www.overleaf.com/project/…`).
   The dialog looks up the project's name on Overleaf. If it asks, click **Sign in to Overleaf…**, sign
   in, and close that window. **Never push (read-only)** is ticked: the project only receives
   Overleaf's changes until you allow pushing (step 2 below).
4. **Open.** The app checks the token and the address, then opens the project (in a new window if
   another project is already open). If the
   project is already in InfiniteLeaf, the dialog offers **Open it** instead of making a second copy.

Your project is now a folder on your disk that follows Overleaf. The **sync button** in the top bar
(it shows the state, for example "● synced") opens the sync panel.

## Sync by hand
Until you turn on automatic sync (below), you decide when things move. In the sync panel:
1. **Check now** asks Overleaf for your coauthors' latest changes.
2. **Apply changes from Overleaf** brings them into your copy. If you and a coauthor edited the same
   lines, the app stops and shows the conflict instead of choosing for you.
3. **Allow pushing** (once per project): new links only receive, so nothing of yours reaches Overleaf
   until you allow it.
4. **Review and push…** shows exactly what would be sent, file by file, with anything risky for
   comments flagged (a renamed file, a whole-file reformat, a large rewrite). Leave files out if you
   want, then push.

## Automatic sync with Overleaf every few seconds
Set this up once per project. Both directions are off until you turn them on.
1. **Link the project.** Projects screen ▸ **Open from Overleaf…** (token, history folder, project address).
2. **Allow pushing.** New links never push. Click the sync button in the top bar to open the sync
   panel, then **Allow pushing**.
3. **Choose how often.** In the same panel, **Sync with Overleaf every**: 1 second to 5 minutes
   (default 5 minutes). Short intervals apply only while the InfiniteLeaf window is in front; in the
   background it checks once a minute. Below 15 seconds Overleaf may ask the app to slow down, and the
   panel then says "Overleaf asked us to slow down · next try …".
4. **Bring coauthors' edits in.** Tick **Apply Overleaf changes automatically**.
5. **Send your edits out.** Tick **Send my edits to Overleaf automatically**. Your edits go once you
   have stopped typing for 10 seconds (or the interval, if longer). The app always takes Overleaf's
   latest changes first, merges, then sends.
6. **What waits for you.** Renaming or moving a file, reformatting a whole file, rewriting more than
   30 % of a file at once, and deleting a file on Overleaf are not sent automatically. The panel says
   "needs a look"; press **Review and push** for those. Everything else goes out on its own, as it would
   in Overleaf's editor.
7. **Offline.** Edits wait and go out, after a merge, once you are back online.

The panel's header shows "Live · every N s" while this is on.

## Comments and review
- **Overleaf comments and review**: comments and suggestions beside the text, a new comment from a
  selection, reply/resolve/accept, and actions made offline are sent when you reconnect.
- **History with Overleaf**: Overleaf's versions and labels next to your own, labels on any earlier
  version (also on Overleaf when the version matches exactly), compare with an Overleaf version.

### Turn comments on, view, reply, resolve, accept
For a project linked to Overleaf. Off until you turn it on.
1. **Turn it on.** Settings ▸ Connections ▸ Overleaf: tick **Show Overleaf comments and suggestions**
   to see them. To act on them too, also tick **Allow accepting, rejecting, resolving and replying on
   Overleaf from InfiniteLeaf**. Both are marked unofficial: they use Overleaf's website, not its Git
   bridge, and may stop working when Overleaf changes its site.
2. **Sign in to overleaf.com once**, in the app's own window: Settings ▸ Connections ▸ Overleaf ▸
   **Browse Overleaf…**. If you are not signed in, the margin says so and offers **Open Overleaf
   review**; sign in there, then press **Check now**.
3. **See the comments.** Click **Review**. It is in the file bar above the editor, on the right; when
   the window is narrow it is tucked under the **⋯** button (More file actions) at the right end of
   that bar (the **⋯** then shows a dot). **Review** on the left rail opens the same margin on its
   Overview tab. Until step 1 is done, or in a project not linked to Overleaf, both are greyed out:
   click one and it says what is missing, with a button that takes you there.
   A margin opens beside the text: **Current file** shows each comment level with the text it is on;
   **Overview** lists every file's comments and suggestions (click one to jump there). **Check now**
   reads Overleaf again; otherwise it refreshes with the sync interval.
4. **Reply and resolve.** Click a comment's card: type in **Reply** (Enter sends, Shift+Enter is a new
   line) or press **Resolve**. Resolved comments are under **Resolved (N)** at the bottom, with **Reopen**.
   **Edit or delete your own:** a message's **⋯** menu has **Edit** (Save / Cancel; ⌘Enter saves, Esc
   cancels) and **Delete**. Delete on the first message of a thread you started removes the whole
   thread, after you confirm, as on Overleaf; resolved threads you started can be deleted from
   **Resolved (N)**. Other people's messages cannot be edited or deleted from InfiniteLeaf.
5. **Suggestions (tracked changes).** Each one has **Accept** and **Reject**; a group has
   **Accept all** / **Reject all**. A reject finishes with your next push.
6. **New comment.** Select text in a `.tex` file: an **Add comment** button appears above it. Type the
   comment and press **Comment**.
7. **Suggesting (track changes).** The **Editing ▾ / Reviewing ▾** switch in the file bar turns
   Overleaf's track changes on or off for you, as in Overleaf: in **Reviewing**, the edits you send to
   Overleaf arrive there as suggestions your coauthors accept or reject. The switch works only when **both** switches in step 1
   are on **and** the project may push (sync panel ▸ **Allow pushing**; new links start read-only), and
   you are signed in. Otherwise it is greyed out; click it to see what is missing and go fix it. Like
   Review, it can be under **⋯** (More file actions) in a narrow window.
8. **Offline.** Actions you take offline wait ("Queued — sent when Overleaf answers") and go out when
   Overleaf answers again.
