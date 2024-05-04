# Thumbdrive grub boot selector
A simple grub script, that sets the default boot entry based on a thumbdribe being connected or not

## Installation

1. Create a file in `/etc/grub.d/01_thumbdrive_selector`
2. Write the following content to it:
```bash
#! /bin/sh

cat << 'EOF'
search --no-floppy --fs-uuid --set thumbdrive <fs-uuid>
if [ "${thumbdrive}" ] ; then
  set default="2" # Set boot entry 2 as default (Windows)
else
  set default="0" # Set boot entry 0 as default (Linux)
fi

EOF
```
3. Find an fs uuid to use for detecting the thumbdrive with `blkid`. It should look something like this: `xxxx-xxxx`
4. Replace `<fs-uuid>` with the id you got from step 3
5. Make the script executable with `chmod +x /etc/grub.d/01_thumbdrive_selector`
6. Run `update-grub`
