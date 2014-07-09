FONTSOURCES = \
	SPRamasun-BoldOblique.sfd	\
	SPRamasun-Bold.sfd		\
	SPRamasun-Oblique.sfd		\
	SPRamasun.sfd

TTFFILES = $(FONTSOURCES:.sfd=.ttf)
AFMFILES = $(FONTSOURCES:.sfd=.afm)
PFAFILES = $(FONTSOURCES:.sfd=.pfa)
PFBFILES = $(FONTSOURCES:.sfd=.pfb)

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
