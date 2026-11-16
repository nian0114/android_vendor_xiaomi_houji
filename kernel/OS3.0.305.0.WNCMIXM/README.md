# Stock kernel module fallback

These original, unmodified modules come from the user-provided global
OS3.0.305.0.WNCMIXM Fastboot ROM. modules.json records their partition and SHA-256.
miev is from the unpacked vendor_boot ramdisk; nxp-nci, spcom and spss_utils
are from vendor_dlkm.
Re-extract these exact files from those partitions when reproducing this baseline.

The houji device external-module adapter checks hashes, AArch64 ELF format,
vermagic flags and every versioned import against current source Module.symvers
before installing any selected file. Export CRCs used by later source builds come
from the original ELF tables, not invented compatibility values.

This is a temporary source-kernel bringup fallback for real Xiaomi event and
NXP NFC and SPSS communication/control interfaces. Static checks for the initial
two modules passed with kernel 6.1.25-g7cbc6862bbca;
device loading and functional validation are still pending. Do not change
vermagic, bypass module version checks, or assume all stock modules are usable.

Module.symvers contains original export CRCs extracted from the selected ELF
tables. The adapter regenerates it from the unchanged files and verifies the
saved table and hash on every build. Future source consumers must opt into
this table explicitly after interface validation; the core build does not
receive it. It is not a fabricated compatibility symbol table.

spcom.ko and spss_utils.ko are selected for active qcom,spcom and
qcom,spss-utils nodes in both product DT variants. Both import only matching
current source symbols, including qcom_spss and the IPC logging provider.
Their DT properties match stock after normalizing remoteproc provider
phandles. Firmware, remoteproc interaction and userspace behavior still need
device validation. This does not permit other stock modules automatically.
