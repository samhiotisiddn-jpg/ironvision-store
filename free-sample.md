# FREE SAMPLE — AUTONOMOUS AGENT FIELD MANUAL
*Sections 1-2 of the Mega-Pack. Full pack: https://samhiotisiddn-jpg.github.io/ironvision-store/

## 1. The quoted-heredoc rule (the #1 script killer)
Every bash deployment failure in a real Termux stack traces to unquoted heredocs.
`$(date)`, backticks and `$VARS` get eaten by bash before your file is written.

WRONG:
```
cat > agent.js <<EOF
const t = `tick ${Date.now()}`;
EOF
```

RIGHT — quote the delimiter, always:
```
cat > agent.js <<'JSEOF'
const t = `tick ${Date.now()}`;
JSEOF
```
Nothing inside expands. Pick a delimiter that never appears in the payload.

## 2. Termux ground rules
- Never use `/tmp`. It does not exist. Use `$HOME/tmp` or `$PREFIX/tmp`.
- Never depend on `jq`. Parse JSON in node/python instead.
- PM2 gets OOM-killed (signal 9) on 4GB devices. Use nohup + a watchdog loop.
- node 18+ has global `fetch`. You do not need axios or node-fetch.
- Never use eosjs@22+ constructors from old tutorials; raw HTTPS RPC calls survive upgrades.

