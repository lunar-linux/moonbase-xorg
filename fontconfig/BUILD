# We need to clear the cache dir or otherwise the build is going to fail
if [ -d /var/cache/fontconfig ]; then
  rm -f /var/cache/fontconfig/*
fi &&

OPTS+=" -D tests=disabled"

default_meson_build &&

install -m644 $SCRIPT_DIRECTORY/10-lunar-fonts.conf /etc/fonts/conf.d/
