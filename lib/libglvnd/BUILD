autoreconf -fi &&

if module_installed mesa-lib; then
  # for GLX and EGL support
  OPTS+=" --enable-glx --enable-egl"
fi &&

default_build
