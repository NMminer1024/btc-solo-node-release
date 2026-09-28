### Added
- SD card health monitoring: the System page now shows a small dashboard with the key SD card health metrics, so you can see card condition at a glance.
- Boot screen now shows the live Bitcoin block height as soon as the node starts syncing.

### Improved
- Mining process (ckpool) uses noticeably less memory over long runs, leaving more headroom for the rest of the system.
- Boot screen now waits until the mining connection is actually up before moving on, so the first screen you see reflects a working node.
- Time sync is lighter on the system: a one-shot sync at boot plus a daily re-sync instead of a constantly running time service.

### Fixed
- After an OTA update, the block data partition now always comes back mounted correctly.
- Interrupted OTA updates no longer leave stale image files behind that eat up storage.
- The disk usage list now visually separates the total row from individual partitions, making it easier to read.
