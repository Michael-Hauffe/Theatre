# Ghost Matinee

A 3D haunted movie theater you can visit with friends as ghosts. The host loads a movie (or shares their screen) and it streams to everyone in the room, with synced play/pause/seek, shared subtitles, chat bubbles, and a lobby with a concession stand.

Play it here: https://michael-hauffe.github.io/Theatre/

## Known good version

**v1.0, confirmed working on November 1, 2026.**
Saved as the branch [`v1.0-working`](https://github.com/Michael-Hauffe/Theatre/tree/v1.0-working) (commit `96160b4`). Leave that branch alone; new work goes on `main`.

Confirmed working in that version:
- Hosting and joining rooms with a 5-letter code or invite link
- Host-only movie file, streamed to guests with picture and sound
- Synced play, pause and seeking for everyone
- Host's subtitles (.srt, .vtt, .ass) shared with all guests
- Host screen sharing onto the theater screen
- High-quality stereo audio for guests
- Hallways, lobby and concession stand, including the employee area behind the counter
- Buying, holding, eating and drinking snacks with Ghost Bucks
- Hide HUD button

If a later change breaks something, the v1.0 code can be restored from that branch.

## Hosting tips

- Host from Chrome or Edge. Guests can use any browser.
- The host's upload speed limits how many guests get smooth video. Three or four is comfortable on typical home internet.
- To share sound during a screen share, tick "Share system audio" (Windows) or share a single Chrome tab (Mac).
