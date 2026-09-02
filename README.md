# Disappointing Bands

Search any band or artist → Claude looks up the lineup, then web-searches each member for public allegations, convictions, and scandals (sex crimes involving minors flagged highest). Green PASS = nothing found; flagged members expand to show what, the legal status (convicted / charged / civil suit / alleged / rumor), and source links.

Single-file app: `index.html` + `icon.png`. No server, no build.

## Setup
1. Open the app, tap ⚙, paste an Anthropic API key (console.anthropic.com → Settings → Keys). It's stored only in that browser's localStorage and sent only to api.anthropic.com.
   - **Personal (identity-linked) keys** also need a Workspace ID (`wrkspc_...`) in the second field — find it under Organization settings → Workspaces in the Console. Workspace-scoped keys don't need it.
2. Search. Results cache locally, so repeat searches are free/instant; "Search again" forces a fresh run.

## Run locally
```
python -m http.server 4395 --directory C:\Users\james\Claude\disappointing-bands
```
(or the `disappointing-bands` entry in `.claude/launch.json`)

## iPhone
Host it anywhere static (GitHub Pages / Netlify), open in Safari, Share → Add to Home Screen. Runs full-screen with the broken-heart icon.

## Cost / model
Lineup lookup runs on `claude-sonnet-5` (cheap, fast). Member research runs on `claude-opus-5` with the `web_search_20260209` server tool — up to 5 searches per member, with three mandatory queries (allegations / arrested-charged-lawsuit / grooming-underage) baked into the prompt and the queries echoed back so a PASS shows what was searched. 4 members researched in parallel. A fresh 5-member band runs roughly $0.60–0.90; a 12-member roster ~$1.80; cached repeats are free.
To trade reliability for cost, change `RESEARCH_MODEL` in index.html to `claude-sonnet-5` (~half the price; it missed a widely-reported 2022 allegation in testing, which is why research went back to Opus).
