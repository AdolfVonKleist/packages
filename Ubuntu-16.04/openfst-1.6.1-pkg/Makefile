NAME=openfst
VERSION=1.6.1
RELEASE=$(shell lsb_release -cs)
TARDIR=$(NAME)-$(VERSION)
TARBALL=$(NAME)-$(VERSION).tar.gz
DOWNLOAD="http://www.openfst.org/twiki/pub/FST/FstDownload/$(TARBALL)"
PKGDIR=/tmp/install_$(NAME)-$(VERSION)_pkg
DEBPKG=../debs/openfst_VERSION_ARCH-$(RELEASE).deb

.phony: default
default: deb
package: deb

.PHONY: clean clean-deb

clean:
	rm -rf $(NAME)*
	rm -rf $(PKGDIR)*

clean-deb:
	rm -f $(DEBPKG)

$(TARBALL):
	curl -o $(TARBALL) "$(DOWNLOAD)"

$(PKGDIR):
	mkdir -p $(PKGDIR)

$(TARDIR): $(TARBALL) $(PKGDIR)
	if [ -z "`dpkg -l | grep zlib1g-dev`" ]; then sudo apt-get install zlib1g-dev; fi
	tar -xvzf $(TARBALL)
	cd $(TARDIR); ./configure --enable-static=yes --enable-shared=yes \
	    --enable-compact-fsts --enable-compress --enable-const-fsts --enable-far \
	    --enable-linear-fsts --enable-lookahead-fsts --enable-mpdt --enable-ngram-fsts \
	    --enable-pdt --enable-special --enable-bin; make -j 2; make install DESTDIR=$(PKGDIR)

.PHONY: deb compile
compile: $(TARDIR)
deb: $(TARDIR) $(PKGDIR)
	fpm -m '"Josef Novak" <josef.robert.novak@gmail.com>' \
	    --license="Apache 2.0" \
	    --vendor="None" \
	    --url="http://openfst.org" \
	    --description="Unofficial OpenFst v$(VERSION) package compiled with all options except python bindings." \
	    -f --log=error \
	    --after-install=post.sh \
	    --after-remove=post.sh \
	    -s dir \
	    -t deb \
	    -n $(NAME) \
	    -v $(VERSION) \
	    -C $(PKGDIR) \
	    -p $(DEBPKG) \
	    -d "zlib1g-dev >= 1.2" \
	    usr/local/bin usr/local/lib usr/local/include
