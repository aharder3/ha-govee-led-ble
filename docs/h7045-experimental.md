# H7045 experimental BLE support – owner trace

This is **unverified Home Assistant support**, not a claim that H7045 works in all modes.

## Evidence (owner-supplied PacketLogger trace)

- BLE advertisement name: `Govee_H7045_8167` (suffix anonymized in public documentation).
- GATT Write Without Response and notifications are used.
- Govee encrypted v2 handshake and authenticated application traffic were observed.
- Decoded 20-byte application commands share the existing `33` command envelope and XOR checksum.
- Brightness commands observed: `33 04 14` (20%), `33 04 64` (100%).
- RGB prefixes observed: `33 05 15 01 FF 00 00` (red), `33 05 15 01 00 00 FF` (blue).
- Whole-device mask seen on this 10-bulb sample: `FF 03`.
- Queries `AA 01 00` and `AA 04 00` produced corresponding replies.

No full raw capture, personal identifiers, negotiated keys, IVs or decrypted pairing information are included here.

## Implementation

- An **experimental** profile reuses the H617A write grammar and provisionally H7025 status grammar.
- Basic power, brightness and static RGB are enabled as test candidates. Power writes are **not yet physically confirmed**.
- Segment writes, scenes, music and colour temperature are **not** exposed.
- Experimental configuration no longer crashes if the model has no upstream confirmation issue yet.

## Still to validate on real hardware

1. ESPHome active BLE proxy connectivity and Govee v2 session setup.
2. Physically verified power ON/OFF, brightness and RGB commands.
3. Actual startup/readback for power, brightness, colour mode.
4. Exact model's status parsing, firmware variations, and potential scene catalogue.
5. Project-wide checks, static analysis and hardware integration tests.

Do not promote H7045 to Supported or merge upstream until tests and hardware confirmation are complete.
