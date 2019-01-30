if [ ! -h /usr/X11R6 ] && [ -d /usr/X11R6 ]; then
  message "You still have the remains of XOrg6 lying around.";
  message "Please make sure you have read the XOrg7 upgrade";
  message "instructions at:";
  message "";
  message "http://wiki.lunar-linux.org/index.php/Install_XOrg7";
  message "";
  exit 1;
fi

OPTS+=" --prefix /usr \
        -Dlegacy=true"

meson $OPTS . build &&

cd build &&
ninja &&
prepare_install &&
ninja install &&

# cleanup
rm -f /usr/include/X11/extensions/{apple,windows}* &&
rm -f /usr/share/pkgconfig/{apple,windows}wmproto.pc &&
rm -f /usr/share/licenses/$MODULE/COPYING-{apple,windows}wmproto &&

touch $SOURCE_DIRECTORY/x11r7.rc &&

# we only need this when are installing in a different prefix then /usr
if [ ${MODULE_PREFIX} != /usr ]; then
  echo export PATH=\"$MODULE_PREFIX/bin:'$PATH'\" >> $SOURCE_DIRECTORY/x11r7.rc
  echo export PKG_CONFIG_PATH=\"$MODULE_PREFIX/lib/pkgconfig:'$PKG_CONFIG_PATH'\" >> $SOURCE_DIRECTORY/x11r7.rc
fi &&

# we still need to install the x11r7.rc file as it get sourced by all xorg7 modules
install -m644 $SOURCE_DIRECTORY/x11r7.rc /etc/profile.d/
