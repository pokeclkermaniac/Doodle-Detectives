# Doodle Detectives

**Describe it. Doodle it. Book 'em.**

A multiplayer party game for phones, for 2–8 players. One player is the **Witness** and describes a goofy suspect. Everyone else is a **Sketch Artist** and draws against the clock. Then comes the lineup, a drumroll and the reveal.

## How to play

1. A random player becomes the **Witness** and sees a suspect card: a mugshot, a nickname, a funny crime and a difficulty tag.
2. The Witness describes the suspect, out loud or in the in-app clue chat, without saying the 2–3 **"You can't say"** words.
3. Every **Sketch Artist** draws on a mugshot board before the timer runs out (15/30/60/90s).
4. Artists who hear a forbidden word tap **Busted!** and type the word. If it's on the card, the Witness loses a point.
5. **Lineup:** each artist picks which of 4 lookalike suspects they drew.
6. **Reveal:** drumroll, card flip, and side-by-side comparison. The Witness picks the best sketch.
7. Everyone is Witness twice. Highest score wins, and awards go to Most Wanted Artist, Star Witness, Eagle Eye and Loose Lips.

### Scoring (competitive)
| Event | Points |
|---|---|
| Artist picks the right suspect in the lineup | +2 artist, +1 Witness |
| Witness picks your sketch as the best | +2 artist |
| Witness gets busted saying a forbidden word | −1 Witness |

**Co-op mode** pools everything into a team score.

## Features

- Room codes, up to 8 players; late arrivals join the next round; the host role moves to another player if the host leaves
- Unlimited procedurally generated suspects (hair, eyewear, mouths, hats, extras), each with a nickname and crime
- Card packs: Classic, Halloween, Office, Fantasy, Animals
- Difficulty: Easy / Medium / Hard / Mix
- Optional chaos rules: wrong hand, blind draw, one continuous line
- Drawing tools: marker in 3 sizes, eraser, undo, and a paint bucket, all using **24-bit hex colors** (color picker, hex input, and 16 presets taken from the suspect generator)
- Flip-card reveal with drumroll, end-of-game "rap sheet" gallery, shareable side-by-side images
- Music and sound effects (with a mute button), vibration, dark mode that follows the phone
- Unlockable visual styles: Mugshot (default), Noir, Cartoon, Notebook
- **Practice solo:** memorize a suspect, draw it from memory, then pick it out of the lineup

## Running it

It's a single self-contained file, `index.html` (HTML + CSS + JS, no build step), hosted on GitHub Pages.

**Multiplayer** uses Firebase Realtime Database with anonymous sign-in, so players never create accounts: they just enter a name and a 4-letter room code.

- Config: `FIREBASE_CONFIG` near the multiplayer section of `index.html` (Firebase web config values are public by design).
- Security rules: `database.rules.json`. Paste these into Realtime Database → Rules.
- Required Firebase setup: **Authentication → Anonymous** enabled, and a **Realtime Database** created.

How it works: the room creator is the host and broadcasts the game state; players send their moves; sketches travel in chunks. Rooms live under `rooms/dd-XXXX` with `presence` (who's here, removed automatically on disconnect) and short-lived `events` (cleaned up after about 20 seconds).

When the page runs as a Claude artifact on claude.ai, it uses Claude's built-in live rooms instead. **Practice solo** works anywhere, offline included.

## Roadmap

- iOS and Android apps
- AI-illustrated suspects
- Public matchmaking
- Custom suspects
- Ads
- Recording the reveal as a video
