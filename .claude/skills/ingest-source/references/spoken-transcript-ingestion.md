# Ingesting Spoken Transcripts (YouTube/Video, Podcasts, Spoken Course Lectures)

Applies when the source is a transcript of someone speaking: a YouTube or video transcript,
a podcast episode, or a recorded/spoken course lecture.

## What's structurally different about spoken material

Speech is composed in real time, not revised before delivery, and that changes how ideas
show up in the transcript:

- **Ideas repeat and get revisited non-linearly.** A speaker will state a point, move on,
  and come back to it later ("like I said earlier..."), restate it with a different example,
  or build it up gradually across several separate moments rather than once in one place.
  Unlike written text, sequential order in the transcript does **not** reliably map to the
  logical structure of the argument.
- **Segmentation needs to consolidate, not just follow order.** Don't mechanically write one
  page per timestamp range or one page per chunk-in-sequence. Find where the same topic
  actually lives across the whole transcript — even if it's scattered across three separate
  moments — and pull it together into one coherent page, the way you'd want to explain the
  point to someone who wasn't following along in real time.
- **Preserve genuine content, not disfluency.** Filler words, false starts, verbal tics,
  and mid-sentence self-corrections are artifacts of speaking, not content — they don't need
  preserving under the depth-preservation rule (§4 point 2). What does need preserving:
  genuine caveats, real examples, and reasoning the speaker actually built out loud, even if
  it took them a roundabout path to get there.

## Multi-speaker sources

Podcasts, interviews, and panel-style videos have more than one speaker. Attribute claims to
the person who actually said them — don't let a host's framing or question get conflated
with a guest's answer, and don't flatten "someone on this podcast said X" into an
unattributed claim in the wiki page.

## Transcription quality

Auto-generated transcripts (the common case for YouTube) carry real transcription-error
risk: misheard words, garbled technical terms, missing punctuation that changes meaning. A
passage that's clearly garbled or ambiguous because of transcription quality — not because
the speaker's own point was unclear — is a legitimate trigger for an `ambiguous` confidence
tag rather than `extracted`. Don't guess at what a garbled passage "probably" meant and
write it as if it were clean.

## Segmentation and page count

Similar to books in that a long-form video or podcast episode can develop several genuinely
distinct concepts worth their own pages — but check for redundancy first, since spoken
content restates itself more than written text does; don't let three restatements of the
same point become three separate pages. A short clip or single-topic video, on the other
hand, may only warrant one page, same as a short article.

## Citation

Cite the video/episode title, channel or show, and the transcript file in `source`. Include
the URL if available — video sources are usually easier to re-locate later than a static
text file, so a URL is worth capturing even though it's not strictly required by §2.
