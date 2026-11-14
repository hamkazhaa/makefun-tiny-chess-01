# Tiny chess engine — make.fun tiny-chess-01

A chess engine in 4 KB of Python. `main.py` (3,530 bytes) is a
zlib+base85 packed engine (allowed by the rules; the baseline ships
the same way): 0x88 board, negamax alpha-beta with transposition
table, MVV-LVA ordering, quiescence (captures, check evasions,
delta pruning), CPW piece-square tables, iterative deepening to
a fixed 80,000 nodes a move (deterministic: no clock, no
unseeded randomness). Depth 4 completes in most middlegame
positions; the cap keeps every move inside the 10 s limit.

It talks only to the env at `MAKEFUN_ENV_URL` (`POST /game`,
`/move`), plays the 8-game gauntlet (6 in practice), and exits
when the env says done. About 3–5 s a move, under the 10 s limit.

## Verify

```bash
python3 -c "import importlib.util; s=importlib.util.spec_from_file_location('m','main.py'); m=importlib.util.module_from_spec(s); s.loader.exec_module(m)"
# perft: startpos d3 = 8902, kiwipete d3 = 97862
```

## Files

- `main.py` — the whole engine (packed)
- `LICENSE` — MIT
- `.makefun/owner.json` — claim file
