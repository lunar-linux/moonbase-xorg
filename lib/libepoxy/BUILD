# Reduce docs size
printf '%s\n' >>doc/Doxyfile.in \
   HAVE_DOT=yes DOT_IMAGE_FORMAT=svg INTERACTIVE_SVG=yes &&

OPTS+=" -Degl=yes" &&

# avoid a circular depend with mesa-lib (via gtk+-3 libinput)
if module_installed mesa-lib; then
   OPTS+=" -Dglx=yes"
else
   OPTS+=" -Dglx=no"
fi

default_meson_build
