# Plank (raised indicators fork)

A fork of [Plank](https://github.com/ricotz/plank) with one fix and one extra theme:

- **Fix:** the dock's inner border line now respects the theme's
  `InnerStrokeColor` alpha. Upstream Plank always draws it partly see-through,
  so a fully transparent theme couldn't hide it.
- **TransparentRaised theme:** a fully transparent dock where the running-app
  indicator dots sit above the screen edge instead of touching it, with no
  visible line.

Everything else is unchanged upstream Plank. See `README` for the original readme.

## Install (Ubuntu / Debian)

1. Install the build dependencies:

   ```sh
   sudo apt install -y git valac autoconf automake libtool autopoint gettext pkg-config \
     libglib2.0-dev libgtk-3-dev libgee-0.8-dev libbamf3-dev libwnck-3-dev \
     libgnome-menu-3-dev libdbusmenu-gtk3-dev libx11-dev libxfixes-dev libxi-dev libxml2-utils
   ```

2. Build and install (to `/usr/local`, alongside any distro Plank):

   ```sh
   git clone -b transparent-inner-stroke https://github.com/darian7b7/plank.git
   cd plank
   ./autogen.sh --prefix=/usr/local --disable-apport --disable-docs
   make -j"$(nproc)"
   sudo make install
   sudo ldconfig
   ```

3. Restart Plank and select the theme:

   ```sh
   killall plank; plank &
   gsettings set net.launchpad.plank.dock.settings:/net/launchpad/plank/docks/dock1/ theme 'TransparentRaised'
   ```

   You can also pick **TransparentRaised** in `plank --preferences`.

## Adjusting the dot height

Copy the theme to your home folder and edit `LineWidth` (higher = dots further
up, 0 = touching the edge):

```sh
mkdir -p ~/.local/share/plank/themes
cp -r /usr/local/share/plank/themes/TransparentRaised ~/.local/share/plank/themes/
nano ~/.local/share/plank/themes/TransparentRaised/dock.theme
```

## Uninstall

From the cloned `plank` folder:

```sh
sudo make uninstall && sudo ldconfig
killall plank; plank &
```
