### Added
- Animated boot video with a smooth fade into the dashboard instead of the static logo.
- The mining pool now runs in solo payout mode: a block you find pays the address you connect with as your stratum username, instead of a preconfigured pool address.

### Improved
- Stratum hashrate, the miner list, and system/network stats now update within seconds instead of every one to two minutes.
- Offline wallets are shown in muted gray on the LCD miner list and the web miners table, so live and inactive miners are easy to tell apart.

### Fixed
- Offline miners no longer show a stale hashrate; they show 0 while disconnected, and their best-share history is kept.
- SD card health status on the About page is now based on hard evidence only, so it no longer misreports on normal wear and can recover once the condition clears.
