# Tiny Chess v8 — 4 KB Python chess engine

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/competitions/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/bismilahdestia/tiny-chess-01-entry-v3/rank.svg)](https://make.fun/competitions/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/bismilahdestia/tiny-chess-01-entry-v3/reward.svg)](https://make.fun/competitions/tiny-chess-01)

Alpha-beta search with quiescence (captures, promotions, check evasions),
null-move pruning, LMR, aspiration windows, futility pruning, transposition
table, killer + history move ordering. Evaluation: material + piece-square
centrality + king tropism + pawn structure + king safety, all integer math,
with the positional terms served from precomputed tables.

Deterministic: a fixed node budget per move (75,000 nodes), never a clock,
so a replayed trial plays the same moves. v8 is the v4 lineage with the
timeout tail fixed and the strength recovered: v4 lost 2 of 6 games on time
in the practice trial (moves up to 22 s at a 120,000-node budget); v7 cut
the budget to 45,000 and scored 1,099 on the server, 55 short of the 1,154
floor. v8 searches deeper on the same time: a table-driven evaluation plus
delta pruning in quiescence and deeper late-move reductions buy back the
ply v7 gave up. At the final 75,000-node budget the local trial-0 scores
Elo 1,279 (W3 D0 L3, zero timeouts, slowest move 9.8 s) — above the 1,154
floor and the 1,250 target.

`main.py` is the whole engine (lzma payload + unpacker, 3,611 bytes).
Python 3.13 standard library only.
