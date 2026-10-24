# 🛡️ SheShield — Women Safety Companion
*recHERsion 2026 submission*

> One tap. Trusted contacts. Live location. Evidence. Works offline as an installable PWA — no app store, no sign-up, no data leaves the device.

## Problem
Women face harassment and threats in transit, campuses and public spaces. In an emergency, unlocking a phone, opening an app and typing a message is too slow — and many existing safety apps need sign-ups, subscriptions or send data to servers.

## Solution
SheShield is a **privacy-first, zero-install safety web app** that automates the whole emergency response in one tap.

| Feature | What it does |
|---|---|
| 🆘 **One-tap SOS** | 5-sec cancel window → siren + vibration + live GPS link to all trusted contacts via WhatsApp/SMS |
| 🎙️ **Auto evidence** | Records audio the moment SOS fires; downloadable from incident log |
| 📍 **Live location** | `watchPosition` keeps the shared link updated while SOS is active |
| 🧭 **Safe Journey check-in** | Timer for a trip; if you don't tap "I'm safe", SOS auto-triggers (dead-man switch) |
| 📞 **Fake call** | Realistic incoming call with a voice (Web Speech API) to exit uncomfortable situations |
| 🤳 **Shake-to-SOS** | Discreet trigger via DeviceMotion when the screen can't be used |
| 🏥 **Nearby help + helplines** | One-tap 112 / 1091 / 181 / 100 and maps for police, hospitals, pharmacies |

## Tech
Vanilla HTML/CSS/JS (no build step) · Geolocation API · MediaRecorder + getUserMedia · Web Audio · Web Speech · DeviceMotion · Vibration API · localStorage · Service Worker + Web App Manifest (installable PWA).

## Architecture
```
 Trigger (button | shake | journey timer expiry)
        │
   5s Countdown ──cancel──▶ safe
        │
   fireSOS() ─┬─ Web Audio siren + vibration
              ├─ Geolocation.watchPosition → live Maps link
              ├─ MediaRecorder → audio evidence (local blob)
              └─ Deep links (wa.me / sms:) → every trusted contact
        │
   stopSOS() → incident log (localStorage) + evidence download
```
**Privacy by design:** contacts, logs and recordings stay in the browser. No accounts, no servers, no tracking.

## Run it
```bash
# any static server (HTTPS or localhost needed for GPS + mic)
python3 -m http.server 8000   # open http://localhost:8000
```
**Live demo:** enable GitHub Pages (Settings → Pages → main / root) → `https://<username>.github.io/<repo>/`

## Demo flow
1. Contacts tab → add a trusted contact
2. SOS tab → press SOS → let countdown finish → siren, live link, WhatsApp/SMS buttons, recording
3. Journey tab → "15 seconds (demo)" → don't check in → auto SOS
4. Fake call tab → ring → accept → voice speaks

## Roadmap
FastAPI + Firebase backend for server-side live-tracking page · background SMS via Twilio · AI risk heatmap from community reports · safe-route suggestions · Hindi/Kannada voice trigger ("Bachao") · wearable integration.

## Limitations (honest)
Browsers can't silently send SMS/WhatsApp — the user taps send on pre-filled messages. Background tracking when the tab is closed needs a native/PWA-push backend (roadmap).

## Team
<Your name(s)> — NITK Surathkal
