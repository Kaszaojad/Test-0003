# J.A.R.V.I.S. for Android

Voice assistant for Android (built for Xiaomi 13T Pro / HyperOS, works on other phones, Android 8+).
Talks to you live through the Gemini Live API and can use the phone through tools.
All data lives in a normal visible folder: `/storage/emulated/0/J.A.R.V.I.S./`

## 1. Build the APK (pick ONE way)

### A) GitHub Actions (no installs, ~5 minutes)
1. Create a free account at github.com, then New repository (Private is fine), name it `jarvis-android`.
2. Upload the CONTENTS of this folder (including the hidden `.github` folder and `gradle/`) to the repo:
   `git init && git add . && git commit -m init && git branch -M main && git remote add origin <repo-url> && git push -u origin main`
3. Open the repo > Actions tab > "Build APK" > wait for the green check.
4. Open the finished run > Artifacts > download `JARVIS-apk` (a zip containing `app-debug.apk`).

### B) Android Studio (on the PC)
1. Install Android Studio, choose File > Open and select this folder, let Gradle sync finish.
2. Build > Build Bundle(s) / APK(s) > Build APK(s). The file is `app/build/outputs/apk/debug/app-debug.apk`.

## 2. Install over the cable
1. Phone: Settings > About phone > tap the OS version 7 times; then Additional settings > Developer options > turn on USB debugging (and "Install via USB" if present).
2. Plug in the cable, set the USB mode to "File transfer".
3. Copy `app-debug.apk` to the phone (e.g. the Download folder).
4. On the phone open it from Files, allow "Install unknown apps" for the file manager, tap Install (if Play Protect warns, choose Install anyway).
   Or from the PC with ADB: `adb install -r app-debug.apk`

## 3. First start
1. Open J.A.R.V.I.S., tap the gear, paste your Gemini API key (https://aistudio.google.com/apikey), set your name, SAVE.
2. Tap START. Grant: All files access (switch ON for J.A.R.V.I.S., then go back), Microphone, Notifications, Contacts.
3. Tap START again and talk. The folder `J.A.R.V.I.S.` now exists in the phone's internal storage.
4. Xiaomi / HyperOS: Settings > Apps > Manage apps > J.A.R.V.I.S. > Battery saver = No restrictions, Autostart = ON,
   and under Other permissions allow "Display pop-up windows while running in the background" (needed so it can open apps while the screen is off or the app is minimised).

## 4. Data folder (open it from the PC in This PC > phone > Internal storage > J.A.R.V.I.S.)
- `prompt.txt` the assistant's instructions (edit freely)
- `config/api_keys.json` optional: `{"gemini_api_key":"...","assistant_name":"...","user_name":"..."}` (same format as the desktop app)
- `memory/long_term.json` long-term memory (you can copy the desktop Mark 57 file here), `memory/reminders.json`
- `chats/` daily Markdown transcripts, `notes/`, `files/`, `downloads/`, `logs/jarvis.log`

## 5. What it can do
web search, weather, time, open apps/links/YouTube/maps, reminders (exact-time notifications), clock timers/alarms,
flashlight, volume, battery, storage, media keys, settings pages, contact lookup, prepare calls/SMS/WhatsApp (you press send),
read/write files in its folder (delete asks you on screen), long-term memory.

## 6. Troubleshooting
- Connection errors: see `logs/jarvis.log`. A wrong key shows as a closed connection right after START.
- It hears itself on the loudspeaker: keep "Mute mic while I speak" ON, or use headphones and turn it OFF to be able to interrupt.
- Models change: the Live model name is editable in Settings.
