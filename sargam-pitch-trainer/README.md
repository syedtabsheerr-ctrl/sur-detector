# Sargam Pitch Trainer

A static, browser-only singing practice tool. It plays a local backing track, compares live microphone pitch against a timed melody reference, plots both on the same time/pitch chart, and exports session measurements.

## Run locally

1. Download/extract the folder.
2. Open `index.html` in a local web server. Microphone permission usually requires HTTPS or `localhost`; opening the file directly may block microphone access.
3. Easiest local server with Python:

   ```bash
   python -m http.server 8000
   ```

4. Open `http://localhost:8000`.

## Deploy to GitHub Pages

1. Create a GitHub repository, for example `sargam-pitch-trainer`.
2. Upload `index.html` (and this README) to the repository root.
3. Open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
5. Open the published HTTPS URL. Allow microphone access when prompted.

No backend, build step, API key, or package install is required.

## Use it

1. Upload the backing track from your device.
2. Load a melody reference as JSON, CSV, or MIDI. Or click **Load a short original demo melody** to test the chart and microphone flow.
3. Headphones are optional. You can sing while the song plays through speakers. For speaker use, keep the mic closer to your mouth than the speakers and lower speaker volume if the detector follows the original singer. The app requests browser echo cancellation to help reduce speaker bleed, but support and results vary.
4. Enable the microphone, play the track, and sing. Your pitch trace appears against the target notes.
5. Use the alignment offset if the reference timing and track timing differ slightly.
6. Record your microphone performance separately with **Record my voice**; the browser downloads the recording when you stop.
7. Export comparison samples as CSV for further analysis.

## Reference formats

### JSON

```json
{
  "title": "My melody",
  "bpm": 90,
  "notes": [
    { "start": 0.00, "end": 0.45, "note": "A3" },
    { "start": 0.50, "end": 0.90, "note": "C4" },
    { "start": 1.00, "end": 1.40, "note": "D4" }
  ]
}
```

### CSV

```csv
start,end,note
0.00,0.45,A3
0.50,0.90,C4
1.00,1.40,D4
```

Times are seconds from the start of the reference. Note names use scientific pitch notation, e.g. `A2`, `C4`, `F#3`, `Bb3`. The app also accepts MIDI files. For multi-track MIDI, it asks which track to load; choose the melody/vocal track, not a full accompaniment track.

## Accuracy notes and limitations

- The app does **not** infer a complete vocal melody from an MP3. It needs a timed melody reference (JSON/CSV/MIDI) to know the intended note at each moment.
- MIDI tracks may contain accompaniment or chords. Select a melody-only track where possible.
- Speakers and headphones are both supported; headphones are optional. With speakers, the microphone can also pick up the backing track. The app requests browser echo cancellation, which may reduce this bleed but is device-dependent. Move the mic closer to your mouth than the speakers and lower playback volume if needed.
- The built-in YIN-style estimator is a practical lightweight browser implementation, not studio-grade source separation. Vibrato, breathiness, distortion, background noise and octave errors can affect readings.
- The chart and pitch score compare the detected fundamental frequency with the reference pitch at the same playback time. They do not rate tone quality, diction, emotion or overall musicianship.
- The reference alignment offset can compensate for a small timing shift. It is not automatic dynamic time warping.
- Audio, microphone stream and practice recording are processed locally; this app has no upload endpoint. Browser recording support varies by browser.
- Saved melody references use local browser storage on that device. Backing audio and practice recordings are not retained after reload unless you keep the downloaded files.

## Browser requirements

A modern browser with Web Audio API, `getUserMedia`, and (for microphone recording) `MediaRecorder`. Microphone access requires HTTPS or localhost.