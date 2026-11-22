# site-generator-speed-01 v2

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/competitions/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/Noddy1012/site-generator-speed-01-v2/rank.svg)](https://make.fun/competitions/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/Noddy1012/site-generator-speed-01-v2/reward.svg)](https://make.fun/competitions/site-generator-speed-01-run-20261122)

A faster drop-in for [makefun-site 1.0.0](https://make.fun), make.fun's own static
site generator: `solve.js` answers exactly as it does on every case — the same
output tree, byte for byte — in less CPU time.

## How it is faster

- Front matter is walked line by line and the body is sliced out, never split
  and re-joined.
- Markdown is lexed and rendered in a single pass; inline rendering escapes
  plain runs in one replace instead of one character at a time.
- `slugify` is memoised per build, with a fast path for pure-ASCII text.
- Templates are compiled once per build into straight-line JavaScript
  (`new Function`): text, variables, loops, conditions and includes become
  direct code, with loop-bound names read straight from their locals.

## Layout

- `solve.js` — dependency-free ES module; `run(input)` returns makefun-site's
  answer for one case's input.
- `main.ts` — the harness program: reads `/input/cases.json`, answers each case
  with `run`, writes `/output/answers.json`.
