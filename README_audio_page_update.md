# MelKoop audio page update

This updated `audio.html` supports the current filenames shown in your folders.

It automatically matches examples by removing prefixes:

- `Clean1` -> key `1`
- `enh_1` -> key `1`
- `noisy_1` -> key `1`
- `enh_p257_403` -> key `p257_403`
- `p257_403` -> key `p257_403`

Therefore, you do not need to rename the files.

## How to use

1. Copy `audio.html` into the root of your repository:

   `C:\Users\engs2653\Documents\GitHub\MelKoop\audio.html`

2. Replace the old `audio.html`.

3. Open GitHub Desktop.

4. Commit message:

   `Update audio page for current filenames`

5. Click `Commit to main`.

6. Click `Push origin`.

7. Wait 1-3 minutes.

8. Open:

   `https://drchk.github.io/MelKoop/audio.html`

## Important

The page will skip files that do not have a matching triplet.

From your screenshots, `p257_259` appears only in the Noisy folder. It will be skipped unless you also add matching Enhanced and Clean files.
