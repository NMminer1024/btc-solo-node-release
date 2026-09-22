# Rockbase — Bitcoin Solo Mining All-in-One

**[ English ]** · [ 中文 ](README.zh-CN.md)

---

### What is this?

Rockbase is an **out-of-the-box Bitcoin node + solo mining all-in-one device**.

Plug in power, connect to your network, and it starts doing two things:

1. **Running a Bitcoin validating node** — it downloads and verifies every block on the blockchain itself, with no reliance on third-party data (in pruned mode, keeping only recent block data to save space);
2. **Serving a local Stratum mining endpoint** — plug your miner into it and mine the Bitcoin mainnet directly. Any block reward you find is 100% yours.

No OS to install, no software to configure, no command line required. The device ships with a color touchscreen and a web console, so every status is visible at a glance.

### Hardware Specifications

| Item | Spec |
|------|------|
| Processor | Canaan K230 (RISC-V) |
| Memory | 1 GB |
| Display | Color touchscreen (480×800 physical) |
| Network | On-board WiFi + USB-to-Ethernet adapter (DHCP) |
| Storage | SD card (blockchain data) |
| Power | DC power adapter |

### Touchscreen UI

The screen has 4 pages — **swipe left/right to switch**:

**① Bitcoind page** — Node overview: current block height, sync progress, connected peers, mining difficulty, UTXO set size.

![LCD Bitcoind page](docs/img/lcd-bitcoind.png)

**② Stratum page** — Mining status: pool hashrate chart, online workers, best share.

![LCD Stratum page](docs/img/lcd-stratum.png)

**③ System page** — Device health: CPU usage, temperature, memory, blockchain data usage.

![LCD System page](docs/img/lcd-system.png)

**④ Network page** — Network info: IP address, MAC address, WiFi signal strength.

![LCD Network page](docs/img/lcd-network.png)

**Peer Map** — On the Bitcoind page, tap the peer count to open a world map showing which nodes around the globe your node is talking to, with animated lines indicating data flow direction.

![Peer Map](docs/img/lcd-peer-map.png)

### Web Console

Open `http://<device-IP>` in any browser (the IP is shown on the Network page or in your router). The console supports 10 languages (English, 中文, Español, Français, Deutsch, Português, Русский, 日本語, 한국어, العربية) — switch in the top-right corner.

**Dashboard** — Everything on one screen: node sync status, Stratum endpoint & hashrate, CPU / memory / temperature / network metrics.

![Web Dashboard](docs/img/web-dashboard.png)

**Miners** — Per-miner hashrate history and contributed shares, so you can confirm each miner is working.

![Web Miners](docs/img/web-miners.png)

**About** — Version info and the firmware update entry (see below).

![Web About](docs/img/web-about.png)

### Network Connection

Rockbase supports two network paths, auto-detected at boot:

- **On-board WiFi** — just join your home wireless network;
- **USB-to-Ethernet adapter** — plug in a USB NIC for a more stable wired connection. Common USB NIC chips are supported out of the box (Realtek RTL8152/RTL8153, ASIX AX88179 gigabit, AX88772 100M, etc.) — no drivers needed.

Both use DHCP. If a USB NIC and WiFi are both available, the USB wired path takes priority.

### Connecting Your Miner

1. Make sure your miner and Rockbase are on the **same LAN**;
2. In your miner's pool settings, enter:

   ```
   stratum+tcp://<Rockbase-IP>:3333
   ```

   (The IP is visible on the LCD Network page or in the web console. Username/password can be anything, e.g. `worker1` / `x`.)
3. Save. Your miner starts submitting work to Rockbase. When the hashrate chart appears on the LCD Stratum page or the web Miners page, you're connected.

> Tip: assign Rockbase a static IP in your router so miners don't lose connection after reboots.

### Firmware Updates

Rockbase uses **A/B dual-slot OTA updates** — even a power loss mid-update won't brick the device:

1. Open the **About** page in the web console;
2. Tap **Check for Updates** to see if a new version is available;
3. If one is, tap **Update Now** — the device downloads, signature-verifies, writes the standby slot, and reboots automatically;
4. If the new firmware fails to boot, the device **rolls back automatically** to the previous version.

All firmware packages are published on the [Releases](https://github.com/NMminer1024/btc-solo-node-release/releases) page, which the device checks automatically when looking for updates.

### Versioning & Releases

- Version format: `vX.Y.ZZ` (e.g. `v0.4.00`). Full package names look like
  `v0.4.00-rockbase-k230-20260922-da181f46-ota`
  (version - platform - build date - code fingerprint - ota);
- Every firmware package is **signed**; the device verifies the signature during update to guarantee authenticity;
- All historical versions are available on the [Releases](https://github.com/NMminer1024/btc-solo-node-release/releases) page.

### FAQ

**Q: How long until it's ready after first power-on?**
A: The first boot downloads and verifies the entire blockchain (~15 GB of downloads). Depending on your connection this takes several hours to a day. The device runs in pruned mode, keeping only the most recent ~4 GB of block data after verification. You can connect miners during sync, but block-finding probability is negligible until sync completes.

**Q: My miner can't connect — what do I check?**
A: Confirm both devices are on the same LAN; confirm the pool URL is `stratum+tcp://IP:3333` (port 3333); check that the LCD Stratum page shows "Running".

**Q: Does the device run hot?**
A: Normal operating temperature is about 55–65°C, viewable live on the System page. Keep the area around the device well ventilated.

**Q: How do I reset the device?**
A: Power cycle it. Blockchain data lives on the SD card and survives reboots.

### Support

- Firmware downloads & release notes: [Releases](https://github.com/NMminer1024/btc-solo-node-release/releases)
- Bug reports: please open a GitHub Issue — attaching an LCD screenshot or web console screenshot helps a lot.
