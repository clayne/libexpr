DEPS= https://github.com/xant/libhl \
      https://github.com/xant/libut.git

.PHONY: all clean

all:
	@mkdir -p .libs; \
	mkdir -p .incs; \
	for i in $(DEPS); do \
	    name=`echo $$i | sed 's,.*/,,;s/.git$$//' `; \
	    if [ ! -f $$name/Makefile ]; then \
		cd ..;\
		git submodule init deps/$$name;\
		git submodule update;\
		cd -;\
	    fi;\
	    export LIBDIR="$(shell pwd)/.libs"; \
	    export INCDIR="$(shell pwd)/.incs"; \
	    export CFLAGS="$(CFLAGS) -DHAVE_UINT64_T"; \
	    make -eC $$name; \
	    if [ $$? -ne 0 ] ; then exit $$?; fi; \
	    make -eC $$name install; \
	done

clean:
	@for i in $(DEPS); do \
	    name=`echo $$i | sed 's,.*/,,;s/.git$$//' `; \
	    if [ -d "$$name" ]; then \
		make -C $$name clean; \
	    fi; \
	done;
	@rm -rf "$(shell pwd)/.libs";
	@rm -rf "$(shell pwd)/.incs";

