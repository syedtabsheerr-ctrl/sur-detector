# Sargam Pitch Trainer v2

A static browser-based Sargam-first singing tutor. Paste or upload Sargam, choose your starting Sa including octave, and compare your live microphone pitch to the selected swara. The live tuner and live pitch chart work without loading any notation or song.

## GitHub Pages

This app lives in the sargam-pitch-trainer folder in the sur-detector repository. GitHub Pages should serve it at:

https://syedtabsheerr-ctrl.github.io/sur-detector/sargam-pitch-trainer/

## Quick start

1. Open the app over HTTPS.
2. Click Enable microphone and allow access.
3. Sing a steady vowel such as aa. Your note and frequency should appear even before you load Sargam.
4. Paste notation or upload a TXT, JSON or CSV Sargam file.
5. Choose Sa and its octave, such as C3, D3 or A2.
6. Select a swara, sing it, and compare your note and frequency with the target.
7. Use Target tone to hear a locally generated reference pitch.
8. Use Next/Previous for manual practice or Auto sequence to advance at a selected fixed interval.

An optional backing-track upload is available for accompaniment only. The app does not extract a melody from the backing audio.

## Roman swara convention

S = Sa; r = komal Re; R = shuddha Re; g = komal Ga; G = shuddha Ga; M = shuddha Ma; m = tivra Ma; P = Pa; d = komal Dha; D = shuddha Dha; n = komal Ni; N = shuddha Ni.

Prefix a dot for a lower octave, for example .S. Suffix an apostrophe for a higher octave, for example S'. Hindi swara names are also accepted: सा रे ग म प ध नि. Mark komal or tivra notes with (k) or (t), for example रे(k), ग(k), म(t).

Example practice sequence:

S R G M P D N S'
S' N D P M G R S

The parser reports unrecognized tokens so you can correct the notation before practising. It is important to verify the swara convention used by your source because different notation systems may use different symbols.

## Input formats

- TXT: Sargam tokens separated by spaces or bars.
- JSON: an object with a notation or sargam string, or a notes array of strings / objects with swara, token, sargam or note fields.
- CSV: one swara token in the first column of each row.

Plain Sargam is an ordered sequence; it normally does not contain reliable rhythm. Auto sequence therefore uses the fixed note length you choose. For rhythm-accurate practice, a timed note format will be added separately.

## What it measures

- A lightweight YIN-style browser pitch detector estimates the dominant voice fundamental frequency.
- Frequency is converted into equal-tempered note name and Sargam label relative to your chosen Sa.
- The current target frequency is calculated from Sa plus the swara semitone offset.
- Pitch difference is displayed in cents. The initial match tolerance is +/- 50 cents.
- The live chart plots microphone pitch independently of Sargam and song loading.
- Optional voice recording downloads a local WebM/Opus file where supported.

## Known limitations

- This version does not infer the melody from an MP3; supplied Sargam is the reference.
- The initial scale uses 12-tone equal temperament. Raga-specific Shruti/intonation is not implemented.
- The detector estimates one dominant fundamental. Vibrato, breathiness, room noise, harmonics and loud accompaniment can affect readings.
- Speaker playback is allowed and headphones are optional. The mic can also hear the singer in the backing track, so lower speaker volume if the pitch detector follows the recording.
- Microphone access requires HTTPS or localhost. If input level stays very low, check browser permission and your operating-system microphone input selection/volume.
- No backend is used. Microphone audio and practice recordings are processed locally in the browser.

## Local testing

From this folder run:

python -m http.server 8000

Then open http://localhost:8000 in your browser.
