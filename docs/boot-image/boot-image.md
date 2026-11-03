# Stock boot and recovery image inspection

## Reference images

Two images were supplied for the Alcatel 9032X / Apollo_8_4G project:

| Image | Size | SHA-256 |
|---|---:|---|
| `boot.img` | 33,554,432 bytes (32 MiB) | `bc05cd6065d3d1f59c44a46d68867e4ddfe3c3c0b7360ef480d9e7f6b8b06972` |
| `recovery.img` | 33,554,432 bytes (32 MiB) | `fea18b7c5c771054aec49559b09162be56dcc504667866fb2ffed54618886c07` |

Both images begin with Android boot magic `ANDROID!`, report boot header version 2, and use a 2048-byte page size.

These hashes identify the exact uploaded files. Keep the originals unchanged in a secure local backup.

## Boot image

File: `boot.img`

| Field | Observed |
|---|---:|
| Kernel size | 8,637,050 bytes |
| Kernel load address | `0x40008000` |
| Ramdisk size | 735,272 bytes |
| Ramdisk load address | `0x44000000` |
| Page size | 2048 bytes |
| Header version | 2 |

Kernel payload SHA-256:

```text
515c0b7756481370fba8f0f8337bd140bfe364dce17c1725fd6db281b933880e
```

Two 78,506-byte DTB payloads were found at offsets 8,560,592 and 9,377,856. The first DTB has SHA-256:

```text
7e3b103c11d51f8aec5b198a22908be62f629c6039f1fa42cedf29ff7c09c423
```

This matches the extracted `apollo_boot_base.dtb` byte-for-byte.

## Recovery image

File: `recovery.img`

| Field | Observed |
|---|---:|
| Kernel size | 8,637,050 bytes |
| Kernel load address | `0x40008000` |
| Ramdisk size | 6,725,929 bytes |
| Ramdisk load address | `0x44000000` |
| Page size | 2048 bytes |
| Header version | 2 |
| Recovery DTBO size | 60,296 bytes |
| Recovery DTBO offset | 15,368,192 |

Kernel payload SHA-256:

```text
515c0b7756481370fba8f0f8337bd140bfe364dce17c1725fd6db281b933880e
```

The boot and recovery images have byte-identical kernel payloads. Their ramdisk payloads differ.

The recovery image contains the same 78,506-byte base DTB at offset 8,560,592. A 60,232-byte FDT payload was found at offset 15,368,256, consistent with the declared 60,296-byte recovery DTBO area including its alignment/padding. Another 78,506-byte DTB was found at offset 15,429,696 and matches the base DTB hash above.

Recovery ramdisk SHA-256:

```text
99e5f4ce283f97586eb259ae8f48ce9cf57bb162955a019100f0d3676af56386
```

## Related device-tree artifacts

- `apollo_boot_base.dtb`: extracted base DTB.
- `apollo_merged.dtb`: output of applying the examined overlay to the base DTB.
- `apollo_merged.dts`: decompiled merged device tree.

The extracted base DTB reports a 512 MiB memory node, while the live device tree reports 2 GiB. The stock boot process therefore requires further investigation before using the extracted DTB as a source for a custom build.

## Interpretation and safety

The identical kernel payload confirms that these two supplied images share the same kernel binary. The different ramdisks and recovery DTBO area are expected structural differences between boot and recovery images.

These observations do not establish that either image is safe to modify or flash, nor do they prove that a custom ROM can boot.

Do not flash experimental images based only on this inspection. First document the complete boot image layout, ramdisk contents, command line, AVB/vbmeta relationship, partition map, and a tested device recovery method.
