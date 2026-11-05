# Ghost Matinee

A 3D haunted movie theater you can visit with friends as ghosts. Anyone in the room can load a movie (or share their screen) and it streams to everyone, with synced play/pause/seek, shared subtitles, chat bubbles, and a lobby with a concession stand.

Play it here: https://michael-hauffe.github.io/Theatre/

## Known good versions

Each confirmed version is saved as its own branch. Leave those branches alone; new work goes on `main`. If a later change breaks something, the code can be restored from the branch.

### v2.0, confirmed working on November 1, 2026 (latest)

Saved as the branch [`v2.0-working`](https://github.com/Michael-Hauffe/Theatre/tree/v2.0-working). Everything in v1.0, plus:

- **One projector for the room.** Anyone can press Load movie or Share screen. Everyone else's Load movie turns gray, and the person showing gets Stop movie, which clears it for everyone. The room host's browser referees who gets the projector.
- **Fresh start between showings.** Whenever the projector is freed (Stop movie, Stop sharing, `/admin reset movie`, or the projectionist leaving), every computer discards the old picture and sound connections and sets them up from scratch.
- **Self-repair.** If a screen share or playing movie shows no picture for 8 seconds, or a playing movie freezes for 8 seconds, that computer reconnects to the projectionist by itself (up to 3 tries in a row, then it shows a notice).
- **Eating in first person.** Your snack shows in your hand and comes to your mouth with each bite or sip.
- **Throwing food.** Hold Throw (or T) to charge: a tap is a gentle toss, 2 seconds is a hard throw, 6 seconds is full power. Food bounces off walls, seats, counters and ghosts, everyone sees it, and it disappears after 30 seconds.
- **Mortimer**, the concession ghost behind the counter. Talk to him with the button, R, or by clicking him.
- **Lobby posters**: 20 original ghost movies as JPG files, six shown at a time, picked randomly per room, with numbered frames. Add, remove or replace them like any image (below).
- **Admin commands** typed in chat, for everyone in the room (below).
- **Show Shortcuts** button that shows the shortcut list only while held.
- **Debug screen**: hold the ` key to see live details on the room, the projector, picture and sound, snacks and performance. Press **P** to copy it all so you can paste it into a message.

If the picture or sound doesn't reach someone, have them hold ` and press P, then paste what was copied. The "Receiving" section shows whether their computer is connected to the projector and how many frames have arrived.

### v1.0, confirmed working on November 1, 2026

Saved as the branch [`v1.0-working`](https://github.com/Michael-Hauffe/Theatre/tree/v1.0-working) (commit `96160b4`):

- Hosting and joining rooms with a 5-letter code or invite link
- Host-only movie file, streamed to guests with picture and sound
- Synced play, pause and seeking for everyone
- Host's subtitles (.srt, .vtt, .ass) shared with all guests
- Host screen sharing onto the theater screen
- High-quality stereo audio for guests
- Hallways, lobby and concession stand, including the employee area behind the counter
- Buying, holding, eating and drinking snacks with Ghost Bucks
- Hide HUD button

## New since v2.0 (not yet confirmed)

- **Skip buttons:** −10s and +10s next to Play (or J and L) skip the movie for everyone. Grayed out during a screen share.
- **Full view:** press **M** to watch just the movie, filling the whole screen like a normal video player (with subtitles). Press **M** or **Esc** to go back to the theater. The controls fade after 3 seconds without moving the mouse.
- **Pick up thrown food:** float next to it and press **X**, the Pick up button, or click it. It goes back in your hands with the bites it had left, and disappears for everyone.
- **More from Mortimer:** about 20 new everyday lines and reactions to being hit with food. Now and then (about 1 talk in 10) he lets slip something about his past; those lines are in their own list, `NPC_BACKSTORY`, in `index.html`.
- **Sharper picture for bigger groups:** whoever shows the movie uploads a separate copy to each viewer, so with several people the bandwidth runs thin. Each viewer's copy now drops to a smaller picture size (1080, 720, 540 or 360 lines) when its bandwidth can't keep the full size sharp, and steps back up when it can. The debug screen shows each viewer's bandwidth, picture size and what's limiting it.
- **Invisible ghosts:** Hide HUD (or H) also hides names and chat bubbles, fades every ghost (you and Mortimer included) out completely, and hides snacks held in hands, so nobody blocks the movie. Thrown snacks stay fully visible.
- **Lobby TVs:** two TVs high on the back wall, either side of the concession counter, show whatever is on the big screen (with subtitles), so you can keep watching while you get snacks.
- **Relay servers for tough networks:** if two players' internet connections can't link up directly (the black screen with the connection stuck on "checking"), the video now goes through a free relay server (Open Relay by Metered, plus PeerJS's own). It's only used when needed. For a private relay, put your own Metered credentials address in `TURN_API_URL` in `index.html`.
- **The room survives the host leaving:** the next person in line (in the order people joined) becomes the host automatically and everyone reconnects to them. A movie shown by anyone other than the old host keeps playing.
- **Reconnecting after a dropout:** if your connection to the room blips, the game shows "Reconnecting…" and gets you back in for up to 90 seconds, keeping your ghost, money and snacks. If the person showing the movie drops out, the projector waits 10 seconds for them before freeing up.
- **Passing the picture along:** whoever shows the movie sends it straight to at most 3 viewers; each of them passes it on to up to 2 more. This lets bigger groups watch without overloading one person's upload. Change the number with `/admin direct viewers 3`.
- **Personal subtitle size:** the Subs: M button (or - and =) changes subtitle size just for you, and it's remembered. Hide subs was already just for you.
- **Emotes:** press 1 to 5 to scream, laugh, cry, clap or shush. Everyone sees the bubble and your ghost acting it out.
- **Mortimer remembers you:** he greets returning players by name, notices how long it's been, knows your usual snack, counts repeat orders and remembers who throws food at him. The memory lives in your browser.
- **Update check:** if your browser is showing an old saved copy of the game, a bar offers a Refresh.

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
| `/admin direct viewers 3` | How many viewers get the movie straight from whoever shows it (1 to 10); everyone else gets it passed along by another viewer |

## Lobby posters

Every poster is an ordinary image file in the [`posters`](posters) folder, listed in [`posters/posters.json`](posters/posters.json). The 20 ghost-movie posters that come with the game are JPGs there too, so you can open, edit or replace any of them in an image editor. Each room shows six of them, picked at random (everyone in the same room sees the same six), and only those six are downloaded.

**To add your own poster:**

1. Put the image in the `posters` folder. JPG, PNG, WebP or GIF all work. Portrait images shaped like a movie poster (2:3, for example 600×900 pixels) look best; other shapes get their edges trimmed to fit the frame.
2. Add its file name to the `images` list in `posters/posters.json`, in quotes, with a comma after the line before it:

   ```json
   {
     "images": [
       "the-last-matinee.jpg",
       "...the other built-in posters...",
       "my-poster.jpg"
     ]
   }
   ```

3. Commit the changes. GitHub Pages updates the site within a minute or two.

**To remove a poster** from the rotation, delete its line from the list (you can leave the file in the folder). **To replace one**, save your image over the old file with the same name.

The order of the list sets the image numbers used by `/admin set poster 2 to image 3`. The file name becomes the poster's name in `/admin list posters` (`my-poster.jpg` shows as "My Poster"). File names are case-sensitive and must be directly in the `posters` folder, not a subfolder. If a listed file is missing, its frame shows a "Coming soon" card.

**Making more ghost posters in the same style:** open [`tools/poster-maker.html`](https://michael-hauffe.github.io/Theatre/tools/poster-maker.html). It draws the 20 built-in posters with code and has a download link under each. To change a title, tagline or colors, edit the `GHOST_POSTERS` list in that file.

## Hosting tips

- Load movies and share screens from Chrome or Edge. Everyone else can watch in any browser.
- The upload speed of whoever loads the movie limits how many friends get smooth video. Three or four is comfortable on typical home internet.
- To share sound during a screen share, tick "Share system audio" (Windows) or share a single Chrome tab (Mac).
- The room host's browser keeps the room together. If the host leaves, the next person in line takes over as host automatically.

## For developers

See [CLAUDE.md](CLAUDE.md) for house rules (including: comment all code heavily) and how the code is organized. The whole game is in `index.html`, with an overview at the top of the file.
