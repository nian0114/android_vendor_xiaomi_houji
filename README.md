# Xiaomi houji proprietary files

Source: Xiaomi 14 Global Fastboot ROM `OS3.0.305.0.WNCMIXM` (Android 16),
`houji_global_images_OS3.0.305.0.WNCMIXM_20261015.0000.00_16.0_global_ef90c126ec.tgz`.

Generated with `device/xiaomi/houji/extract-files.py --kang` and its common module.
The matching device proprietary lists record the source and post-fixup hashes.
Both userspace vendor trees use this same ROM, including IMS; no older IMS or Pixel blobs are included.
The modem firmware exception for the CN test device is recorded below.
Vendor security patch: `2026-10-01`. Runtime compatibility still needs build and device validation.

Firmware images under `radio/` use Git LFS. Install Git LFS before cloning or syncing.

## Stock kernel bundle

`kernel/stock/` is extracted from the same ROM with
`device/xiaomi/houji/extract-kernel.py`. It contains the unmodified boot kernel,
the complete concatenated vendor_boot DTB, the DTBO table without stock AVB
padding/footer, and all module trees from vendor_boot, vendor_dlkm and system_dlkm.
The Lineage build generates and signs its own boot/vendor_boot/DTBO images.

The bundle has 340 ramdisk, 313 vendor_dlkm and 60 system_dlkm modules. The
versioned system_dlkm layout and stock loading metadata are preserved. Modules
are not stripped or patched, so module signatures and KMI data remain intact.
`provenance.json` records the ROM, kernel release and source image hashes;
`SHA256SUMS` covers every extracted file. Do not mix this bundle with the older
MiCode source-built Image or modules. Source-mode compatibility material under
`kernel/OS3.0.305.0.WNCMIXM/` remains separate.

## CN radio firmware exception

The bring-up phone reports `ro.boot.hwc=CN`. The initial Global radio pair
booted its modem but returned `NO_RF_CALIBRATION_INFO` on both radio-power
requests. To restore its original radio baseline, `radio/modem.img` and
`radio/modemfirmware.img` are taken together from the user's official China
`OS3.0.307.0.WNCCNXM` Fastboot images. All other firmware and the complete
kernel/userspace vendor baseline remain Global OS3.0.305.0.WNCMIXM.

| Packaged image | Original file | SHA-256 |
| --- | --- | --- |
| modem.img | NON-HLOS.bin | 3ccb918129b84228c6e3454969a83ba24f6df5e72ca10488e9044a0d11c21d8b |
| modemfirmware.img | MODEM-FW.bin | 66dcc89d63d047a8d0a1f70139c09f7378d82387e21d83fa062636447b5315fa |

This is a CN-specific bring-up choice, not a claim that this pair is
appropriate for Global hardware. On-device radio recovery still requires
validation after installing it. No per-device persist/NV images are
included or replaced. See `device/xiaomi/houji/docs/dev/radio-firmware.md`
for extraction and verification notes.
