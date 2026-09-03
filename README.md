# SR Terminal — Standard Reserve Simulator

Interactive mental-model tool for the Standard Reserve whitepaper (v0.1).
Single-page app, no build step, deploys directly to Vercel.

## Quick deploy

1. Import `https://github.com/roadsidedev/SR-terminal` in Vercel
2. Framework preset: **Other** (or leave as-is — no build command needed)
3. Deploy — `index.html` is served at root

Or from the CLI:
```bash
vercel --prod
```

## Local use

Just open `index.html` in a browser. No server required.

## What it models

| Mechanism | Implementation |
|---|---|
| Supply identity | `S_circ = 100M + M(t) − B(t)` (wp eq 3.1) |
| Flow signal | `signal = F_{n-1} + F_{n-2}` — slow lever for issuance (wp eq 4.1) |
| Issuance | `I = baseRate × days × m`, pro-rata across open branches (wp eq 5.1) |
| Policy multiplier | Asymmetric: cuts immediate, raises earned (wp eq 5.2) |
| License auction | Daily Dutch in $STANDARD, 100% burned |
| Charter auction | Daily Dutch in ETH, proceeds feed fee engine |
| Resolution fee | Quadratic in 7-epoch exit pressure: `floor + (P/sat)^2 × (ceil − floor)`, 50% burned / 50% redistributed (wp eq 9.1) |
| Dormancy | 30-day inactivity → revocation + informant bounty |
| Fee routing | 70% active vault / 15% POL / 15% team |
| Buybacks | Rate-limited: `min(0.10·V, 0.002·R)` per epoch |

**Note:** The whitepaper redacts all numeric launch parameters. Every constant in this terminal is an editable assumption.

## Project structure

```
SR-terminal/
├── index.html        ← self-contained app (HTML + CSS + JS)
├── vercel.json       ← SPA routing config
├── README.md
└── .gitignore
```

## License

MIT
