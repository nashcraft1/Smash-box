# Smash Box — support site

Three pages in six languages. No dependencies, nothing to install: what is
in this folder is what gets served.

    index.html          hero screenshot, 3-step how to play, features, screenshots
    how-to-play.html    full rules, point values, themes, awards, tips
    privacy.html        privacy policy (App Store Connect requires one)

The pictures — app icon, header, screenshots in each language — are added by
`../build_website.py`, which leaves every page's own wording alone. Edit the
text in the HTML directly; re-run the script after changing the layout or
the screenshots. It is safe to run any number of times.

    python3 metadata/build_website.py

    index.html          how-to-play.html          privacy.html
    de/  es/  fr/  ja/  zh-Hans/   (same three pages each)
    assets/style.css

English is at the root so the bare domain works; every page carries a language
switcher, and each language's pages link only to each other.

## Hosting it on GitHub Pages

1. Create a repository — `smashbox-site` will do.
2. Copy the **contents of this folder** into it (not the folder itself, or every
   URL gains a `/website/` in the middle).
3. `git add . && git commit -m "Smash Box support site" && git push`
4. Repository → Settings → Pages → Source: *Deploy from a branch*, branch
   `main`, folder `/ (root)`.

A minute later it is live at `https://<user>.github.io/smashbox-site/`.

## What to put in App Store Connect

Both URLs are set per language, so point each store locale at its own pages.
With `<base>` standing in for the address above:

| Store locale | Support / Marketing URL | Privacy Policy URL |
|---|---|---|
| en-US, en-GB, en-AU | `<base>/` | `<base>/privacy.html` |
| de-DE | `<base>/de/` | `<base>/de/privacy.html` |
| es-ES | `<base>/es/` | `<base>/es/privacy.html` |
| fr-FR | `<base>/fr/` | `<base>/fr/privacy.html` |
| ja | `<base>/ja/` | `<base>/ja/privacy.html` |
| zh-Hans | `<base>/zh-Hans/` | `<base>/zh-Hans/privacy.html` |

**The URLs currently on the listing are dead.** Every locale still points at
`http://web.me.com/nashcraft1/...` — MobileMe, which Apple shut down in 2012.
Replacing them is the one part of this that is not optional.

## Before it goes up

The privacy policy gives **nashcraft1@gmail.com** as the contact, because that
is the account address. If you would rather publish something else, it appears
once per language file:

    grep -rl nashcraft1@gmail.com .

The policy describes the app as it actually is — no collection, no analytics,
no ads, no network calls to you, iCloud key-value sync only. If the app ever
gains an SDK that phones home, the policy has to change with it.
