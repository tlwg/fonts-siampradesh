FONTSOURCES = \
	THK2DJuly8-BoldItalic.sfd	\
	THK2DJuly8-Bold.sfd		\
	THK2DJuly8-Italic.sfd		\
	THK2DJuly8.sfd

TTFFILES = $(shell echo $(FONTSOURCES) | sed 's/.sfd/.ttf/g')
AFMFILES = $(shell echo $(FONTSOURCES) | sed 's/.sfd/.afm/g')
PFAFILES = $(shell echo $(FONTSOURCES) | sed 's/.sfd/.pfa/g')
PFBFILES = $(shell echo $(FONTSOURCES) | sed 's/.sfd/.pfb/g')

TYPE1FILES =
if INCLUDE_PFA
TYPE1FILES += $(PFAFILES) $(AFMFILES)
endif
if INCLUDE_PFB
TYPE1FILES += $(PFBFILES) $(AFMFILES)
endif

CLEANFILES = *.ttf *.g2n *.pfb *.pfa *.afm *.pfm *.otf *.enc *.tfm

EXTRA_DIST = $(FONTSOURCES)

if INCLUDE_TTF
ttf_DATA = $(TTFFILES)
endif

if INCLUDE_TYPE1
type1_DATA = $(TYPE1FILES)
endif

include $(top_builddir)/scripts/gen.mk
