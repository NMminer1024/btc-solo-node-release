### New
- SD Card Health monitoring on the About page: shows the card model, cumulative data written, I/O errors, and how long tracking has been running.

### Improved
- Time sync now runs once at boot and re-syncs daily instead of keeping a background time service running, reducing steady-state CPU and storage activity.
- The About page layout is tidier: the Firmware and Storage cards now line up, and the SD Card Health card shows the four most useful numbers.

### Fixed
- Interrupted firmware updates (for example, a freeze or power loss mid-download) could leave a large temporary file behind that slowly filled the config partition over time. These leftovers are now cleaned up automatically.
