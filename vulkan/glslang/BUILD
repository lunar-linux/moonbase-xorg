export CXXFLAGS+=" -ffat-lto-objects"
OPTS+=" -DBUILD_SHARED_LIBS=ON"

default_cmake_build &&

pushd /usr/lib &&
  for lib in libglslang*.so; do
      ln -sf "${lib}" "${lib}.0"
  done
popd
