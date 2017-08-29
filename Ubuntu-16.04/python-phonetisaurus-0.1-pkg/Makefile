# Template for python servlet project using FPM
#  * https://github.com/jordansissel/fpm
SETUP=setup.py
.phony: default
default: deb
package: deb

.PHONY: deb

# For this super hack we just copy the contents of the
# ../phonetisaurus-0.1-pkg/Phonetisaurus package, which must
# be compiled first.
deb: $(PKGDIR)
	cp -rf ../phonetisaurus-0.1-pkg/Phonetisaurus/* .
	fpm -m '"Josef Novak" <phonetisaurus@gmail.com>' \
	  --license="BSD3" \
	  --vendor="None" \
	  --url="https://github.com/AdolfVonKleist/Phonetisaurus" \
	  --description="Spitch AG phonetisaurus python bindings." \
	  -f --log=error \
	  -s python \
	  -t deb \
	  -d "phonetisaurus" \
	  $(SETUP)
