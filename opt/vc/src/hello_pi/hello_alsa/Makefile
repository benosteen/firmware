OBJS=hello_alsa.o
BIN=hello_alsa.bin

CFLAGS+=-DSTANDALONE -D__STDC_CONSTANT_MACROS -D__STDC_LIMIT_MACROS -DTARGET_POSIX -D_LINUX -fPIC -DPIC -D_REENTRANT -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64 -U_FORTIFY_SOURCE -Wall -g -ftree-vectorize -pipe -DUSE_EXTERNAL_OMX -DUSE_VCHIQ_ARM -Wno-psabi -I$(SDKSTAGE)/opt/vc/include/

LDFLAGS+=-L$(SDKSTAGE)/opt/vc/lib/ -lasound 

INCLUDES+=-I$(SDKSTAGE)/opt/vc/include/ -I./ -I../libs

all: $(BIN) $(LIB)

%.o: %.c
	@rm -f $@ 
	$(CC) $(CFLAGS) $(INCLUDES) -g -c $< -o $@ -Wno-deprecated-declarations

%.bin: $(OBJS)
	$(CC) -o $@ -Wl,--whole-archive $(LDFLAGS) $(OBJS) -Wl,--no-whole-archive -rdynamic

%.a: $(OBJS)
	$(AR) r $@ $^

clean:
	for i in $(OBJS); do (if test -e "$$i"; then ( rm $$i ); fi ); done
	@rm -f $(BIN) $(LIB)

