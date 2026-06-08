# MelKoop audio examples page instructions

## Files/folders expected

Place `audio.html` in the root of the repository:

```text
MelKoop/
├── index.html
├── README.md
├── audio.html
└── Audio/
    ├── Noisy/
    ├── Enhanced/
    └── Clean/
```

The folder names are case-sensitive on GitHub Pages. Use exactly:

```text
Audio/Noisy
Audio/Enhanced
Audio/Clean
```

For each example, the same filename must exist in all three folders, for example:

```text
Audio/Noisy/sample_01.wav
Audio/Enhanced/sample_01.wav
Audio/Clean/sample_01.wav
```

## Edit required

Open `audio.html` and edit this line:

```javascript
const GITHUB_USER = "YOUR_GITHUB_USERNAME";
```

Change it to your GitHub username, for example:

```javascript
const GITHUB_USER = "yourusername";
```

Keep:

```javascript
const GITHUB_REPO = "MelKoop";
const BRANCH = "main";
```

unless your repository or branch has a different name.

## Add a link from the main page

In `index.html`, add this button/link somewhere near the top:

```html
<a class="button" href="audio.html">Listen to audio examples</a>
```

If your page does not have a button style, use:

```html
<p><a href="audio.html">Listen to audio examples</a></p>
```

## GitHub Desktop

1. Copy `audio.html` into the root of your `MelKoop` repository.
2. Make sure your audio folders are in `MelKoop/Audio/Noisy`, `MelKoop/Audio/Enhanced`, and `MelKoop/Audio/Clean`.
3. Open GitHub Desktop.
4. You should see the new/changed files.
5. Commit message: `Add audio examples page`.
6. Click `Commit to main`.
7. Click `Push origin`.
8. Wait 1-3 minutes for GitHub Pages to update.
9. Open `https://YOUR_GITHUB_USERNAME.github.io/MelKoop/audio.html`.
