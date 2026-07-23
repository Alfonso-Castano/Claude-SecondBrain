# Ingesting Written Text (Books, Articles, Written Course Material)

Applies when the source is prose someone wrote: a book, an article, a blog post, or
text-based course material (a written module, a set of course notes).

## What's structurally different about written text

Written prose is composed, not spontaneous. An author revises before you see it, which
means arguments tend to be built deliberately: a claim gets set up, supported with
evidence or an example, and then concluded — once, in one place, in a considered order.
This matters directly for two of §4's steps:

- **Depth preservation (§4 point 2) is tested hardest here.** Because the argument is
  already built cleanly, it's tempting to extract just the conclusion — that's the whole
  failure mode the depth-preservation rule exists to catch. If a chapter spends three pages
  building toward a framework with a worked example, the wiki page needs to show that
  argument being built, not just state the framework.
- **Segmentation should usually follow the author's own structure** (chapters, sections,
  headers) rather than inventing new groupings — the author already did useful
  organizational work; don't discard it. A distinct chapter or major section usually earns
  its own page or its own clear subsection within a page, per the new-page-vs-edit rule
  (§3.1).

## Chunking a long source

Books (especially audiobook transcripts pasted as one unbroken block of text, no chapter
breaks) can be long enough that reading the whole thing in one pass isn't practical. Chunk
along natural topic or argument boundaries — where the source itself shifts from one
framework or concept to the next — not by arbitrary token count. Splitting mid-argument
risks writing a page that only captures half of a built point, which is exactly the
flattening failure self-verification (§4 point 4) is supposed to catch — better to avoid
causing it than to rely on catching it after the fact.

## Segmentation and page count

Expect the page count to scale with how much distinct, page-worthy content the source
actually contains, not with the source's length:

- **Books** typically earn several distinct pages — one per major framework or concept the
  book develops, since a book usually covers enough ground for that to be genuinely
  distinct material (this happened with the Hormozi ingestion: one book, seven pages, each
  covering a different framework the book built).
- **Articles** are usually much narrower in scope — a single focused argument or a small
  handful of claims. Resist over-splitting a short piece into artificially many pages just
  to mirror the book pattern; one or two pages is often the honest right size.
- **Written course material** is already modular by the source's own design (a syllabus,
  numbered modules, lessons) — mirror that existing structure directly rather than
  re-deriving your own segmentation. Citations should be granular enough to trace back to a
  specific module or lesson, not just "the course" as a whole. Only the actual taught
  content (concepts, frameworks, explanations) belongs in the wiki — not exercises or
  assignments, unless a specific exercise itself demonstrates a technique worth capturing.

## Citation and honest caveats

Cite the specific title, author (where known), and the raw file in `source`. If the source
is an audiobook narration or a condensed edition rather than the full print text, note that
as an honest limitation — a narration may have trimmed print-only material (footnotes,
appendices, sidebars), and the wiki page shouldn't imply completeness it doesn't have.
