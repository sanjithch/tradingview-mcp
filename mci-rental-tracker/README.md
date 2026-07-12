# MCI Rental Car Price Tracker

Automated price monitoring for a rental car at **Kansas City International Airport (MCI)**.

## Trip
- **Pickup:** Aug 12, 2026, 10:00 PM
- **Drop-off:** Aug 15, 2026, 10:00 PM
- **Vehicle class:** Standard / Midsize
- **3-day rental**

## How it works
A scheduled Routine runs **every ~3 hours** and:
1. Web-searches current MCI standard/midsize daily rates for the trip dates.
2. Appends the observed price to `price_history.json` (`observations` array).
3. Computes the **running average** of all logged prices.
4. If the newest quote is **below the running average**, sends a push notification with the price, the average, and a booking link.
5. Commits the updated log to this branch so history survives across runs.

Monitoring runs until the **Aug 12 pickup day**, then the Routine stops itself.

## Observation format
```json
{ "ts": "2026-07-12T18:00Z", "price_per_day": 46, "total_3day": 138, "source": "kayak", "below_avg": false }
```

## Notes
- Prices come from public comparison sites (KAYAK/Priceline/Expedia/etc.), so they are reliable ballpark rates, not a locked quote. When a good dip appears, book directly with the provider to lock it.
