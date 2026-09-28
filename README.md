# Smart-Search Floor Manager: 3D Map, Countdown & Squad Share

A single-file web app (no build step, no dependencies) for finding free classrooms:
**Search → see the room on the map → check how long it's free → claim it → call the squad.**

## Features
- Tilted 3D floor map (toggle 2D) with floor selector and animated floor switch
- Room colors: 🟢 available, 🟡 available soon (class ends within 15 min), 🔴 occupied
- Live HH:MM:SS countdown from the timetable (green >30 min, yellow 10–30, red <10); the room flips to occupied at 00:00:00
- AI-style natural-language search ("AC room on the ground floor for 2 hours") that highlights matches with ⭐
- Filters: AC, minimum capacity, available only
- Claim Room (confirmation, saved in localStorage, never edits the timetable)
- Call the Squad: pre-filled WhatsApp link (`wa.me`) plus Copy Message fallback
- Demo mode: set any time and everything updates; "Use Current Time" returns to real time
- Responsive (desktop, tablet, mobile)

## Run
Open `index.html` in a browser.

## Deploy on GitHub Pages
```bash
git init && git add . && git commit -m "Smart-Search Floor Manager"
git branch -M main
git remote add origin https://github.com/<you>/smart-floor-manager.git
git push -u origin main
```
Then go to **Settings → Pages → Deploy from branch → main / root**.

## Use your own timetable
Edit the `DATA` section at the top of the script. The `ROOMS` and `TT` objects are generated there. Replace them with real data in this shape:
```js
ROOMS.push({id:"IST 309", fl:3, cap:40, ac:true});
TT["IST 309"] = [{s:14.5*3600, e:15.5*3600, c:"Machine Learning"}]; // seconds since midnight
```
Everything (status, colors, countdown, search, messages) is computed from `TT`.

## Key functions
`getRoomStatus`, `getNextClass`, `getRemainingTime`, `calculateCountdown`, `getAvailableUntil`, `claimRoom`, `generateWhatsAppMessage`, `shareRoom`, `highlightRoomOnMap`
