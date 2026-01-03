# Debian Live Build

Git repository: https://salsa.debian.org/live-team/live-build.git

```
git clone https://salsa.debian.org/live-team/live-build.git debian-live-build
cd debian-live-build
sudo make install
sudo lb --version
sudo lb clean --purge
sudo lb config
sudo lb build
```

We will have `live-image-amd64.hybrid.iso` ready to boot.

# BlankOn Live Build

Git repository: https://github.com/BlankOn/blankon-live-build/

This repository contains configuration and script to build the ISO using Debian Live Build tool. Because of the nature of `lb` commands that could make a mess of the original configuration, the build script (`build.sh`) need to be run on separate working directory.

```
git clone https://github.com/BlankOn/blankon-live-build
mkdir live-build-workdir
cp blankon-live-build/build.sh live-build-workdir/build.sh
cd live-build-workdir
sudo ./build.sh https://github.com/BlankOn/blankon-live-build verbeek
```

## General Workflow

<img src="https://github.com/BlankOn/revival/blob/main/assets/images/blankon-live-build-workflow.png?raw=true"/>

## Configuration Overview

- `config/binary` - Configuration that represent the compiled binary of the ISO
- `config/boostrap` - Anything that related to bootstrap
- `config/chroot` - Anything that related to chroot.
- `config/common` - Distribution and package related
- `config/source` - Package source configuration
- `config/archives/blankon.key.binary` and `config/archives/blankon.key.chroot` - Initially the `lb` will try to use the keyring package from `--keyring-packages blankon-keyring` argument, but in some cases, especially in chroot reconfiguration, these package is still missing and these `blankon.key.*` will serve as backup.
- `config/bootloaders` - Boot loader configuration, currently using GRUB with custom background (`config/bootloaders/grub-legacy/splash.xpm.gz`)
- `config/hooks` - Small modifications to the system will be maintained here. If a modification is heavily tied to certain packages, then these packages should be updated instead. Smaller number will be executed first. Higher number will override the smaller ones.
  - `config/hooks/live` - The hooks that will be executed when the OS booted in live session.
  - `config/hooks/normal` - The hooks that will be executed during the ISO build process
- `config/package-lists/live.list.chroot` - The list of the package that will be prepared for live session. There are live session specific packages listed here like `live-boot`, `live-config`, `live-config-systemd`

## What are important to setup / package / modify

- Branding
  - `/etc/os-release`
  - About interface in GNOME's Settings
  - Default GRUB background
  - Default desktop background / wallpaper
  - Installer customization
- Default apps
- System behaviours
  - Default services
- System convention
  - Default font, etc

# References

- https://www.debian.org/devel/debian-live/
- https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html
- From BlankOn wiki: https://github.com/BlankOn/wiki/blob/master/TimPengembang/Pemaket/LiveBuild.md
