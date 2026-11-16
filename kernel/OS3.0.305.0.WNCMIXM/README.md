# Stock kernel module fallback

These original, unmodified modules come from the user-provided global
OS3.0.305.0.WNCMIXM Fastboot ROM. modules.json records their partition and SHA-256.
miev is from the unpacked vendor_boot ramdisk; nxp-nci is from vendor_dlkm.
Re-extract these exact files from those partitions when reproducing this baseline.

The houji device external-module adapter checks hashes, AArch64 ELF format,
vermagic flags and every versioned import against current source Module.symvers
before installing either file. Export CRCs used by later source builds come
from the original ELF tables, not invented compatibility values.

This is a temporary source-kernel bringup fallback for real Xiaomi event and
NXP NFC interfaces. Static checks passed with kernel 6.1.25-g7cbc6862bbca;
device loading and functional validation are still pending. Do not change
vermagic, bypass module version checks, or assume all stock modules are usable.

Module.symvers contains the five actual GPL export CRCs extracted from miev's
ELF tables. Core source modules need this input before external module staging;
the adapter regenerates it from the unchanged ELF and verifies the saved table
and hash on every build. It is not a fabricated compatibility symbol table.
