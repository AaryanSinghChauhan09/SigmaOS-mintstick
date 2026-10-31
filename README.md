# SigmaOS Mintstick

Rust model for removable-media discovery, formatting, image writing, and
checksum records, inspired by Linux Mint's Mintstick utility.

## Current behavior and safety

This is not a disk writer. `scan_devices()` returns two hard-coded mock devices
(`/dev/sdb` and `/dev/sdc`); `write_image()` and `format_device()` only append
operation records to memory. `calculate_checksum()` returns a mock checksum
without reading the image, and `verify_checksum()` therefore does not verify
real media. No filesystem is formatted and no block device is written.

Do not use this crate to flash or format a real device. A production writer
needs fresh device identity and capacity checks, explicit user confirmation,
exclusive-device handling, bounded writes, progress and cancellation semantics,
read-back verification, and a recoverable error report.

## Development

The public entry point is `MintstickManager`. Run `cargo check` and `cargo test`
for local crate validation; neither establishes real-device support.
