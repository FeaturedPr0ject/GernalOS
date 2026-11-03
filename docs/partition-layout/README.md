# Partition layout

This directory is reserved for a verified partition map for Alcatel 9032X / Apollo_8_4G.

Known observations include a 32 MiB boot partition, a 32 MiB recovery partition, a super partition of approximately 4.61 GiB, and a userdata partition. Exact sizes, names, offsets, and flash procedures must be confirmed from fresh device output and the matching firmware.

Do not treat eMMC boot regions such as `preloader_a` and `preloader_b` as proof of Android OS A/B slots.
