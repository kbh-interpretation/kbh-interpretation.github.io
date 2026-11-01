# Копенгагенская интерпретация: the podcast's feed

«Копенгагенская интерпретация», подкаст о Дании и мире. Feed: <https://kbh-interpretation.github.io/feed.xml>

- `show.toml` and `episodes.toml`: the show and its episodes.
- `build_feed.py`: writes `feed.xml` and `index.html` from them (Python 3.11+, standard library only). It is the same
  file as in `soviema/soviema.github.io`; keep the two in step.
- `art/`: the show cover and the episode art (3000×3000 JPEG, RGB), served by GitHub Pages.
- The audio files are in the repository `kbh-interpretation/audio-1`, served by GitHub Pages at
  `https://kbh-interpretation.github.io/audio-1/`. Pages gives them an audio MIME type, which Apple's player needs;
  GitHub release assets do not play in it.

## Adding an episode

1. Add the audio to the audio repository, commit and push. Use AAC in `.m4a` (Apple's encoder, `aac_at`) or MP3.
   - The file must be under 100 MiB, GitHub's limit per file. At 128 kb/s that is about 1 h 48 min; encode longer
     episodes at 112 kb/s (about 2 h 03 min) or 96 kb/s.
   - When `audio-1` nears 900 MB (Pages' limit is 1 GB per site), start `audio-2`.
2. Put its art in `art/ki-epNN.jpg`.
3. Add an `[[episode]]` to `episodes.toml`:
   - a new random `guid` (`python3 -c "import uuid; print(uuid.uuid4())"`);
   - `audio`: `audio-1/ki-epNN.m4a`;
   - `length`: the file's size in bytes;
   - `duration`: `HH:MM:SS`.
4. Run `python3 build_feed.py`, read `git diff feed.xml`, then commit and push.

Never change an episode's `guid`, file name or date once it is out: podcast apps identify episodes by the guid.

Episodes #1–#9.2 were moved here from Spotify for Creators on 2026-10-31 and 2026-11-01.
- GUIDs, dates and descriptions are unchanged.
- The audio of #4 (MP3 320 kb/s, 180 MB) and #7 (AAC 128 kb/s, 111 MB) was re-encoded to AAC at 128 and 112 kb/s to
  fit the 100 MiB limit.
- The audio of #3 and #8 is encoded at 128 kb/s from the show's own mixes of their first release, which are longer than
  the later versions on Spotify: 1:03:27 instead of 1:00:54 and 1:16:00 instead of 1:07:31.
- The other audio files are unchanged.
- The art of #5 was converted from grayscale to RGB (Apple's artwork rule); the picture is the same.
