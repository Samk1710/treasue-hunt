
# 🌌 Ophiuchus: The 13th Zodiac of Songs


A personalized music deduction game powered by Spotify OAuth, Google Gemini 2.5 Flash for intelligence and narrative, real-time TTS audio generation, and MongoDB session persistence.
Players explore four interactive rooms to collect clues and identify a hidden Cosmic Song derived from their own Spotify listening history.

## Technical Architecture

### Core Stack

* Framework: Next.js 14 (App Router, Server Actions, API Routes)
* Language: TypeScript
* Authentication: Spotify OAuth 2.0 via NextAuth.js
* Music Data: Spotify Web API (top tracks, saved tracks, recently played, audio features)
* AI Services: Google Gemini 2.5 Flash

  * Text generation for riddles and scoring
  * Flash Preview TTS for emotional audio scenes
* Database: MongoDB with Mongoose ODM
* Media Storage: Cloudinary for audio files
* Audio Processing: PCM-to-WAV conversion pipeline for serverless compatibility
* Deployment: Serverless functions on Vercel

---

## Game Flow

### Phase 1 — Big Bang Initialization

Triggered after Spotify login.

Backend processing:

1. Token refresh and session validation handled by NextAuth
2. Concurrent Spotify API requests gather player music behavior
3. Weighted scoring combines recency and frequency of listens
4. Selection algorithm chooses:

   * One Cosmic Song
   * Two Intermediary Songs for room clues
5. Gemini generates a cryptic opening hint
6. Full session state stored in MongoDB

Performance target: Under seven seconds from login to game start.

---

## Room Systems

### Nebula — Riddle of Echoes

Interpretive deduction gameplay.

Technical details:

* Gemini produces a poetic riddle describing an Intermediary Song
* Spotify Track ID check ensures accurate guessing
* Limited attempts enforced via MongoDB atomic writes
* Successful guesses unlock a thematic clue toward the Cosmic Song

---

### Cradle — The Veiled Origin

Artist-focused questioning and reasoning.

Technical details:

* Gemini responses drawn strictly from verified Spotify metadata
* Prompt rules prevent exposing artist name directly
* Final guess validated through normalized string comparison
* Rewards a deeper artist-linked clue

---

### Comet — Flash of the Past

Memory-based challenge with time pressure.

Technical details:

* Lyric snippet shown briefly on screen (ten seconds)
* One guess attempt validated against Spotify IDs
* AI fallback generates stylistically accurate lyric if needed
* Correct guess yields a partial lyric clue from the Cosmic Song

---

### Aurora — The Voice of Light

Emotional song inference using audio-driven clues.

Technical details:

* Gemini creates a short emotional narrative scene
* Scene synthesized to WAV and uploaded to Cloudinary
* URL cached in MongoDB to prevent regeneration
* Player guesses a song based on emotional tone
* Gemini evaluates emotional similarity on a numeric scale
* High score unlocks a mood-based clue for the Cosmic Song

---

## Authentication and Session Management

* Spotify OAuth handled via NextAuth with automatic token refresh
* JWT used for server-side session validation
* MongoDB stores room progression, scores, and audio references
* Atomic operations ensure consistency during rapid interactions

---

## Spotify Integration Strategy

Primary data sources:

* Saved songs
* Recently played tracks
* Medium-term top tracks
* Audio feature embeddings
* Artist metadata including genres and popularity

Derived analytics:

* Listening frequency weighting
* Emotional profile clustering (valence, energy, danceability)
* User mood and genre patterns

Used to ensure clue relevance and difficulty balance.

---

## Engineering Highlights

* Integrated text and audio generation with Gemini
* Emotional similarity scoring for accurate song-matching gameplay
* Cloud-hosted TTS audio with global performance optimization
* Weighted selection algorithm ensures Cosmic Song is personally meaningful
* Time-bound interactions enforce real challenge dynamics
* Minimal storage of playback data for strict privacy compliance
* Serverless infrastructure supports scaling without configuration
* Adaptive clue generation aligns difficulty with player performance

---

## Future Plans

* Faster clue generation through speculative prefetching
* Spotify Web Playback SDK for in-game audio
* Analytics-driven calibration of difficulty levels
* Mobile and voice-driven input features
* Synchronized multiplayer game mode

---

## License

MIT Licensed. Free to use and modify.

---


