# 3x3 Report Generator

Paste your weekly notes and get a 3-column table: **3 goals accomplished, 3 blockers, 3 objectives for next week**. Edit any cell, then copy for email, copy as Markdown, or print to PDF.

Single static file (`index.html`), no build step, no dependencies.

## Deploy on GitHub Pages

1. Create a new repo (for example `3x3-report`) and add `index.html` and this `README.md` to the root.
2. In the repo, go to **Settings > Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch", choose `main` and `/ (root)`, then Save.
4. After a minute, the site is live at `https://<your-username>.github.io/<repo-name>/`.

Share that link with coworkers.

## How generation works

Four ways to use it, from least to most setup:

- **Sort my notes (default, no AI, no key):** runs entirely in the browser. Write one item per line and the page sorts each line into Goals, Blockers or Objectives, then keeps the top 3 of each.
  - Tags make it reliable: `done:` or `+` = goal, `blocked:` or `issue:` = blocker, `next:` or `>` = objective, `!!` = top priority.
  - Untagged lines are sorted by keywords ("shipped", "fixed" = goal; "waiting on", "stuck" = blocker; "will", "kick off" = objective).
  - Lines that did not make the top 3 appear below the table as buttons you can click to swap in.
  - If you paste last week's objectives, anything not matched by a goal this week is added as a "Carryover:" objective.
  - Empty slots show "(need input)". Always review the table before sending, since keyword sorting is simple and will occasionally misfile a line.
- **Blank table:** type directly into the cells. No AI, no key.
- **Copy prompt:** the page builds a ready-made prompt from your notes. Paste it into Claude (or any chat app) and copy the table back.
- **Generate with Claude:** each user pastes their own Anthropic API key under "Claude API settings". The browser calls the API directly, so notes never touch any server except Anthropic's. The key is only saved locally if "Remember key" is checked.

## Weekly log

- Click **Save to log** under the table to store that week's report. Saving the same week label again replaces it.
- The next time you open the page, **last week's objectives fill in automatically** (from the most recent saved week that isn't the current one), so unfinished items are flagged as "Carryover:". Your name is remembered too.
- The Log section lists every saved week with **Open** and **Delete**, plus **Copy log as Markdown** (handy for quarterly reviews), **Export backup** and **Import backup** (JSON), and **Clear log**.
- The log is stored in your browser's local storage on that device only. It is never uploaded, never shared with coworkers who use the same link, and it will not follow you to another browser or computer. Clearing site data erases it, so export a backup now and then.

## Notes for sharing with a team

- GitHub Pages is static, so **never hardcode an API key** in `index.html`. Anyone who opens the page could read it.
- If you want coworkers to generate without their own keys, put a small proxy in front of the API (Cloudflare Worker, Vercel or Netlify function) that holds the key server-side, then point the `fetch` URL in `index.html` at it. Add auth or rate limiting there.
- Check your company's policy on sending work notes to AI services before rolling this out.
