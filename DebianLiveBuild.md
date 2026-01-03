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

# References

- https://www.debian.org/devel/debian-live/
- https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html
- From BlankOn wiki: https://github.com/BlankOn/wiki/blob/master/TimPengembang/Pemaket/LiveBuild.md
