. /etc/profile.d/x11r7.rc &&

autoreconf -fi &&

default_build &&

mkdir -p /etc/X11/xorg.conf.d
install -m644 $SCRIPT_DIRECTORY/11-evdev-mouse.conf /etc/X11/xorg.conf.d/
