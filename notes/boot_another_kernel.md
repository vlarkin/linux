
## How to configure GRUB to boot another kernel


Open the file `/etc/default/grub` with GRUB variables and set the following
```text
GRUB_DEFAULT=saved
```

Look into the GRUB configuration file for id options
```console
grep menuentry /boot/grub/grub.cfg
```

Choose a long menuenty option id you want to boot and set it for the next boot
```console
grub-reboot "menuentry_id_option"
```

If you have submenu entries, use first a submenu option id and when ">" with a menuenty option id
```console
grub-reboot "submenu_id_option>menuentry_id_option"
```

Update GRUB configuration and reboot
```console
update-grub
reboot
```

If another kernel works fine, set it by default
```console
grub-set-default "submenu_id_option>menuentry_id_option"
update-grub
```

