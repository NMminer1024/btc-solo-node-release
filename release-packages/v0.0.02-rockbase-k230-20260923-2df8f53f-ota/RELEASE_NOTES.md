### What's new

- Fixed a disk-space issue that could block firmware updates on long-running nodes:
  - Old downloaded firmware images are now cleaned up automatically after each update
  - Pool server log files are now size-limited so they no longer grow without bound
  - Update logs are rotated and old update logs are pruned automatically
- OTA update dialog now shows release notes (what's new) before you confirm an update
