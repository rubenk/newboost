AC_INIT([newboost], [1.0.0])
AC_LANG([C++])

AC_ARG_VAR([BOOST_CPPFLAGS], [Preprocessor flags for Boost])
AC_ARG_VAR([BOOST_LDFLAGS], [Linker flags for Boost])

SAVE_CPPFLAGS="$CPPFLAGS"
SAVE_LDFLAGS="$LDFLAGS"
CPPFLAGS="$BOOST_CPPFLAGS $CPPFLAGS"
LDFLAGS="$BOOST_LDFLAGS $LDFLAGS"

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
SAVE_LIBS="$LIBS"
LIBS="-lboost_program_options"
AC_LINK_IFELSE(
  [AC_LANG_PROGRAM(
   [[#include <boost/program_options.hpp>]],
   [[
     boost::program_options::variables_map vm;
     boost::program_options::notify(vm);
   ]]
  )],
  [
    AC_MSG_RESULT([yes])
    BOOST_LIBS="$LIBS"
  ],
  [AC_MSG_ERROR([Unable to find Boost.Program_options library])]
)
LIBS="$SAVE_LIBS"


AC_CHECK_HEADERS([boost/test/unit_test.hpp], [], [
  AC_MSG_ERROR([Unable to find Boost.Test headers])
])



AC_MSG_CHECKING([for Boost.Test])
SAVE_LIBS="$LIBS"
LIBS="-lboost_unit_test_framework"
AC_LINK_IFELSE(
  [AC_LANG_SOURCE(
   [[
     #define BOOST_TEST_MODULE autoconf
     #define BOOST_TEST_DYN_LINK
     #define BOOST_TEST_NO_MAIN
     #include <boost/test/unit_test.hpp>

     BOOST_AUTO_TEST_CASE(autoconf)
     {
       BOOST_CHECK(true);
     }

     int main(int argc, char *argv[])
     {
       return boost::unit_test::unit_test_main( &init_unit_test, argc, argv );
     }
   ]]
  )],
  [
    AC_MSG_RESULT([yes])
    BOOST_LIBS="$BOOST_LIBS $LIBS"
  ],
  [AC_MSG_ERROR([Unable to find Boost.Test library])]
)

CPPFLAGS="$SAVE_CPPFLAGS"
LIBS="$SAVE_LIBS"
LDFLAGS="$SAVE_LDFLAGS"


AC_MSG_NOTICE([BOOST_CPPFLAGS: $BOOST_CPPFLAGS])
AC_MSG_NOTICE([BOOST_LDFLAGS: $BOOST_LDFLAGS])
AC_MSG_NOTICE([BOOST_LIBS: $BOOST_LIBS])
AC_MSG_NOTICE([CPPFLAGS: $CPPFLAGS])
AC_MSG_NOTICE([CXXFLAGS: $CXXFLAGS])
AC_MSG_NOTICE([LDFLAGS: $LDFLAGS])
AC_MSG_NOTICE([LIBS: $LIBS])
