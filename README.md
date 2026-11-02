# Ghost Matinee

A 3D haunted movie theater you can visit with friends as ghosts. Anyone in the room can load a movie (or share their screen) and it streams to everyone, with synced play/pause/seek, shared subtitles, chat bubbles, and a lobby with a concession stand.

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

## What's new since v1.0 (not yet confirmed)

- **One projector for the room.** Anyone can press Load movie. Everyone else's Load movie turns gray, and the person showing the movie gets a Stop movie button that clears it for everyone. Screen sharing works the same way and is now open to everyone, not just the host.
- **Eating in first person.** Your snack shows in your hand and moves to your mouth with each bite or sip.
- **Throwing food.** Hold Throw (or T) to charge: a tap is a gentle toss, 2 seconds is a hard throw, 6 seconds is full power. Food bounces off walls, seats, counters and ghosts, everyone sees it, and it disappears after 30 seconds.
- **Mortimer**, the concession ghost behind the counter. Talk to him with the button, R, or by clicking him.
- **Lobby posters**: 20 original ghost movies, six shown at a time, picked randomly per room. Add your own (below).
- **Show Shortcuts** button that shows the shortcut list only while held.
- **Debug screen**: hold the ` key (top left of the keyboard) to see live details on the room, the projector, picture and sound, your snacks and performance. Press **P** to copy it all to the clipboard so you can paste it into a message. The sound status moved from the main screen into the debug screen.

If the picture or sound doesn't reach someone, have them hold ` and press P, then paste what was copied. The "Receiving" section shows whether their computer is connected to the projector and how many frames have arrived.

## Admin commands

Anyone in the room can type these in the chat box. Commands that change things are carried out by the host's browser for everyone; a guest's command works just the same.

| Type this | What it does |
|---|---|
| `/admin show commands` | Shows this list on your screen |
| `/admin list posters` | Numbers of the six poster frames (also on brass plaques under each frame) and of every poster image |
| `/admin set poster 2 to image 3` | Puts image 3 in frame 2, for everyone |
| `/admin reset poster 2` | Frame 2 goes back to its random pick |
| `/admin shuffle posters` | A new random set of posters |
| `/admin reset posters` | Back to the room's original posters |
| `/admin reset movie` | Stops the movie or screen share; Load movie works again for everyone |
| `/admin pause` | Pauses the movie for everyone |
| `/admin clear food` | Removes all thrown food |
| `/admin announce Showtime!` | A big message across everyone's screen |
| `/admin mortimer Welcome, folks!` | Mortimer says it |
| `/admin list people` | Who's in the room |
| `/admin kick Ben` | Removes someone (they can rejoin with the code). The host can't be kicked |
| `/admin summon` | Brings everyone to where you are |
| `/admin give everyone 20` | Gives everyone 1 to 100 Ghost Bucks |

## Adding your own lobby posters

1. Put your poster images in the [`posters`](posters) folder. JPG, PNG, WebP or GIF all work. Portrait images shaped like a movie poster (2:3, for example 600×900 pixels) look best; other shapes get their edges trimmed to fit the frame.
2. Open [`posters/posters.json`](posters/posters.json) and add each file name to the `images` list, in quotes, separated by commas:

   ```json
   {
     "keepBuiltInPosters": true,
     "images": ["my-poster.jpg", "another one.png"]
   }
   ```

3. Commit the changes. GitHub Pages updates the site within a minute or two.

Your images join the random rotation with the built-in ghost posters. To show only your own, change `"keepBuiltInPosters": true` to `false`. File names are case-sensitive and must match exactly, and images must be in the `posters` folder itself, not a subfolder. If an image can't be found, a built-in poster takes its place.

## Hosting tips

- Load movies and share screens from Chrome or Edge. Everyone else can watch in any browser.
- The upload speed of whoever loads the movie limits how many friends get smooth video. Three or four is comfortable on typical home internet.
- To share sound during a screen share, tick "Share system audio" (Windows) or share a single Chrome tab (Mac).
- The room host's browser keeps the room together. If the host leaves, the room closes.

## For developers

See [CLAUDE.md](CLAUDE.md) for house rules (including: comment all code heavily) and how the code is organized. The whole game is in `index.html`, with an overview at the top of the file.
