### Fixed
- The SD Card Health "Tracking" line on the About page could show a wrong start date (1970) and an absurd tracking duration on boards without a real-time clock. It now only starts counting once the system time is synced, so the date and duration are correct.
- Closing a popup (Peer Map, Miners, Network Settings, Timezone, etc.) with the X button could occasionally take a long time to disappear. It now closes instantly.
