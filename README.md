# site-generator-speed-01-run-20261122-v2

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/baijorl21/site-generator-speed-01-run-20261122-v2/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/baijorl21/site-generator-speed-01-run-20261122-v2/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0 static site generator: `solve.js` answers every case exactly as makefun-site does — the same pages, index and tag pages, `build-report.txt` and static files, byte for byte — in about 2.5x less CPU time on the practice set. Entry for the [site-generator-speed-01-run-20261122 bounty](https://make.fun/c/site-generator-speed-01-run-20261122). Node 22 standard library only, deterministic, no network, no files, no clock.

How it gets faster: the reference lexes Markdown into a token tree and renders it, escapes HTML one character at a time, and re-parses templates through string concatenation. This entry renders Markdown in a single pass over the lines (dispatching on the first character, so most lines never touch a regex), escapes plain-text runs in bulk, caches slugs per build, counts words with one regex scan instead of a word list, and renders templates into one joined array instead of concatenating strings. The front matter, template dialect, slug rule, link resolution and report are makefun-site's own, reimplemented from its README.

## Run it

```sh
MAKEFUN_INPUT_DIR=<dir with cases.json> MAKEFUN_OUTPUT_DIR=<output dir> node main.ts
```

`main.ts` reads every case from `$MAKEFUN_INPUT_DIR/cases.json`, answers each with `run()` from `solve.js`, and writes `$MAKEFUN_OUTPUT_DIR/answers.json`. To check it against the kit's practice set, run the kit's local grader from inside the unpacked kit:

```sh
node cli/makefun.mjs grade-local --kit . --bot <path to this repo> --driver process
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=r9wmade1&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
