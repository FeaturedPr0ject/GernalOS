# Memory layout research

## Important discrepancy

The extracted base DTB contains this memory declaration:

```dts
memory {
    device_type = "memory";
    reg = <0x00 0x40000000 0x00 0x20000000>;
};
```

With two address cells and two size cells, this describes a region starting at `0x40000000` with a size of `0x20000000` (512 MiB).

The live device tree reports:

- `#address-cells = 2`
- `#size-cells = 2`
- memory base `0x40000000`
- memory size `0x80000000` (2 GiB)

The live system also reports approximately 1.8 GiB in `MemTotal`, which is consistent with a 2 GiB device after memory reservations.

## Live reserved-memory observations

The live tree contains MediaTek reservation nodes for items including TEE, ATF, framebuffer, SSPM, CCCI/modem shared memory, SCP, Wi-Fi, GPU, and persistent logs.

Selected live `mblock` ranges observed during research:

| Node | Start | Size |
|---|---:|---:|
| mblock-1-dramc-rk0 | `0xBFFFF000` | 4 KiB |
| mblock-2-log_store | `0x7FFC0000` | 4 MiB |
| mblock-3-atf-reserved | `0x47D80000` | 4 MiB |
| mblock-4-atf-log-reserved | `0xBFFBF000` | 256 KiB |
| mblock-5-SSPM-reserved | `0x7FEC0000` | 1 MiB |
| mblock-6-tee-reserved | `0x7D6C0000` | 40 MiB |
| mblock-7-ram_console | `0x47C80000` | 64 KiB |
| mblock-8-pstore | `0x47C90000` | 896 KiB |
| mblock-9-minirdump | `0x47D70000` | 64 KiB |
| mblock-10-framebuffer | `0x7C910000` | 13.6875 MiB |
| mblock-11-atf-ramdump-memory | `0xBFF30000` | 512 KiB |
| mblock-12-SPM-reserved | `0x77FF0000` | 64 KiB |
| mblock-13-ccci_tag_mem | `0x9FFF0000` | 64 KiB |
| mblock-14-ccci | `0xAE000000` | 256 MiB |
| mblock-15-md_smem_ncache | `0x72000000` | 1.4375 MiB |
| mblock-16-ccci | `0x7A000000` | 22 MiB |

These are observations from the live device tree, not a finished custom memory map. Do not copy them into a new device tree without understanding the bootloader, kernel reservation code, and firmware contract.

## Investigation conclusion

The extracted base DTB does not match the live memory size declaration. The live tree has additional `mblock` entries not found in the extracted base DTB or the examined DTBO. This suggests that another boot stage may modify or supplement the tree, but the responsible stage has not been proven.

**Do not use the extracted base DTB unchanged as the final ApolloOS memory configuration.**
