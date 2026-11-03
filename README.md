# GernalOS

> [!WARNING]
> **AI-ASSISTED PROJECT — NOT HUMAN-VERIFIED.** This repository's documentation and some project materials have been created or edited with substantial AI assistance. Treat generated content, commands, configuration, and technical conclusions as unverified until independently checked on the target device. AI output may be incomplete or incorrect. The project is experimental and is not a ready-to-flash ROM.

See [AI disclosure](docs/AI-DISCLOSURE.md) for details.

**GernalOS** is a device-focused Android development project for the **Alcatel 3T8 (9032X), codename `Apollo_8_4G`**.

The ROM concept is named **ApolloOS**. This repository is the project's development workspace for device research, documentation, and future bring-up work.

> **Development status: Research / bring-up preparation.**
> No GernalOS/ApolloOS build is currently claimed to boot or be suitable for installation. Do not flash experimental images to a device.

## Target device

| Item | Verified information |
|---|---|
| Model | Alcatel 9032X |
| Product / device | Apollo_8_4G |
| Android stock base | Android 10 |
| Platform | MediaTek MT6761 |
| Kernel | Linux 4.9.190+ |
| CPU architecture | ARM 32-bit (`armv7l`) |
| Primary ABI | `armeabi-v7a` |
| Physical RAM | 2 GiB |
| Dynamic partitions | Reported enabled by the stock system |

Device facts are based on observations from the stock device. Values must be revalidated against the exact firmware used for development.

## Repository layout

```text
GernalOS/
├── device/
│   └── tcl/
│       └── apollo_8_4g/
├── kernel/
│   └── mediatek/
├── vendor/
│   └── tcl/
├── recovery/
├── docs/
│   ├── hardware/
│   ├── partition-layout/
│   ├── boot-image/
│   └── development/
├── tools/
├── backups/
│   └── README.md
└── README.md
```

Directories are initialized with documentation placeholders. They do not yet contain a complete device tree, kernel source, or vendor blobs.

## Current research findings

- The stock boot image under examination is a 32 MiB image.
- Its embedded DTB was extracted and matched byte-for-byte by SHA-256 with the file named `apollo_boot_base.dtb`.
- The extracted base DTB reports a 512 MiB memory node, while the live device tree reports 2 GiB. The stock boot process therefore requires further investigation before using the extracted DTB as a source for a custom build.
- A merged DTB/DTBO artifact exists for analysis only. Successful overlay application does not establish boot compatibility.
- The stock system reports dynamic partitions. The OS A/B scheme has not been established.

See [device research](docs/hardware/device-research.md), [memory research](docs/hardware/memory-layout.md), and [boot image notes](docs/boot-image/boot-image.md).

## Safety and contribution rules

- Never commit private data, account credentials, device identifiers, or personal backups.
- Do not publish proprietary firmware or vendor binaries unless redistribution rights are confirmed.
- Do not flash experimental boot, recovery, vbmeta, super, or partition images without a verified backup and a device-specific recovery plan.
- Record the source firmware version, extraction method, hashes, and validation status for every binary artifact.
- Mark observations, hypotheses, and confirmed facts separately.

## License

The repository currently includes an MIT license. That license does not grant redistribution rights to third-party firmware, kernel code, vendor blobs, or other components copied into this project. Preserve each component's original license and notices.
