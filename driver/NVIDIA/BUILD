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

ln -s libGL.so.$VERSION            nvidia-installer-$VERSION/libGL.so           &&
ln -s libnvidia-glcore.so.$VERSION nvidia-installer-$VERSION/libGLcore.so.1     &&
ln -s libnvidia-tls.so.$VERSION    nvidia-installer-$VERSION/libnvidia-tls.so.1 &&

echo libXvMCNVIDIA_dynamic.so.1 > XvMCConfig &&

# build installer
cd nvidia-installer-$VERSION &&

 make rebuild_tls_test &&
 make rebuild_tls_test_dso &&
 make rebuild_rtld_test.unstripped &&
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

prepare_install &&

make modules_install KERNEL_UNAME=$KVER &&
install -dm 0755 /usr/lib/modprobe.d &&
echo "blacklist nouveau" > /usr/lib/modprobe.d/nvidia.conf &&
touch /usr/lib/modprobe.d/nvidia.conf &&
cd .. &&

mkdir -p /etc/OpenCL/vendors &&
install -m0444 nvidia.icd /etc/OpenCL/vendors &&
install -m0755 nvidia-bug-report.sh /usr/bin &&
install -m0755 nvidia-installer /usr/bin &&
install -m0755 nvidia-smi /usr/bin &&
ln -sf  /usr/bin/nvidia-installer /usr/bin/nvidia-uninstall &&
install -m0755 nvidia-xconfig /usr/bin &&

install -m0755 libnv*.so.$VERSION /usr/lib &&
ln -sf /usr/lib/libnvidia-cfg.so.$VERSION /usr/lib/libnvidia-cfg.so.1 &&
ln -sf /usr/lib/libnvidia-cfg.so.1 /usr/lib/libnvidia-cfg.so &&

install -m0755 libcuda.so.$VERSION /usr/lib &&
ln -sf /usr/lib/libcuda.so.$VERSION /usr/lib/libcuda.so.1 &&
ln -sf /usr/lib/libcuda.so.1 /usr/lib/libcuda.so &&

install -m0755 libGL.so.$VERSION /usr/lib &&

install -m0755 libOpenCL.so.1.0.0 /usr/lib &&
ln -sf /usr/lib/libOpenCL.so.1.0.0 /usr/lib/libOpenCL.so.1.0 &&
ln -sf /usr/lib/libOpenCL.so.1.0 /usr/lib/libOpenCL.so.1 &&
ln -sf /usr/lib/libOpenCL.so.1 /usr/lib/libOpenCL.so &&

mkdir -p /usr/lib/tls &&
install -m0755 tls/libnvidia-tls.so.$VERSION /usr/lib/tls &&

install -m0755 libvdpau_nvidia.so.$VERSION /usr/lib/vdpau &&
ln -sf /usr/lib/vdpau/libvdpau_nvidia.so.$VERSION /usr/lib/vdpau/libvdpau_nvidia.so.1 &&
ln -sf /usr/lib/vdpau/libvdpau_nvidia.so.1 /usr/lib/libvdpau_nvidia.so &&

mkdir -p /usr/lib/xorg/modules/drivers &&
install -m0755 nvidia_drv.so /usr/lib/xorg/modules/drivers &&
mkdir -p /usr/lib/xorg/modules/extensions &&
install -m0755 libglx.so.$VERSION /usr/lib/xorg/modules/extensions &&

mkdir -p /usr/share/{applications,doc/NVIDIA_GLX-1.0/html} &&
install -m0444 html/* /usr/share/doc/NVIDIA_GLX-1.0/html &&

install -m0444 README.txt LICENSE NVIDIA_Changelog /usr/share/doc/NVIDIA_GLX-1.0 &&
install -m0444 nvidia-xconfig.1.gz nvidia-smi.1.gz nvidia-installer.1.gz /usr/share/man/man1 &&

# Register Nvidia XvMC library for use in any XvMC enabled media player
install -m644 XvMCConfig /etc/X11 &&

install -Dm644 $SCRIPT_DIRECTORY/50-nvidia.conf /usr/share/X11/xorg.conf.d/50-nvidia.conf &&

if in_depends $MODULE "gtk+-3" ; then
  install -m0755 nvidia-settings /usr/bin &&
  install -m0444 nvidia-settings-$VERSION/doc/nvidia-settings.desktop /usr/share/applications &&
  install -m0444 nvidia-settings-$VERSION/doc/nvidia-settings.png /usr/share/doc/NVIDIA_GLX-1.0 &&
  install -m0444 nvidia-settings.1.gz /usr/share/man/man1
fi
