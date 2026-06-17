# marietta-agitator

Bluetooth low-energy sit-in beacon. broadcast a short sign-message as a BLE advertisement on any ESP32 (~$5-8). intended to make presence VISIBLE in the RF spectrum — not hidden, not interfering, just countable. "you're choosing to be seen, that's the whole idea of a sit-in."

## what it does

continuously broadcasts a Bluetooth advertisement with your message as the device name. low power, low frequency, no encryption, no attempt at anonymity. if BLE scanners see you, that's the point.

## options

**Option A: code-based (static message)**
- edit `good_trouble.ino`, set `TAIL` to your personal sign
- keep `PREFIX` and `SITIN_OUI` as the group agreed (shared identity)
- compile and flash via Arduino IDE

**Option B: config-based (web UI, no code)**
- flash `good_trouble_config.ino` without editing
- on first boot, creates `good-trouble-setup` Wi-Fi network
- join from your phone, set your message via captive portal
- to change later: hold BOOT while replugging to re-enter config mode

## hardware

- any ESP32 dev board (e.g., ESP32-WROOM, $5-8)
- USB cable and computer for initial flash
- no antenna upgrade needed (internal BLE antenna sufficient)

## protocol

- BLE advertisement, low power
- non-connectable, non-scannable
- beacon name = your message (max ~29 bytes for full UUID + data)
- advertising interval = 100 ms (standard BLE)
- TX power = low (set in code)

## ethics

- leave power LOW and timing as-is. don't "fill" the band — that breaks everyone's signal including the rest of the crowd's
- keep the made-up shared OUI. don't impersonate real brands or nearby networks
- one beacon per person. the crowd is the message; don't be individually loud
