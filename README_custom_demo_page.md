# MelKoop custom demo page update

This package gives you a custom public page name:

https://drchk.github.io/MelKoop/demos.html

It also hides the browser download button on the audio players using:

controlsList="nodownload noplaybackrate"
oncontextmenu="return false"

Important: this does NOT fully prevent downloading. GitHub Pages is a public static website. Anyone who can play a public audio file can still technically download it from browser developer tools or the direct file URL.

## How to use with GitHub Desktop

1. Copy `demos.html` into:

   C:\Users\engs2653\Documents\GitHub\MelKoop\demos.html

2. Open GitHub Desktop.

3. Commit message:

   Add custom audio demo page

4. Click `Commit to main`.

5. Click `Push origin`.

6. Wait 1-3 minutes.

7. Open:

   https://drchk.github.io/MelKoop/demos.html

## To remove index.html from the URL

Use:

https://drchk.github.io/MelKoop/

instead of:

https://drchk.github.io/MelKoop/index.html

## To remove drchk.github.io from the URL

You need a custom domain that you own, for example:

https://melkoop.example.com

Then configure the custom domain in GitHub:

Repository → Settings → Pages → Custom domain
