AC_INIT([newboost], [1.0.0])
AC_LANG([C++])

AC_CHECK_HEADERS([boost/version.hpp], [], [
  AC_MSG_ERROR([Unable to find Boost headers])
])

AC_MSG_CHECKING([for Boost version >= 1.35])
AC_PREPROC_IFELSE(
  [AC_LANG_PROGRAM(
    [[#include <boost/version.hpp>]],
    [[
      #if BOOST_VERSION < 103500
      #error invalid version
      #endif
    ]]
  )],
  [AC_MSG_RESULT([yes])],
  [AC_MSG_ERROR([Boost is too old])],
)

AC_CHECK_HEADERS([boost/program_options.hpp], [], [
  AC_MSG_ERROR([Unable to find Boost.Program_options headers])
])

AC_MSG_CHECKING([for Boost.Program_options])
SAVE_LDFLAGS="$LDFLAGS"
LDFLAGS="-lboost_program_options $LDFLAGS"
AC_LINK_IFELSE(
  [AC_LANG_PROGRAM(
   [[#include <boost/program_options.hpp>]],
   [[
     boost::program_options::variables_map vm;
     boost::program_options::notify(vm);
   ]]
  )],
  [AC_MSG_RESULT([yes])],
  [AC_MSG_ERROR([Unable to find Boost.Program_options library])]
)
LDFLAGS="$SAVE_LDFLAGS"


