# The Upshot: Archive Explorer

I transcribed ten years of Ultiworld Disc Golf's podcast *The Upshot*, plus the
subscriber-only *Inside the Circle* segments, and built a small tool for looking at what
the show actually talks about. 868 episodes, about 876 hours of audio, 2016 to 2026.

**[View the explorer](https://dgoodenough.github.io/upshot-archive/)**

## What's in it

**What the show talks about.** A word cloud of every player, course, tournament, and brand
the hosts mention, sized by how often it comes up. You can filter by category, or by who
said it.

**Mentions over time.** Click any name to chart it across the decade, and compare up to six
at once. There's a per-episode toggle, which matters because recent years have far more
episodes than early ones.

**Who's on the mic.** Every voice I could identify, ranked by hours of speech or by number
of episodes.

**This week in Upshot history.** What aired around today's date, across all ten years.

## How I built it

Transcription runs locally with faster-whisper (large-v3), diarization with pyannote.audio.
The interesting problem was speaker identity: diarization tells you *someone* spoke, not
who. I clustered x-vector embeddings across all 868 episodes, then worked out who each
cluster was from episode titles, host introductions, and self-introductions. That got 98%
of all speaking time attributed across 130 named people.

The hardest cases were conflations, where two guests with similar voices merge into one
cluster. Those needed splitting by hand, and I learned the hard way that re-clustering
silently undoes the splits, so the fixes live in an overrides table keyed on something
stable.

Entity mentions come from a curated disc golf gazetteer matched across every segment. The
site itself is one self-contained HTML file. No dependencies, no build step, no external
requests.

## What's published here

Aggregate statistics only. Mention counts, speaking-time totals, episode titles, air dates.

There are no transcripts, no audio, and no excerpts of the show in this repository or on
the site. The full-text search in my local copy runs against an index that stays on my
machine.

## A note on scope

This is an unofficial fan project. It isn't affiliated with Ultiworld or produced with
them.

*The Upshot* is Ultiworld's copyrighted work, and the episode titles and names in this
analysis belong to their respective owners. If you're with Ultiworld and want something
changed or taken down, open an issue and I'll handle it quickly.

## License

MIT, covering the code only. It doesn't extend to the podcast content the code describes.
