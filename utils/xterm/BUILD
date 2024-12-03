. /etc/profile.d/x11r7.rc &&

OPTS+=" --with-app-defaults=/etc/X11/app-defaults \
        --disable-imake \
        --enable-logging \
        --enable-88-color \
        --enable-256-color"

LDFLAGS+=" -lncurses"

default_build &&

# cosmetic but needed adjustments:
if ! grep -q 'XTerm*loginShell:' /etc/X11/app-defaults/XTerm; then
  echo 'XTerm*loginShell: true' >> /etc/X11/app-defaults/XTerm &&
  echo 'XTerm*loginShell: true' >> /etc/X11/app-defaults/XTerm-color
fi &&

install -Dm 644 {,/usr/share/applications/}xterm.desktop
