LIB			= 	-L $(ROOT)/vendor/lib
INCLUDE		=	-I $(ROOT)/vendor/textmate/build/include \
				-I $(ROOT)/vendor/textmate/Shared/include
CFLAGS		=	-g -std=c++1y -stdlib=libc++ -pipe -fPIC -gdwarf-2 -m64 -mmacosx-version-min=10.7 -funsigned-char -D'NULL_STR="\uFFFF"' -DREST_API='"$rest_api"' -Wall -Wwrite-strings -Wformat -Winit-self -Wmissing-include-dirs -Wno-parentheses -Wno-sign-compare -Wno-switch -IShared/include -fcolor-diagnostics -DNDEBUG -Os -include $(ROOT)/vendor/textmate/Shared/PCH/prelude.cc

.PHONY: all clean
all: main

main: main.cc
	g++ $(CFLAGS) $(LIB) $(INCLUDE) -ltm -o $@  main.cc

clean:
	@-rm *.o
	@-rm main
