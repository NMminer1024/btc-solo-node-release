### Added
- You can now start and stop Bitcoind and Stratum directly from the web dashboard. Each card has a menu button (three dots) with a Start/Stop action that follows the current state.
- The Stratum card now shows a third status, "Waiting for Bitcoind", when mining is paused because Bitcoind is not ready yet. If you try to start Stratum in this state, a dialog explains exactly why it cannot start (for example, Bitcoind is not running or still syncing). Stratum starts automatically once Bitcoind is ready.
- Stopping a service asks for confirmation first, so it cannot be triggered by accident.
