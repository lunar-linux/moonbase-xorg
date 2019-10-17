if [[ $GALLIUM == y ]]; then
  # Mesa Gallium mklib breaks build when linker flags are set
  bad_flags linker &&
  OPTS+=" -Dosmesa=gallium \
          -Dgallium-xa=true \
          -Dgallium-extra-hud=true \
          -Dgallium-opencl=disabled"

#        -Dgallium-opencl=icd \
#        -Dgallium-nine=true \

  OPTS+=" -Dgallium-drivers=swrast,$(echo $GALLIUMDRIVER | sed s/\ /,/g)"
fi

if [[ $VULKAN == y ]]; then
  OPTS+=" -Dvulkan-drivers=$(echo $VULKANDRIVER | sed s/\ /,/g)"
fi

OPTS+=" -D platforms=x11,drm" &&
if in_depends $MODULE wayland-protocols; then
  OPTS+=",wayland"
fi

OPTS+=" -Db_lto=false \
        -Db_ndebug=true \
        -Dglx=dri \
        -Dgbm=true \
        -Degl=true \
        -Ddri3=true \
        -Dgles1=false \
        -Dgles2=true \
        -Dvalgrind=false \
        -Dshared-glapi=true \
        -Dswr-arches=avx,avx2 \
        -Ddri-drivers=$(echo $MESADRIVER | sed s/\ /,/g)" &&

default_meson_build &&

# indirect rendering
ln -s /usr/lib/libGLX_mesa.so.0 /usr/lib/libGLX_indirect.so.0
