# Life Log app

An installable web app (PWA) version of the Life Log Claude page: log mood, study time and habits, see trends and tips, and play the daily quiz. It works offline and opens full screen from the home screen.

## Where data lives

- **Your entries, habits and quiz results are saved only on the device** (browser storage). Nothing personal is sent to GitHub. Use *Edit habits and goal → Download backup* to keep a copy, and *Restore backup* on a new phone.
- The app does not share entries with the Claude page. Each keeps its own log.

## Files

- `index.html`: the app (same code as the Claude page; outside Claude it skips the database and the AI question writer)
- `sw.js`: the service worker. It caches the app for offline use and fetches the quiz briefing network-first. Bump `VERSION` after changing any app file.
- `manifest.webmanifest`, `icons/`: what the phone needs to install the app
- `quiz/briefing.json`: the current-events quiz questions (news, politics, stocks). A copy of the Claude page's `quiz/briefing` database document.

## Updating the quiz briefing

Write `quiz/briefing.json` as `{ "asOf": "YYYY-MM-DD", "items": [ { "id", "c", "q", "o", "w", "s" } ] }`, where `c` is `news`, `politics` or `stocks`, `o` lists the options with the correct one first, `w` explains the answer and `s` names the source. At least 3 items are needed. The app picks it up the next time it opens.

## Testing locally

```bash
powershell -NoProfile -ExecutionPolicy Bypass -File serve.ps1 8788
```

Then open http://localhost:8788. A phone can only install the app from an HTTPS address, such as GitHub Pages.
