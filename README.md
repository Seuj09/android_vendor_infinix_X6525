# Infinix Smart 8 (X6525) — vendor tree

Vendor makefiles for the **Infinix Smart 8 X6525** (Unisoc T606 / UMS9230), for
use with the LineageOS 20 device tree:

- Device tree: <https://github.com/Seuj09/android_device_infinix_X6525> (`lineage-20`)
- Vendor tree: this repository (`lineage-20`)

LineageOS 20 (Android 13, SDK 33) is the target, matching the stock vendor
blobs. The device currently builds and boots with this tree.

## Blobs are not in this repository

`proprietary/` is git-ignored. Only the generated makefiles are tracked here;
the binaries are extracted from your own stock dump, so nothing proprietary is
redistributed.

Generated files that are tracked:

```
Android.bp                  # Soong prebuilt modules
Android.mk                  # legacy make glue
BoardConfigVendor.mk        # board flags (required by BoardConfig.mk)
X6525-vendor.mk             # PRODUCT_COPY_FILES / product packages
```

## Setting up

From the root of a LineageOS 20 source tree:

```bash
git clone https://github.com/Seuj09/android_device_infinix_X6525 \
    -b lineage-20 device/infinix/X6525
git clone https://github.com/Seuj09/android_vendor_infinix_X6525 \
    -b lineage-20 vendor/infinix/X6525
```

Then extract the blobs from a stock dump:

```bash
# dump layout: system/ system_ext/ product/ vendor/ odm/ ...
device/infinix/X6525/extract-files.sh /path/to/x6525-dump
```

`extract-files.sh` runs the usual LineageOS `extract_utils.sh` flow using
`device/infinix/X6525/proprietary-files.txt` and writes into `proprietary/`.

To regenerate the blob list from a fresh dump (for example after an OTA):

```bash
python3 tools/gen-blob-list.py /path/to/x6525-dump \
    -o device/infinix/X6525/proprietary-files.txt
```

The dump is easiest to produce from the stock `super` partition:

```bash
lpunpack super.img /path/to/dump
```

## Building

```bash
source build/envsetup.sh
lunch lineage_X6525-userdebug
mka bacon
```

## Notes

- Dynamic partitions: `system system_ext vendor product odm vendor_dlkm`.
- A/B with virtual A/B; `boot` holds the GKI kernel, `vendor_boot` holds the
  DTB and vendor ramdisk, plus a separate `dtbo`.
- The makefiles here were generated from the stock dump and are kept in sync
  with `device/infinix/X6525`. If you change one side, regenerate both.

Blob licensing: these files are proprietary to Infinix/Transsion/Unisoc. Use
them only on hardware you own.
