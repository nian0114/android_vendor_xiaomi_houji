# Late stock module group

These unmodified files are from the same global OS3.0.305.0.WNCMIXM dump as
the bootstrap group in the parent directory. modules.json records exact
partition provenance and SHA-256; Module.symvers contains original ELF exports.

btpower depends on source-built securemsm. bt_fm_slim additionally depends on
btpower and the bootstrap miev module. Keep provider-before-consumer order.
The device stock-extra adapter runs after source external drivers and verifies
all imports against their actual symbol tables and earlier verified blobs.

Bluetooth DT descriptions are restored from the same stock merged trees in
kernel/xiaomi/houji-devicetrees/qcom/houji-sm8650-bluetooth.dtsi. No module
bytes, version strings or imported CRCs are changed. Successful static checks
do not establish runtime CFI, power sequencing, SLIM or Bluetooth audio behavior.
