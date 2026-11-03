# Stock boot image inspection

## Examined image

File examined: `boot_full_32MiB(3).img`

| Field | Observed |
|---|---|
| File size | 33,554,432 bytes (32 MiB) |
| Boot magic | `ANDROID!` |
| Boot header version | 2 |
| Page size | 2048 bytes |

## Embedded DTB verification

Two DTB payloads were found in the image:

| Copy | Offset | Size |
|---|---:|---:|
| DTB 1 | 8,560,592 | 78,506 bytes |
| DTB 2 | 9,377,856 | 78,506 bytes |

Both payloads were reported to match the extracted `apollo_boot_base.dtb` byte-for-byte.

SHA-256:

```text
7e3b103c11d51f8aec5b198a22908be62f629c6039f1fa42cedf29ff7c09c423
```

This verifies the provenance of the extracted DTB relative to the examined image. It does not verify the boot image's complete compatibility with a custom ROM.

## Related artifacts

- `apollo_boot_base.dtb`: extracted base DTB.
- `apollo_merged.dtb`: output of applying the examined overlay to the base DTB.
- `apollo_merged.dts`: decompiled merged device tree.

Keep original firmware images unchanged. Record SHA-256 hashes and extraction tools/versions for all future analysis.

## Warning

Do not flash this image or a modified version based only on the inspection above. First document the complete boot image layout, kernel, ramdisk, command line, AVB/vbmeta relationship, partition map, and device recovery method.
