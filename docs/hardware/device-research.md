# Device research: Alcatel 9032X

## Identity

| Property | Observed value |
|---|---|
| Product | `Apollo_8_4G` |
| Model | `9032X` |
| Android release | `10` |
| Build incremental | `1E24` |
| Build fingerprint | `Alcatel/9032X/Apollo_8_4G:10/QP1A.190711.020/1E24:user/release-keys` |
| Platform | `mt6761` |
| Kernel | `4.9.190+` |
| Kernel architecture | `armv7l` |
| Primary ABI | `armeabi-v7a` |
| RAM | 2 GiB |

These values were observed on the stock device. Confirm them again when switching firmware or device variants.

## Device tree observations

The extracted base DTB identifies the platform as MediaTek MT6761 and describes four Cortex-A53 CPU nodes.

The extracted tree also contains MediaTek display, pinctrl/GPIO, I2C, touch, and sensor descriptions. Multiple touch-controller nodes appear in the extracted tree; the active touch hardware must be identified from the live device and driver logs before choosing a final device-tree configuration.

A charger node being marked disabled in the stock tree is not evidence that it should be enabled in a custom tree.

## Confirmed versus pending

### Confirmed observations

- Stock Android 10 firmware is installed.
- The live kernel reports MT6761 and ARM 32-bit.
- The live device reports 2 GiB physical RAM.
- The live device reports dynamic partitions enabled.

### Pending investigation

- Exact active touchscreen controller and panel configuration.
- Exact charger IC and battery/charging integration.
- Complete stock kernel source and build configuration.
- Vendor blob inventory and redistribution permissions.
- Verified boot/recovery image format and partition flashing procedure.
- Whether the device uses an OS A/B slot scheme. Metadata slot copies and eMMC boot regions alone do not prove OS A/B.
