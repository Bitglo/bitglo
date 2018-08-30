
Debian
====================
This directory contains files used to package bitglod/bitglo-qt
for Debian-based Linux systems. If you compile bitglod/bitglo-qt yourself, there are some useful files here.

## bitglo: URI support ##


bitglo-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install bitglo-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your bitglo-qt binary to `/usr/bin`
and the `../../share/pixmaps/bitglo128.png` to `/usr/share/pixmaps`

bitglo-qt.protocol (KDE)

