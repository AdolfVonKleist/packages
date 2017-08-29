NAME=phonetisaurus
VERSION=0.1
RELEASE=$(shell lsb_release -cs)
GITREPO="https://github.com/AdolfVonKleist/Phonetisaurus.git"
PKGDIR=/tmp/install_$(NAME)-$(VERSION)_pkg
TARDIR=Phonetisaurus

.phony: default
default: deb
package: deb

.PHONY: clean

clean:
	rm -rf $(NAME)*
	rm -rf $(PKGDIR)*

$(TARDIR):
	git clone $(GITREPO) \
	&& cd Phonetisaurus && git checkout -b giuliopaci-build-refactoring master \
	&& git pull https://github.com/giuliopaci/Phonetisaurus.git build-refactoring \
	&& git checkout master && git merge --no-ff giuliopaci-build-refactoring \
	&& mkdir -p $(PKGDIR) \
	&& cd src; ./configure; make -j 2; make install DESTDIR=$(PKGDIR)

.PHONY: deb compile
compile: $(TARDIR)
deb: $(TARDIR) $(PKGDIR)
	fpm -m '"Josef Novak" <phonetisaurus@gmail.com>' \
	    --license="BSD3" \
	    --vendor="None" \
	    --url="https://github.com/AdolfVonKleist/Phonetisaurus" \
	    --description="Unofficial Phonetisaurus package compiled with all options." \
	    -f --log=error \
	    --after-install=post.sh \
	    --after-remove=post.sh \
	    -s dir \
	    -t deb \
	    -n $(NAME) \
	    -v $(VERSION) \
	    -C $(PKGDIR) \
	    -p $(NAME)_VERSION_ARCH-$(RELEASE).deb \
	    -d "zlib1g-dev >= 1.2" \
	    usr/local/bin usr/local/lib usr/local/include
