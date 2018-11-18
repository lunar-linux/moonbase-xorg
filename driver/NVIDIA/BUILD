if [[ `arch` == x68_64 ]]; then
  ARCH=`arch`
else
  ARCH=x86
fi &&

# This check needs to check the kernel it's built against, not the running kernel.
if [ -f /usr/src/linux/vmlinux.o ]; then
  GCCKNL=$(strings -a /usr/src/linux/vmlinux.o | grep 'GCC: (' | head -1 | awk '{ print $3 }') &&
  GCCNOW=$(gcc --version | grep gcc | cut -d\  -f3) &&
    if [[ "$GCCKNL" != "$GCCNOW" ]]; then
      message "${PROBLEM_COLOR}"                                    \
              "The kernel is compiled using gcc version: $GCCKNL"   \
              "but you try to compile nvidia kernel module with"    \
              "gcc version: $GCCNOW. You can not use different"     \
              "gcc to build kernel and modules. Please lin kernel"  \
              "with current gcc, then reboot and lin nvidia driver."\
              "${DEFAULT_COLOR}" &&
        false
    fi
fi &&

# Temporary paths and symlinks to make sources compilable
LD_LIBRARY_PATH="$SOURCE_DIRECTORY:$LD_LIBRARY_PATH" &&
CFLAGS="-L$SOURCE_DIRECTORY $CFLAGS"                 &&
export SYSSRC=/usr/src/linux                         &&

ln -s libnvidia-glcore.so.$VERSION nvidia-installer-$VERSION/libGLcore.so.1     &&
ln -s libnvidia-tls.so.$VERSION    nvidia-installer-$VERSION/libnvidia-tls.so.1 &&

echo libXvMCNVIDIA_dynamic.so.1 > XvMCConfig &&

# build installer
cd nvidia-installer-$VERSION &&

 make rebuild_tls_test &&
 make rebuild_tls_test_dso &&
# make rebuild_rtld_test.unstripped &&
 make &&

 install -m 755 _out/*/nvidia-installer      .. &&
 install -m 755 _out/*/mkprecompiled         .. &&
 install -m 644 _out/*/nvidia-installer.1.gz .. &&
 cp             tls_test_Linux-$ARCH         ../tls_test        &&
 cp             tls_test_dso_Linux-$ARCH.so  ../tls_test_dso.so &&

cd .. &&

# optionally build nvidia-settings
if in_depends $MODULE "gtk+-3" ; then
  export GTK3_AVAILABLE=$(usex gtk3 1 0) 1
  cd nvidia-settings-$VERSION &&

  make -C src/libXNVCtrl clean &&
  make -C src/libXNVCtrl &&
  make &&

  install -m 755 src/_out/*/nvidia-settings .. &&
  install -m 644 doc/_out/*/nvidia-settings.1.gz .. &&
  sedit 's/__UTILS_PATH__/\/usr\/bin/' doc/nvidia-settings.desktop &&
  sedit 's/__PIXMAP_PATH__/\/usr\/share\/doc\/NVIDIA_GLX-1.0/' doc/nvidia-settings.desktop &&
  sedit 's/__NVIDIA_SETTINGS_DESKTOP_CATEGORIES__/Settings;DesktopSettings;/' doc/nvidia-settings.desktop &&
  cd ..
fi &&

# build nvidia-xconfig
cd nvidia-xconfig-$VERSION &&

 make &&

 install -m 755 _out/*/nvidia-xconfig      .. &&
 install -m 644 _out/*/nvidia-xconfig.1.gz .. &&

cd .. &&

# We make the kernel modules on our own
KVER=$(cat /usr/src/linux/include/config/kernel.release) &&
cd kernel &&
make module KERNEL_UNAME=$KVER &&
rm -f $SOURCE_DIRECTORY/{libGL.so,libGLcore.so.1,libnvidia-tls.so.1} &&
# We don't want to track the kernel module
make modules_install KERNEL_UNAME=$KVER &&

prepare_install &&

install -dm 0755 /usr/lib/modprobe.d &&
echo "blacklist nouveau" > /usr/lib/modprobe.d/nvidia.conf &&
touch /usr/lib/modprobe.d/nvidia.conf &&
cd .. &&

# Driver
install -D -m755 nvidia_drv.so /usr/lib/xorg/modules/drivers/nvidia_drv.so &&

# GLX extension
install -D -m755 libglxserver_nvidia.so.${VERSION} /usr/lib/nvidia/xorg/libglxserver_nvidia.so.${VERSION} &&
ln -sf libglxserver_nvidia.so.${VERSION} /usr/lib/nvidia/xorg/libglxserver_nvidia.so.1 &&
ln -sf libglxserver_nvidia.so.${VERSION} /usr/lib/nvidia/xorg/libglxserver_nvidia.so &&

install -D -m755 libGLX_nvidia.so.${VERSION} /usr/lib/libGLX_nvidia.so.${VERSION} &&
ln -sf libGLX_nvidia.so.${VERSION} /usr/lib/libGLX_nvidia.so.0 &&
ln -sf libGLX_nvidia.so.${VERSION} /usr/lib/libGLX_nvidia.so &&

# VDPAU
install -D -m755 libvdpau_nvidia.so.${VERSION} /usr/lib/vdpau/libvdpau_nvidia.so.${VERSION} &&
ln -sf libvdpau_nvidia.so.${VERSION} /usr/lib/vdpau/libvdpau_nvidia.so.1 &&
ln -sf libvdpau_nvidia.so.1 /usr/lib/vdpau/libvdpau_nvidia.so &&

# OpenGL
install -D -m755 libEGL_nvidia.so.${VERSION} /usr/lib/libEGL_nvidia.so.${VERSION} &&
ln -sf libEGL_nvidia.so.${VERSION} /usr/lib/libEGL_nvidia.so.0 &&
ln -sf libEGL_nvidia.so.${VERSION} /usr/lib/libEGL_nvidia.so &&
install -D -m755 libGLESv1_CM_nvidia.so.${VERSION} /usr/lib/libGLESv1_CM_nvidia.so.${VERSION} &&
ln -sf libGLESv1_CM_nvidia.so.${VERSION} /usr/lib/libGLESv1_CM_nvidia.so.1 &&
ln -sf libGLESv1_CM_nvidia.so.${VERSION} /usr/lib/libGLESv1_CM_nvidia.so &&
install -D -m755 libGLESv2_nvidia.so.${VERSION} /usr/lib/libGLESv2_nvidia.so.${VERSION} &&
ln -sf libGLESv2_nvidia.so.${VERSION} /usr/lib/libGLESv2_nvidia.so.2 &&
ln -sf libGLESv2_nvidia.so.${VERSION} /usr/lib/libGLESv2_nvidia.so &&
install -D -m644 10_nvidia.json /usr/share/glvnd/egl_vendor.d/10_nvidia.json &&

# CUDA
install -D -m755 libcuda.so.${VERSION} /usr/lib/libcuda.so.${VERSION} &&
ln -sf /usr/lib/libcuda.so.$VERSION /usr/lib/libcuda.so.1 &&
ln -sf /usr/lib/libcuda.so.1 /usr/lib/libcuda.so &&

# OpenCL
install -m0755 libOpenCL.so.1.0.0 /usr/lib &&
ln -sf /usr/lib/libOpenCL.so.1.0.0 /usr/lib/libOpenCL.so.1.0 &&
ln -sf /usr/lib/libOpenCL.so.1.0 /usr/lib/libOpenCL.so.1 &&
ln -sf /usr/lib/libOpenCL.so.1 /usr/lib/libOpenCL.so &&

# Other libs
install -m0755 libnv*.so.$VERSION /usr/lib &&
#install -m0755 libGL.so.$VERSION /usr/lib &&

# TLS lib
install -D -m755 tls/libnvidia-tls.so.${VERSION} /usr/lib/tls/libnvidia-tls.so.${VERSION} &&

install -D -m644 nvidia.icd /etc/OpenCL/vendors/nvidia.icd &&
install -D -m755 nvidia-bug-report.sh /usr/bin/nvidia-bug-report.sh &&
install -D -m755 nvidia-debugdump /usr/bin/nvidia-debugdump &&
install -D -m755 nvidia-smi /usr/bin/nvidia-smi &&
install -D -m644 nvidia-smi.1.gz /usr/share/man/man1/nvidia-smi.1.gz &&
install -D -m755 nvidia-xconfig /usr/bin/nvidia-xconfig &&
install -D -m644 nvidia-xconfig.1.gz /usr/share/man/man1/nvidia-xconfig.1.gz &&
install -D -m755 nvidia-cuda-mps-server /usr/bin/nvidia-cuda-mps-server &&
install -D -m755 nvidia-cuda-mps-control /usr/bin/nvidia-cuda-mps-control &&
install -D -m644 nvidia-cuda-mps-control.1.gz /usr/share/man/man1/nvidia-cuda-mps-control.1.gz &&
install -D -m755 nvidia-modprobe /usr/bin/nvidia-modprobe &&
install -D -m644 nvidia-modprobe.1.gz /usr/share/man/man1/nvidia-modprobe.1.gz &&
install -D -m755 nvidia-persistenced /usr/bin/nvidia-persistenced &&
install -D -m644 nvidia-persistenced.1.gz /usr/share/man/man1/nvidia-persistenced.1.gz &&
install -D -m644 nvidia-persistenced-init/systemd/nvidia-persistenced.service.template /usr/lib/systemd/system/nvidia-persistenced.service &&

# Lib symlinks
ln -sf libnvidia-cfg.so.$VERSION /usr/lib/libnvidia-cfg.so.1 &&
ln -sf libnvidia-cfg.so.$VERSION /usr/lib/libnvidia-cfg.so &&
ln -sf libnvcuvid.so.$VERSION /usr/lib/libnvcuvid.so &&
ln -sf libnvidia-cbl.so.$VERSION /usr/lib/libnvidia-cbl.so &&
ln -sf libnvidia-eglcore.so.$VERSION /usr/lib/libnvidia-eglcore.so &&
ln -sf libnvidia-encode.so.$VERSION /usr/lib/libnvidia-encode.so.1 &&
ln -sf libnvidia-encode.so.$VERSION /usr/lib/libnvidia-encode.so &&
ln -sf libnvidia-fatbinaryloader.so.$VERSION /usr/lib/libnvidia-fatbinaryloader.so &&
ln -sf libnvidia-fbc.so.$VERSION /usr/lib/libnvidia-fbc.so.1 &&
ln -sf libnvidia-fbc.so.$VERSION /usr/lib/libnvidia-fbc.so &&
ln -sf libnvidia-glcore.so.$VERSION /usr/lib/libnvidia-glcore.so &&
ln -sf libnvidia-glsi.so.$VERSION /usr/lib/libnvidia-glsi.so &&
ln -sf libnvidia-glvkspirv.so.$VERSION /usr/lib/libnvidia-glvkspirv.so &&
ln -sf libnvidia-ifr.so.$VERSION /usr/lib/libnvidia-ifr.so.1 &&
ln -sf libnvidia-ifr.so.$VERSION /usr/lib/libnvidia-ifr.so &&
ln -sf libnvidia-ml.so.$VERSION /usr/lib/libnvidia-ml.so.1 &&
ln -sf libnvidia-ml.so.$VERSION /usr/lib/libnvidia-ml.so &&
ln -sf libnvidia-ptxjitcompiler.so.$VERSION /usr/lib/libnvidia-ptxjitcompiler.so.1 &&
ln -sf libnvidia-ptxjitcompiler.so.$VERSION /usr/lib/libnvidia-ptxjitcompiler.so &&
ln -sf libnvidia-rtcore.so.$VERSION /usr/lib/libnvidia-rtcore.so &&
ln -sf libnvidia-tls.so.$VERSION /usr/lib/libnvidia-tls.so &&
ln -sf libnvidia-wfb.so.$VERSION /usr/lib/libnvidia-wfb.so.1 &&
ln -sf libnvidia-wfb.so.$VERSION /usr/lib/libnvidia-wfb.so &&
ln -sf libnvoptix.so.$VERSION /usr/lib/libnvoptix.so.1 &&
ln -sf libnvoptix.so.$VERSION /usr/lib/libnvoptix.so &&

# Register Nvidia XvMC library for use in any XvMC enabled media player
install -m644 XvMCConfig /etc/X11 &&

install -D -m644 $SCRIPT_DIRECTORY/10-nvidia-drm-outputclass.conf /usr/share/X11/xorg.conf.d/10-nvidia-drm-outputclass.conf &&
install -D -m644 $SCRIPT_DIRECTORY/50-nvidia.conf /usr/share/X11/xorg.conf.d/50-nvidia.conf &&

if in_depends $MODULE "gtk+-3" ; then
  install -m0755 nvidia-settings /usr/bin &&
  install -m0444 nvidia-settings-$VERSION/doc/nvidia-settings.desktop /usr/share/applications &&
  install -m0444 nvidia-settings-$VERSION/doc/nvidia-settings.png /usr/share/doc/NVIDIA_GLX-1.0 &&
  install -m0444 nvidia-settings.1.gz /usr/share/man/man1
fi &&

gather_docs README.txt LICENSE NVIDIA_Changelog
