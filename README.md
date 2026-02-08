# my arch-setup

- create ESP and root partition using `cfdisk`
- format ESP with `mkfs.fat -F32 *esp*` and format root partition with `mkfs.ext4 *root_partition*`
- mount root partition with `mount *root_partition* /mnt` and ESP with `mount --mkdir *esp* /mnt/boot`
- install packages 
```bash 
pacstrap -K /mnt base base-devel linux linux-firmware networkmanager grub efibootmgr ly niri mako fuzzel udiskie xdg-desktop-portal-gtk xdg-desktop-portal-gnome swaybg swaylock pipewire pipewire-session-manager pipewire-pulse wireplumber git helix sudo nano kitty egl-wayland nvidia-dkms nvidia-utils
```
- generate fstab `genfstab -U /mnt >> /mnt/etc/fstab`
- chroot into system `arch-chroot /mnt`
- set root password with `passwd`
- add user with `useradd -m *user*`
- set user password with `passwd *user*`
- set visudo editor `EDITOR=helix visudo /etc/sudoers.d/10-editor`
- write this inside:
```bash
Defaults editor=/usr/bin/helix, !env_editor
```
- run `visudo` and uncomment wheel section to give sudo privilige to wheel group
- add user to wheel group with `usermod -aG wheel *user*`
- enable display manager with `systemctl enable ly@tty2.service`
- disable getty@tty2 service `systemctl disable getty@tty2.service`
- enable NetworkManager `systemctl enable NetworkManager.service`
- install grub `grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=Arch`
- generate grub config `grub-mkconfig -o /boot/grub/grub.cfg`
- exit chroot
- unmount with `umount -R /mnt` (optional)
- reboot and pray
- done
