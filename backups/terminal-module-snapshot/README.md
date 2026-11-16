# Terminal Module Snapshot

This is a partial, source-level snapshot of the existing Apollo_8_4G terminal module, recorded from the development conversation.

## Source device

- Device: Alcatel 9032X
- Product: Apollo_8_4G
- Android: 10
- Kernel: 4.9.190+
- Architecture: ARMv7 (32-bit)
- Root manager: Magisk 31.1

## Known module layout

```
terminal/
├── module.prop
└── system/
    └── etc/
        └── terminal/
            ├── README.txt
            └── bin/
                ├── kinfo
                └── sysinfo
```

## Included files

- `sysinfo`: reconstructed from the script content shown during development; see the adjacent file.

## Not included

- `kinfo`: the executable/script contents were not provided in the conversation, so it is not fabricated here.
- `module.prop` and the module's `README.txt`: their exact contents were not available.
- No device dump, private files, account details, serial numbers, or personal data are included.

## Backup status

Partial snapshot only. To make a complete backup, export the current module directory from the tablet and compare it with this snapshot before replacing or packaging anything.
