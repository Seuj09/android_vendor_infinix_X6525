# vendor/infinix/X6525

This directory is **generated** by `device/infinix/X6525/extract-files.sh` from
your own dump. It is intentionally empty in this scaffold.

After running:

```bash
python3 tools/gen-blob-list.py ~/x6525-dump -o device/infinix/X6525/proprietary-files.txt
device/infinix/X6525/extract-files.sh ~/x6525-dump
```

you should see:

```
Android.bp
Android.mk
BoardConfigVendor.mk        <- required by BoardConfig.mk
X6525-vendor.mk             <- inherited by device.mk
proprietary/                <- the blobs
```

Until `BoardConfigVendor.mk` exists, the build will stop with an error about a
missing file. That is expected.

Keep this directory out of a public git repo unless you have redistribution
rights for the blobs. Most X6525 trees keep only the makefiles in git and
regenerate `proprietary/` locally.
