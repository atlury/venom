# Venom Linux

This repo contain scripts to bootstrap base system of venom linux. Venom Linux is distro inspired by [CRUX](https://crux.nu) but based on [LFS](http://www.linuxfromscratch.org/lfs/) and [BLFS](http://www.linuxfromscratch.org/blfs/) with multilib enabled targetting experienced users. Venom Linux use 'KISS' philosophy for packages. It use BSD-style init and BSD-like port system for packages. 

You can get prebuilt iso of this distro [here](https://sourceforge.net/projects/venomlinux/) which you can install to your machine if you dont want to bootstrap it yourself. The available iso is base, xorg, lxde, mate and xfce4.

### Bootstrap Benom Linux

Run `./01-toolchain` to build temporary toolchain (multilib). Then run `./02-base` to build base system of Venom Linux. `/mnt/lfs` directory is used to build this distro, so make sure you dont have any important files in this directory before run the script. Use `chroot` script to chroot into Venom Linux base system to configure it by running `./chroot /mnt/lfs`.

### Configure Venom Linux (through chroot)

hostname, timezone, clock, font, keymap and daemon:

    # vim /etc/rc.conf

partitions (/, swap and etc):

    # vim /etc/fstab
    
locales:

    # vim /etc/locales
    # genlocales

root password:

    # passwd
    
add user:

    # useradd -m -G users,wheel,audio,video -s /bin/bash <your user>
    # passwd <your user>
    
install grub:

    # grub-install /dev/sdX
    # grub-mkconfig -o /boot/grub/grub.cfg
    
### Package manager

This distro come with custom package manager called [scratchpkg](https://github.com/emmett1/scratchpkg). This some basic command of this package manager that you should know:

installing packages:

    # scratch install <pkg1> <pkg2> <pkgN>
    
removing packages:

    # scratch remove <pkg1> <pkg2> <pkgN>
    
search packages:

    # scratch search <pattern>
    
update packages repo:

    # scratch sync
    
full system upgrade (should run after updating packages repo):

    # scratch sysup

fix broken packages (recommended run after full system upgrade or after removing packages):

    # revdep -r
    
update packages configuration files (recommended run after packages upgraded):

    # updateconf
    
### Notes

- run `scratch help` to see available options for `scratch`
- run `revdep -h` to see available options for `revdep`

