. /etc/profile.d/x11r7.rc &&

export CFLAGS="${CFLAGS//-fno-plt} -fcommon"
export CXXFLAGS=${CXXFLAGS//-fno-plt}
export LDFLAGS=${LDFLAGS//-Wl,-z,now}

OPTS+=" --with-default-dri=3"

./autogen.sh &&

default_build
