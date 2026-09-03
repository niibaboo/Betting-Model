# Goal Watch — Setup Checklist

Over 2.5 / BTTS predictor for Premier League, Bundesliga, Eredivisie,
Ligue 1, and Primeira Liga. Combines each home team's home scoring/
conceding record with each away team's away record, recency-weighted,
normalized against the league average, run through Poisson math.

## Step 1 — Get a free API key
Go to https://www.football-data.org/client/register
- Sign up (email + password), verify your email
- Your API key appears on your account dashboard — copy it
- No cost, no card required

## Step 2 — Set up the repo
Either reuse your existing GitHub repo or create a new one. Add these
two files in this exact layout:
```
your-repo/
├── goal_watch.py
└── .github/
    └── workflows/
        └── goal_watch.yml
```

## Step 3 — Add the API key as a GitHub secret
- Repo → **Settings** → **Secrets and variables** → **Actions**
- **New repository secret**
- Name: `FOOTBALL_DATA_API_KEY` (must match exactly — the workflow
  reads this exact name)
- Value: paste the key from Step 1
- Save

## Step 4 — Enable GitHub Pages
- Repo → **Settings** → **Pages**
- Source: **Deploy from a branch**, Branch: **main**, Folder: **/docs**
- Save

## Step 5 — Run it once manually
- Repo → **Actions** tab → "Update Goal Watch Report" → **Run workflow**
- This takes **8-12 minutes** — that's expected, not a bug. The free
  API tier is capped at 10 requests/minute, and the script deliberately
  paces itself to stay under that limit rather than getting blocked.

## Step 6 — Find your live page
Settings → Pages will show your URL, something like:
`https://<you>.github.io/<repo>/goal_watch.html`

## What to expect
- Shows every upcoming fixture (next 7 days) in the 5 leagues
- Each fixture: home team's home L5 (scored/conceded), away team's
  away L5 (scored/conceded), expected goals for each side, P(Over 2.5),
  P(BTTS Yes)
- Runs automatically once a day (edit the cron line in the workflow
  file to change the time) — or trigger manually anytime from Actions

## One honest caveat
BTTS assumes the two teams' scoring is statistically independent,
which isn't quite true in real matches (teams that go up big tend to
ease off). Trust Over/Under 2.5 numbers here more than BTTS numbers.
