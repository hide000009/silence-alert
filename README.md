# Silence Alert

A [Windower](https://www.windower.net/) addon for **Final Fantasy XI** that plays a "ding" sound **only when Silence actually lands on an enemy**.

No more guessing from the battle log — and no false alarms: resists, "no effect", Barspell lines, and party members getting silenced never trigger the sound.

## Features

- Dings only on a real, applied Silence (strict detection, see below)
- Single-file install: the `ding.wav` sound is generated automatically on first load
- Chat messages are in English (pure ASCII file), so nothing garbles on the JP client
- Optional party-only mode: only alert for your own / your party's Silence

## Install

1. Copy the `silence_alert` folder into your Windower addons folder:
   `Windower4/addons/silence_alert/silence_alert.lua`
2. In game:
   ```
   //lua load silence_alert
   //sa test
   ```
   `//sa test` plays the sound once so you can check it.

## Usage

```
//sa test    Play the sound once
//sa on      Enable alerts
//sa off     Disable alerts
//sa party   Toggle party-only mode
```

## How it works

Detection is deliberately strict, to avoid false alarms:

- **Action check:** a Silence spell finishes on a monster *and* the result is the "effect applied" message (236). Resists / no-effect / immune results never ding.
- **Log check (backup, for the Japanese client):** the battle-log line "<monster> is afflicted with Silence" counts only when the named target really is a monster (checked with `get_mob_by_name`). バサイレス/バサイレラ (Barsilence) lines, party members, and wear-off lines are ignored.
- A 1-second debounce prevents double dings when both checks fire.

The sound is a two-tone ping (G6 → C7) synthesized by the addon itself into `ding.wav` on first load; replace that file with your own `.wav` if you prefer a different sound.

## License

MIT — see [LICENSE](LICENSE).
