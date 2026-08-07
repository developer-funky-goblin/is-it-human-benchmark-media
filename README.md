# is-it-human-benchmark-media

Benchmark media for the [Is It Human](https://github.com/developer-funky-goblin/is-it-human) evaluation
harness: self-hosted images, video, and text for items whose `label_source` is a generator run in-house or
an original of known provenance, rather than a published dataset with its own stable URL.

## Why this is a separate repo

The harness's own schema and writer live in the main repo, in a committed SQLite database. This repo holds
only the media bytes, kept separate so the main repo's clone size doesn't grow with the benchmark set.

This repo is the archive of record: every addition or replacement is a reviewable pull request, and
`retired_at` on a `benchmark_items` row is set rather than deleting a file, so run history stays intact.

## Serving

Published via [GitHub Pages](https://developer-funky-goblin.github.io/is-it-human-benchmark-media/), which
is what `benchmark_items.url` points at for self-hosted items. `.nojekyll` disables the default Jekyll
build, since this repo is a plain file tree, not a site.

## Layout

```
images/<benchmark_item_id>.<ext>
video/<benchmark_item_id>.<ext>
text/<benchmark_item_id>.<ext>
```

Every file is named by the `benchmark_items.id` it belongs to. A replacement item gets a new id and a new
file; the old file is left in place for run history, matching the harness's own replace-don't-overwrite rule.
