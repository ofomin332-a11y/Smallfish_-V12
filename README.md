# Smallfish Public Signal Mode v9
Railway-ready, MEXC public futures data only. No MEXC API key/secret and no orders.

Pattern: liquidity sweep -> 10m CHoCH -> fresh bias -> EARLY setup -> 5m/1m trigger -> final signal.

V9 adds an EARLY SETUP Telegram alert when a fresh sweep+CHoCH is detected, instead of waiting until price is already several ATR away. Final SIGNAL still requires 5m + 1m confirmation and location filters.


## V9 automatic reversal

Final V9 signals are tracked automatically. When price moves **+0.48% or -0.48% directly from the original Entry**, the bot immediately sends one opposite-direction reversal signal. This is **not** 48% of the distance from Entry to TP/SL. No additional CHoCH, sweep, or confirmation is required for the reversal.

- The first side reached (+0.48% or -0.48% from Entry) triggers the reversal.
- Reversal Entry = current market price at the trigger.
- TP1 = original Entry.
- TP2 = original SL.
- SL = original TP.
- The original signal is removed from reversal tracking after the first trigger, so it cannot duplicate the same reversal.
- The reversal percentage is fixed in code at `0.0048` (0.48%).
