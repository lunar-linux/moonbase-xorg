. /etc/profile.d/x11r7.rc &&

sedit 's/\/opt\/local/\${X11R7_PREFIX}/g' Makefile &&
sedit 's/\/usr\/local/\/usr\/share/g' Makefile &&

sedit 's/int lcexceptionscmp(const char \*\*a, const char \*\*b) { return stricmp(\*a, \*b); }/int lcexceptionscmp(const void *a, const void *b) { return stricmp(*(const char **)a, *(const char **)b); }/' rman.c &&

prepare_install &&
make install
