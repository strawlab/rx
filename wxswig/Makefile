all: wxswig

PKGVERSION = SWIG-1.3.29
TARBALL = build/$(PKGVERSION)-wx.tar.gz
TARBALL_URL = http://pr.willowgarage.com/downloads/$(PKGVERSION)-wx.tar.gz
SOURCE_DIR = build/SWIG-1.3.29
UNPACK_CMD = tar xzf
MD5SUM_FILE = md5.checksum
include $(shell rospack find mk)/download_unpack_build.mk

UNAME := $(shell uname)

WXSWIG_CONFIGURE_PARAMS = --prefix=$(shell rospack find wxswig)
ifeq ($(UNAME), Darwin)
WXSWIG_CONFIGURE_PARAMS += --disable-dependency-tracking
endif

$(VERSION)/Makefile: $(VERSION)/Makefile.in $(VERSION)/configure $(VERSION)/configure.in
	cd $(VERSION) && \
		./configure --prefix=$(WXSWIG_ROOT)

wxswig: $(SOURCE_DIR)/unpacked
ifneq ($(MAKE),)
	cd $(SOURCE_DIR) && ./configure $(WXSWIG_CONFIGURE_PARAMS) && $(MAKE) $(ROS_PARALLEL_JOBS) && $(MAKE) install
else
	cd $(SOURCE_DIR) && ./configure $(WXSWIG_CONFIGURE_PARAMS) && make $(ROS_PARALLEL_JOBS) && make install
endif
	mv bin/swig bin/swig-real
	cp swig-wrap bin/swig
	touch wxswig

clean:
	rm -rf bin share wxswig $(SOURCE_DIR)

wipe: clean
	rm -rf build
