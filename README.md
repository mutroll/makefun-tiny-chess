# Tiny Chess — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88-board chess engine in pure Python: negamax alpha-beta search with a transposition table, PVS, null-move pruning, LMR and quiescence search, MVV-LVA/killer/history move ordering, and material + piece-square evaluation. The whole engine is packed into 4,040 bytes with the kit's makefun compress and searches a deterministic fixed number of nodes per move. In the kit's practice gauntlet it scored a mean Elo of 1404, above the sunfish 4 KB baseline's 1365.

## How it works

The board uses the 0x88 representation, where off-board squares are detected with a single AND against 0x88. Search is negamax alpha-beta backed by a Zobrist transposition table, so positions reached by different move orders are scored once. Instead of a clock, each move gets a deterministic fixed node budget — 105k nodes in the opening, 95k in the middlegame, 80k in the endgame — which makes every replay of a game identical. The readable source, engine.py, is packed into main.py with the kit's `makefun compress`.

## Verification

Move generation was verified with perft, exact on 5 standard test positions. The packed main.py replayed a full practice trial ply-for-ply identical to the readable source, so the packed artifact plays exactly the game the source plays. Practice gauntlet trials scored Elo 1279 / 1279 / 1654 (mean 1404) against the kit anchors — above the sunfish 4 KB baseline's practice mean of 1365 and well above the 1154 final floor.
