# GitHub Profile Card

A dynamic, auto-updating GitHub profile SVG card that showcases your projects, languages, contribution stats, and more.

**[中文](README.md)**

<div align="center">
  <img src="https://raw.githubusercontent.com/2982136527/2982136527/main/profile-card.svg" width="960" alt="Profile Card" />
</div>

## Features

- **Tech Arsenal** — Auto-detects your top 12 languages and displays them as orbiting icons around a glowing sun
- **Project Grid** — Lists all your repositories with descriptions, languages, and last push dates
- **Activity Dashboard** — Shows contribution count, repo count, followers, and a streak indicator
- **Contribution Snake** — Animated snake path through your contribution grid
- **Auto-updates** — Runs every 6 hours via GitHub Actions

## Quick Start

### 1. Create your profile repo

Create a new repository with the **same name as your GitHub username** (e.g., if your username is `octocat`, create `octocat/octocat`).

### 2. Copy the files

Copy these files into your new repo:
- `.github/workflows/update-profile.yml`
- `hero-banner.svg` (the header image)

### 3. (Optional) Add a Personal Access Token

If you want **private repos** included in the stats:

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Fine-grained tokens](https://github.com/settings/tokens?type=beta)
2. Create a token with `repo` scope (or `metadata:read` for just language data)
3. Go to your profile repo's **Settings > Secrets and variables > Actions**
4. Add a secret named `PAT` with your token value

### 4. Trigger the workflow

Go to your repo's **Actions** tab, select "update profile", and click **Run workflow**.

### 5. Update your README

Replace your `README.md` with:

```markdown
<div align="center">
  <img src="profile-card.svg" width="960" alt="Profile Card" />
</div>
```

## Customization

### Changing the color theme

The default theme uses a pink/purple/cyan palette. To change it, search and replace these colors in the workflow:

| Color | Usage |
|-------|-------|
| `#FF69B4` | Primary pink |
| `#D4A5FF` | Secondary purple |
| `#00D4FF` | Accent cyan |
| `#00ff88` | Success green |
| `#0a0a1a` | Background |

### Changing the schedule

Edit the `cron` line in the workflow to change update frequency:

```yaml
on:
  schedule:
    - cron: "23 */6 * * *"  # Every 6 hours at :23
```

### Adding custom language icons

Edit the `LANG_MAP` object in the workflow to add or change language display config:

```javascript
'YourLang': { abbr: 'YL', color: '#FF0000', textColor: '#fff' },
```

## How It Works

1. **GitHub Actions** runs on schedule (every 6 hours) or manual trigger
2. Fetches your repos, languages, contributions, and follower data via GitHub API
3. Generates an SVG with:
   - Dynamic tech arsenal based on your actual top languages
   - Project grid from your repos
   - Dashboard with real stats
   - Contribution snake from your calendar
4. Commits the updated SVG to your repo

## FAQ

**Q: Why don't I see private repos?**
A: You need to set up a Personal Access Token (PAT) as described above.

**Q: Can I use this without the arsenal section?**
A: Yes, just remove the `arsenalSection` from the workflow and adjust the height calculations.

**Q: The SVG looks cached / old**
A: GitHub caches raw SVG files. Add `?v=timestamp` to the image URL in your README, or wait a few minutes.

## License

MIT — use however you like!
