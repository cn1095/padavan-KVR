SRC_NAME = rtty-8.2.0
SRC_URL = https://github.com/zhaojh329/rtty/releases/download/v8.2.0/rtty-8.2.0.tar.gz
CFLAGS   += -O2 -ffunction-sections -fdata-sections
LDFLAGS  += -Wl,--gc-sections

THISDIR = $(shell pwd)

all: download_test extract_test config_test
	$(MAKE) -j$(HOST_NCPU) -C $(SRC_NAME)/build 

download_test:
	( if [ ! -f $(SRC_NAME).tar.gz ]; then \
		wget -t5 --timeout=20 --no-check-certificate -O $(SRC_NAME).tar.gz $(SRC_URL); \
	fi )

extract_test:
	( if [ ! -d $(SRC_NAME) ]; then \
		tar -xf $(SRC_NAME).tar.gz; \
	fi )

config_test:
	( if [ -f ./config_done ]; then \
		echo "the same configuration"; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( mkdir -p $(SRC_NAME)/build && cd $(SRC_NAME)/build ; \
	cmake -DCMAKE_TOOLCHAIN_FILE=../../cross-mipsel-linux.cmake \
		  -DCMAKE_BUILD_TYPE=Release \
		  -DUSE_OPENSSL=ON \
		  -DOPENSSL_FOUND=TRUE .. \
	)

clean:
	if [ -f $(SRC_NAME)/Makefile ] ; then \
		$(MAKE) -C $(SRC_NAME) clean ; \
	fi ; \
	rm -f config_done
	rm -rf install

romfs:
	$(ROMFSINST) $(THISDIR)/$(SRC_NAME)/build/src/rtty /usr/bin/rtty
