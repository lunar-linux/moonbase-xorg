# Reduce docs size
printf '%s\n' >>doc/Doxyfile.in \
   HAVE_DOT=yes DOT_IMAGE_FORMAT=svg INTERACTIVE_SVG=yes &&

mkdir build &&

cd build &&

# avoid a circular depend with mesa-lib (via gtk+-3 libinput)
if module_installed mesa-lib; then
   OPTS+=" -Dglx=yes -Degl=yes"
else
   OPTS+=" -Dglx=no -Degl=no"
fi &&

meson --prefix /usr \
      $OPTS && 

ninja &&

prepare_install &&

ninja install
