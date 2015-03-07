TMLIBS := textmate/build/Frameworks/parse/libparse.a \
				textmate/build/Frameworks/text/libtext.a \
				textmate/build/Frameworks/plist/libplist.a \
				textmate/build/Frameworks/scope/libscope.a \
				textmate/build/Frameworks/bundles/libbundles.a \
				textmate/build/Frameworks/regexp/libregexp.a \
				textmate/build/Frameworks/cf/libcf.a 

.PHONY: all
all: lib/libtm.a

textmate/build.ninja:
	@(cd textmate; git submodule update --init;)
	@echo 'EXPORT        = src/*.h' >> textmate/Frameworks/parse/target; 
	@(cd textmate; export builddir=./build; ./configure)

$(TMLIBS): textmate/build.ninja
	@(cd textmate; ninja $(subst textmate/,,$@);)
	@(cd textmate; name=`dirname $@`; name=`basename $$name`; ninja $$name/headers)

lib:
	@mkdir lib

lib/libtm.a: $(TMLIBS) | lib
	@for lib in $(TMLIBS); do \
		cp $$lib lib; \
		(cd lib; ar -x `basename $$lib`); \
		(cd lib; rm `basename $$lib`); \
	done
	@(cd lib; ar -cqs libtm.a *.o)
	@-rm lib/*.o
	

.PHONY: clean
clean:
	@(cd textmate; git checkout .)
	@-rm -rf textmate/build
	@-rm textmate/build.ninja
	@-(cd textmate; rm $(TMLIBS))
	@-rm -rf lib
