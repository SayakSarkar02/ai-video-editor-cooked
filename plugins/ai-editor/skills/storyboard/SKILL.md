---
name: storyboard
description: Breaks a video idea or script into a numbered shot list with recording tips. Use when the job type is "storyboard" or the user says "plan my video", "storyboard", "shot list", or "what clips should I record".
license: MIT
compatibility: Claude Code on Mac, Windows or Linux. Stdlib only (writes one JSON file).
---

# Storyboard

The user wrote a video idea or script on the Storyboard page. Turn it into a concrete shot list they can record on their phone right now.

## Input

The job's `args.idea` is the user's text — anything from a one-line concept to a full script.

## Output

Write a JSON file to `$LIBRARY/storyboards/<job-id>.json` where `$LIBRARY` is the AI_EDITOR_LIBRARY
folder (default: `~/Movies/AI Editor` on Mac, `~/Videos/AI Editor` on Windows/Linux). Create the
`storyboards/` folder if it does not exist.

The JSON has this shape:

```json
{
  "name": "standing-desk-reel",
  "clips": [
    {
      "title": "Hook",
      "description": "Close-up of you sitting down looking tired, then standing up energised. Camera at desk height.",
      "duration": "3-5s",
      "tips": "Film this twice: once slouched, once standing tall. Quick cut between them."
    },
    {
      "title": "The problem",
      "description": "Wide shot of your old setup — messy desk, bad posture.",
      "duration": "4-6s",
      "tips": "Slightly messy is fine, it should feel relatable."
    }
  ]
}
```

## Rules

1. **3 to 8 clips.** Short-form reels work best with 3-8 distinct shots. More than 8 is overwhelming.
2. **Each clip is one camera setup.** The user records each clip separately and drops it into the slot.
3. **Concrete, actionable.** Say exactly what to point the camera at, where to stand, what to say. Never vague.
4. **Duration estimates.** Give a range like "3-5s" for each clip — helps the user know how long to record.
5. **Tips field.** Practical recording advice: framing (close-up / wide / POV), lighting notes, what to say vs show.
6. **Name field.** A short kebab-case name for the video (used as a folder name). Derived from the idea.
7. **Hook first.** The first clip should always be the hook — the most attention-grabbing moment.
8. **CTA last.** If the idea implies a call to action, make it the last clip.

## Steps

1. Read the job args from the `wait` command output. The `idea` field has the user's text.
2. Think about what makes a good short-form video for this idea. Consider the hook, the story arc, and the payoff.
3. Write the JSON to `$LIBRARY/storyboards/<job-id>.json`.
4. Mark the job done.

## Library path

```bash
python3 -c "from pathlib import Path; import os, json; d=json.load(open(os.path.expanduser('~/.ai-video-editor/state.json'))); print(d['root'])"
```
