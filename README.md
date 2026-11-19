# Tiny Chess — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88-board chess engine in pure Python: negamax alpha-beta search with a transposition table, PVS, null-move pruning, LMR and quiescence search, MVV-LVA/killer/history move ordering, and material + piece-square evaluation. The whole engine is packed into 4,074 bytes with the kit's makefun compress and searches a deterministic fixed number of nodes per move. In the kit's practice gauntlet it scored a mean Elo of 1404, above the sunfish 4 KB baseline's 1365; the current build's local practice results are under Verification.

## How it works

The board uses the 0x88 representation, where off-board squares are detected with a single AND against 0x88. Search is negamax alpha-beta backed by a Zobrist transposition table, so positions reached by different move orders are scored once. Instead of a clock, each move gets a deterministic fixed node budget — 125k nodes in the opening, 115k in the middlegame, 95k in the endgame — which makes every replay of a game identical. Move legality is checked once per move inside the search loop (the earlier build made and unmade every move twice per node), the transposition table is capped so late-game searches stay fast, and the interpreter's cyclic GC is disabled; together these keep every move well inside the 10-second limit. The readable source, engine.py, is packed into main.py with the kit's `makefun compress`.

## Verification

Move generation was verified with perft, exact on 5 standard test positions. The packed main.py's LZMA payload decompresses byte-for-byte to engine.py, and the packed artifact itself played the practice trials below. Local practice gauntlet (the kit's env and scorer run on this machine): the previous build scored Elo 1099 on trial 0 with two games lost on time (worst move 11.3 s); the current build scored 1451 / 1279 / 1451 on trials 0 / 1 / 2 (mean 1394), won 11 of 18 games with no timeouts, and its worst move over 791 timed moves was 4.2 s — every game decided by checkmate or adjudication, none on time, and every trial wall time under 12 minutes of the 30-minute budget.
