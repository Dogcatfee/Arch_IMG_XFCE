# Arch_IMG
Scripts to build x86_64-bit Arch Linux IMG files, that can be written similarly to RPi images. Attempts made to be compatible with existing Archiso recipies.

# TODO
* Get EFI working correctly
* Generate fstab
* More compatibility with existing Archiso scripts

# Default GIT build
Notable packages, includes AUR packages

   * Desktop
     - Lightdm ( enabled )
     - XFCE4
     - i3
   * Browsers
     - chromium
     - firefox
     - midori
   * Dev tools
     - vim
     - git
     - base-devel
   * Themes
     - Paper icons
     - Arc gtk themes
   * System
     - Gparted
     - Pacaur & Yaourt
     - TLP ( enabled )
     - sudo

# Basic requirement stuff:
  - Arch Linux install 64-bit
  - [TODO] Dependencies, base-devel, gpg key for AUR cower.
  - Enough disk space to install Arch. 1G For bare minimum IMG build. 5Gb for Default GIT Build. [Direct DISK build does not depend on main disk space]

# Default GIT Build
* Run `./yes_build_aur.sh` to do git and makepkg on AUR packages + enable AUR.
* Run `./build_image.sh` to build the image.

# Running IMG Builds
1. Run `./yes_aur.sh` to configure ./pacman.conf with ./aur_repo_x86_64 if using AUR. Run `./no_aur.sh` if not using AUR.
2. [Optional] Customize `./build_image.sh` to adjust *size, name, path* for image.
3. Customize packages to install in ./packages.both and ./packages.x86_64
4. Customize services, users, and other configurations in ./airootfs/root/customize_airootfs.sh
5. Run `./build_image.sh` to build `[default:./production_disk.img]`

# Running direct DISK Builds
WARNING: Will repartition disk in argument, and wipe. Does nothing by default.
1. Run `./yes_aur.sh` to configure ./pacman.conf with ./aur_repo_x86_64 if using AUR. Run `./no_aur.sh` if not using AUR.
2. [Optional] Customize `./build_on_usb.sh` to adjust partitions, defaults to filling disk.
3. Customize packages to install in ./packages.both and ./packages.x86_64
4. Customize services, users, and other configurations in ./airootfs/root/customize_airootfs.sh
5. Run `./build_on_usb.sh <device: ex:/dev/sda>` to build directly onto disk.
6. Example: `./build_on_usb.sh /dev/sdb` will wipe `/dev/sdb` and install Arch linux.

# Getting and enabling AUR packages
* AUR package git links are added to ./aur_git.links.
* Package names can be added or removed from ./packages.x86_64.
* Run `./yes_build_aur` to fetch and build packages that are listed in ./aur_git.links.
* AUR pacman config can be re-enabled with `./yes_aur.sh`.

# Disabling and deleting AUR packages
* Run `./no_aur.sh` to disable custom repo in pacman.conf.
* Run `./clean_aur.sh` to remove AUR repo and AUR_BUILDER files.
