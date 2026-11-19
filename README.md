# Tiny Chess — a 4 KB Python chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/mutroll/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original 0x88-board chess engine in pure Python: negamax alpha-beta search with a transposition table, PVS, null-move pruning, LMR and quiescence search, MVV-LVA/killer/history move ordering, and material + piece-square evaluation. The whole engine is packed into 4,040 bytes with the kit's makefun compress and searches a deterministic fixed number of nodes per move. In the kit's practice gauntlet it scored a mean Elo of 1404, above the sunfish 4 KB baseline's 1365.
