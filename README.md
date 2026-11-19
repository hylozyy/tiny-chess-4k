# Hylo Tiny Chess

A chess engine in a single `main.py` of 3,937 bytes (limit 4,096), Python 3.13 standard library only, built for the make.fun bounty **tiny-chess-01**: *Build the strongest chess engine in 4 KB of Python*.

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/hylozyy/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/hylozyy/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01)

## The engine

- **Board**: 10x12 mailbox that rotates to the side to move, with pseudo-legal moves and king capture. The move that is sent is always one of the env's own `legal_moves`.
- **Evaluation**: PeSTO piece-square tables, tapered between middlegame and endgame by the phase at the root and kept incrementally during search. A mop-up term drives the losing king to the edge once one side is clearly ahead.
- **Search**: iterative deepening negamax with PVS, a transposition table, check extension, null-move pruning, reverse futility pruning, futility and late-move pruning, late move reductions, killer moves, history heuristic, and capture quiescence with delta pruning. Pruning is switched off in won endgames so mates are found.
- **Rules**: mates, stalemates, repetitions (rebuilt from the game's full move list), the fifty-move rule and insufficient material are all scored correctly. Draws carry a contempt that grows against weaker opponents.
- **Time**: a fixed node budget per move, scaled by the opponent's rung and the move number. It never reads the clock, so replays are identical.

## Run it

```
MAKEFUN_ENV_URL=<env url> python3 main.py
```

`main.py` is `engine.py` packed by `makefun compress`.

Entered on [make.fun](https://make.fun/bounty/tiny-chess-01).

## License

MIT, see `LICENSE`.
