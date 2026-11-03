# Development roadmap

## Phase 1 — Research and preservation

- [x] Create project repository.
- [x] Record stock device identity and platform facts.
- [x] Inspect stock boot image header and embedded DTB.
- [x] Record the extracted-DTB versus live-memory discrepancy.
- [ ] Archive original stock images with verified hashes in a safe local backup.
- [ ] Record exact firmware package version and extraction commands.
- [ ] Verify partition map and boot/recovery image layout.

## Phase 2 — Hardware and source audit

- [ ] Identify active display panel and touchscreen controller.
- [ ] Identify sensors, camera, audio, modem, Wi-Fi, Bluetooth, and charging ICs.
- [ ] Locate matching kernel source and configuration.
- [ ] Inventory vendor components and their licenses.
- [ ] Determine verified boot and slot behavior.

## Phase 3 — Device tree and build preparation

- [ ] Establish the correct Android base and supported build environment.
- [ ] Create a device tree from verified device data.
- [ ] Integrate kernel and vendor components with appropriate licenses.
- [ ] Configure recovery and partition handling.
- [ ] Run static validation and build checks.

## Phase 4 — Controlled testing

- [ ] Define a non-destructive test plan.
- [ ] Confirm a full recovery route before any write operation.
- [ ] Test boot components incrementally.
- [ ] Record logs, regressions, and known limitations.

No phase beyond research/preservation is complete yet.
