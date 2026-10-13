# ble-sign-beacon

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

## ethics & prohibited behaviors (speech vs. blockade)

- **Leave power LOW (-12 dBm) and timing standard (~100 ms + random jitter):** Don't amplify (+9 dBm) or burst spam (20 ms). That causes venue capture effect and band exhaustion, breaking everyone's signal including fellow protesters.
- **Keep the honest locally-administered OUI (`02:47:54`):** Never impersonate Apple, Google, Microsoft, or Samsung hardware.
- **Never doppelgang nearby civilian devices:** Sniffing and cloning real bystander MACs or GATT attributes fabricates false forensic evidence in automated surveillance dragnets (the "Sentinel" trap), framing innocent people.
- **Never tamper with the Access Address (`0x8E89BED6`):** Injecting illegal sync words or snooped connection addresses poisons baseband receiver correlators and drops civilian connections.
- **Never corrupt Block 1 (Flags):** Don't advertise contradictory BR/EDR capabilities or zero-timeout Limited Discoverable states that crash OS Bluetooth daemons or drain phone batteries.
- **Never hijack Block 3 (Manufacturer Data) for UI DoS:** No SourApple / AppleJuice / SwiftPair / FastPair proximity popups that freeze civilian phones or block emergency calls.
- **Never clone medical or safety UUIDs:** Never mirror Continuous Glucose Monitors (`0x181F`), Hearing Aids (`0x1851`), or key fobs.
- **One beacon per person:** The crowd is the message; don't be individually loud.

