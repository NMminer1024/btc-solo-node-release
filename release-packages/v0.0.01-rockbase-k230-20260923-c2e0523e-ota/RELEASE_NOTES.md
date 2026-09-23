### Added
- Version numbering restarts from v0.0.01. This is the first release of the new version line; all previous releases and version tags have been retired.

### Improved
- Mining pool reconnects noticeably faster after a network interruption (retry interval reduced from 60s to 5s).
- The "bitcoind ready" check is now more reliable: the node must stay healthy for 3 consecutive checks instead of 2 before mining is considered ready.
