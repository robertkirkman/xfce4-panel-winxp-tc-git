# xfce4-panel-winxp-tc-git
# This is an obsolete repo,
# superseded by: [xfce-winxp-tc-git](https://aur.archlinux.org/packages/xfce-winxp-tc-git)

xfce4-panel git version source package for **Arch Linux** with patch from [rozniak's fork](https://github.com/rozniak/xfce-winxp-tc-panel) for use with [rozniak's Windows XP Total Conversion for XFCE](https://github.com/rozniak/xfce-winxp-tc).

## Installation
- Two required build dependencies, `libxfce4ui-devel` and `libxfce4util-devel`, must be manually installed from AUR:
```sh
git clone https://aur.archlinux.org/libxfce4ui-devel.git
cd libxfce4ui-devel
makepkg -si
cd ..
git clone https://aur.archlinux.org/libxfce4util-devel.git
cd libxfce4util-devel
makepkg -si
cd ..
```
- OR, if using an AUR helper:
```sh
yay -S libxfce4ui-devel libxfce4util-devel
```
- Next, clone this repository and build and install this package:
```sh
git clone https://github.com/robertkirkman/xfce4-panel-winxp-tc-git.git
cd xfce4-panel-winxp-tc-git
makepkg -si
```
- To view the tweaked `xfce4-panel`, restart any instances of its binary (or log out and log into a session that automatically launches `xfce4-panel`).

Based on [`xfce4-panel-git` from AUR](https://aur.archlinux.org/packages/xfce4-panel-git/).
