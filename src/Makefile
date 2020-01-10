MANDIR=/usr/share/man/cs
SECTIONS=1 2 3 4 5 6 7 8

all:

install: $(SECTIONS:%=install-section-%)

install-section-%:
	install -m 755 -d $(DESTDIR)$(MANDIR)/man$*
	find . -name '*.$*' -not -path '*.pc*' -print0 | xargs -r -0 install -m 644 -t $(DESTDIR)$(MANDIR)/man$*

check:
	# Check man pages syntax
	# We ignore includes (.so), because directory structure does not allow checking this
	find . -name '*.[1-8]' -not -path '*.pc*' | \
		while read page ; do \
			if grep -q '\.so' $$page; then continue ; fi ; \
			perl check-hyphens.pl $$page ; \
		done

.PHONY: all install check
