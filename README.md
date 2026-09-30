# Smallfish Public Signal Mode v9
Railway-ready, MEXC public futures data only. No MEXC API key/secret and no orders.

Pattern: liquidity sweep -> 10m CHoCH -> fresh bias -> EARLY setup -> 5m/1m trigger -> final signal.

V9 adds an EARLY SETUP Telegram alert when a fresh sweep+CHoCH is detected, instead of waiting until price is already several ATR away. Final SIGNAL still requires 5m + 1m confirmation and location filters.


## V9 automatic reversal

Final V9 signals are tracked automatically. When price reaches 48% of the distance from the original Entry toward either the original TP or the original SL, the bot immediately sends one opposite-direction reversal signal. No additional CHoCH, sweep, or confirmation is required for the reversal.

- TP-side reversal: opposite direction, current market price as Entry, TP1 = original Entry, TP2 = original SL.
- SL-side reversal: opposite direction, current market price as Entry, TP1 = original Entry, TP2 = original TP.
- The original signal is removed from reversal tracking after the first trigger, so it cannot duplicate the same reversal.
- `REVERSAL_PCT=0.48` can be changed in Railway environment variables if needed.
