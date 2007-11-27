#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.61)
AC_INIT(thaifonts-dip-sipa, 0.1.0)
AM_INIT_AUTOMAKE

# Check options
AC_ARG_ENABLE(ttf,
              [AC_HELP_STRING([--disable-ttf],
                              [disable TTF generation])],
              , enable_ttf="yes")
if test "x$enable_ttf" = "xyes"; then
  AC_ARG_WITH(ttfdir,
    [AC_HELP_STRING([--with-ttfdir=DIR],
                    [font directory in DIR [PREFIX/share/fonts/th/TTF]])],
    [ttfdir="$withval"], [ttfdir=\$\{prefix\}/share/fonts/th/TTF])
  AC_MSG_CHECKING(--with-ttfdir)
  AC_MSG_RESULT("$ttfdir")

  AC_SUBST(ttfdir)
fi

AC_ARG_ENABLE(pfa,
              [AC_HELP_STRING([--enable-pfa],
                              [enable Type1 PFA generation])],
              , enable_pfa="no")
AC_ARG_ENABLE(pfb,
              [AC_HELP_STRING([--enable-pfb],
                              [enable Type1 PFB generation])],
              , enable_pfb="no")
if test "x$enable_pfa" = "xyes" -o "x$enable_pfb" = "xyes"; then
  AC_ARG_WITH(type1dir,
    [AC_HELP_STRING([--with-type1dir=DIR],
                    [font directory in DIR [PREFIX/share/fonts/th/Type1]])],
    [type1dir="$withval"], [type1dir=\$\{prefix\}/share/fonts/th/Type1])
  AC_MSG_CHECKING(--with-type1dir)
  AC_MSG_RESULT("$type1dir")

  AC_SUBST(type1dir)
fi

AM_CONDITIONAL(INCLUDE_TTF,test $enable_ttf = "yes")
AM_CONDITIONAL(INCLUDE_PFA,test $enable_pfa = "yes")
AM_CONDITIONAL(INCLUDE_PFB,test $enable_pfb = "yes")
AM_CONDITIONAL(INCLUDE_TYPE1,test $enable_pfa = "yes" -o $enable_pfb = "yes")

# Checks for programs.
AC_PROG_INSTALL
AC_PROG_LN_S
AC_CHECK_PROGS(RMDIR,rmdir,no)

AC_CHECK_PROGS(FONTFORGE,fontforge pfaedit,no)

if test "x$FONTFORGE" = "xno"; then
  AC_MSG_ERROR([You need fontforge to generate fonts.])
fi

dnl prefer mkfontscale over ttmkfdir
AC_CHECK_PROG(MKFONTSCALE,mkfontscale,mkfontscale)

# xorg or xfree86?
if test "x$MKFONTSCALE" = "xmkfontscale"; then
  if $MKFONTSCALE -n >/dev/null 2>&1; then
    # xorg's mkfontscale
    MKFONTSCALE="mkfontscale -a tis620-0 -a tis620-2"
    rm -f fonts.scale encodings.dir
  else
    # xfree86's mkfontscale
    MKFONTSCALE="mkfontscale -e tis620-0 -e tis620-2"
  fi
fi

if test "x$enable_ttf" = "xyes"; then
  if test "x$MKFONTSCALE" = "x"; then
    AC_CHECK_PROG(TTMKFDIR,ttmkfdir,ttmkfdir)
    if test "x$TTMKFDIR" = "x"; then
      AC_MSG_ERROR([You need mkfontscale or ttmkfdir])
    else
      if (ttmkfdir -h 2>&1 | grep -- --encoding >/dev/null); then
        # ttmkfdir 2
        TTMKFDIR="ttmkfdir -e /usr/X11R6/lib/X11/fonts/encodings/encodings.dir -o fonts.scale"
      else
        # ttmkfdir 1
        TTMKFDIR="ttmkfdir > fonts.scale"
      fi
    fi
  else
    TTMKFDIR="$MKFONTSCALE"
  fi
  AC_MSG_RESULT([Will create fonts.scale for TTF using $TTMKFDIR])
fi

if test "x$enable_pfa" = "xyes" -o "x$enable_pfb" = "xyes"; then
  if test "x$MKFONTSCALE" = "x"; then
    AC_CHECK_PROG(TYPE1INST,type1inst,type1inst)
    if test "x$TYPE1INST" = "x"; then
      AC_MSG_ERROR([You need mkfontscale or type1inst])
    fi
  else
    TYPE1INST="$MKFONTSCALE"
  fi
  AC_MSG_RESULT([Will create fonts.scale for Type1 using $TYPE1INST])
fi
AC_CHECK_PROG(FCCACHE,fc-cache,[fc-cache])


AC_CONFIG_FILES([Makefile
                 02-TH-Krub/Makefile
                 04-TH-Niramit-AS/Makefile
                 06-TH-Kodchasal/Makefile
                 07-TH-Sarabun-PSK/Makefile
                 08-TH-K2D-July8/Makefile
                 09-TH-Mali-Grade-6/Makefile
                 10-TH-Chakra-Petch/Makefile
                 11-TH-Baijam/Makefile
                 12-TH-KoHo/Makefile
                 13-TH-Fah-Kwang/Makefile
                 scripts/Makefile
                 scripts/gen.mk])

AC_OUTPUT