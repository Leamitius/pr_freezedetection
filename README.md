# Freeze Detector — Adobe Premiere Pro Extension

Automatically detects frozen frames in a video and cuts them out of the timeline.

---

## Requirements

- Adobe Premiere Pro 2019 or newer
- Windows 10 / 11

No Python or FFmpeg installation required — everything is bundled.

---

## Installation

### Step 1 — Copy the extension folder

Copy the entire `FreezeDetector` folder to:

```
C:\Program Files (x86)\Common Files\Adobe\CEP\extensions\
```

The result should look like this:

```
C:\Program Files (x86)\Common Files\Adobe\CEP\extensions\FreezeDetector\
    freeze_detector.exe
    index.html
    CSInterface.js
    CSXS\
        manifest.xml
    js\
        panel.js
    jsx\
        main.jsxbin
```

> You may need administrator rights to copy files into Program Files.

---

### Step 2 — Enable unsigned extensions (registry entry)

Adobe Premiere Pro blocks unsigned extensions by default. You need to add a registry entry once to allow them.

**Option A — Automatic (recommended)**

Open PowerShell as Administrator and run:

```powershell
reg add "HKCU\Software\Adobe\CSXS.12" /v PlayerDebugMode /t REG_SZ /d 1 /f
```

> If you are on an older version of Premiere Pro, try `CSXS.11` or `CSXS.10` instead of `CSXS.12`.

**Option B — Manual via regedit**

1. Press `Win + R`, type `regedit`, press Enter
2. Navigate to: `HKEY_CURRENT_USER\Software\Adobe\CSXS.12`
3. Right-click the folder → New → String Value
4. Name it `PlayerDebugMode`, set the value to `1`

---

### Step 3 — Open the panel in Premiere Pro

1. Launch Adobe Premiere Pro
2. Go to **Window → Extensions → Freeze Detector**

The panel will appear. On first launch it may take a few seconds to load.

---

## Usage

1. Open a sequence with the source video on **Track 1**
2. In the Freeze Detector panel, set the **Temp / Output Folder** (defaults to your system temp folder)
3. Select the **offset** (0 = even clips, 1 = odd clips)
4. Click **Run Freeze Detection**

The extension will analyse the video, detect frozen frames, cut them out, and arrange the remaining clips on Track 2.

---

## Troubleshooting

- **Panel does not appear in the menu** — make sure the registry entry was added and Premiere Pro was restarted afterwards.
- **Panel appears but does nothing** — check the log file in your temp folder (`_freeze_log.txt`) for error details.
- **FPS conversion takes a long time** — the extension converts the video to 30 fps before analysis if needed. This is normal for long videos.