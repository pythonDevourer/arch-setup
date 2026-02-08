# arch-setup

- create ESP and root partition using `cfdisk`
- format ESP with `mkfs.fat -F32 *esp_partition*` and format root partition with `mkfs.ext4 *root_partition*`
- mount them with `mount`
