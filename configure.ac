AC_INIT(local-project, esyscmd(grep :version lpro.asd | cut -d\" -f2 | tr -d \\n),
        stuart.dils@gmail.com)
AC_SUBST(DATA_DIR)
AC_SUBST(PKG_MANAGER)
AC_SUBST(PKG_DB)
AC_SUBST(PROJECT_ROOT_DIR)

PROJECT_ROOT_DIR="`pwd`"

dnl AC_ARG_WITH(data-dir,
dnl 	[  --data-dir-path=PATH   specify the location of the gdep database directory],
dnl 	DATA_DIR=$withval, DATA_DIR="$prefix/share/")

AC_PATH_PROGS(ROSWELL, ros)

# Is there a better way to check which management tools are being used?
# get the package manager used:
AC_CHECK_PROGS(PKG_MANAGER, zypper yum pkg apt-get)


# get the package database
if [[ PKG_MANAGER = ":pkg" ]]; then
   PKG_DB=":pkg"
else
   AC_CHECK_PROGS(PKG_DB, rpm dpkg)
fi

if test "$PKG_MANAGER" = "no"; then
   AC_MSG_WARN([Package manager not found. You will not be able to install packages with gdep])
fi
if test "$PKG_DB" = "no"; then
   AC_MSG_WARN([Package databse tool not found. You will not be able to check if a project's package dependencies have been updated.])
fi


AC_OUTPUT
AC_CONFIG_FILES(src/settings.lisp)
AC_CONFIG_FILES(Makefile)
AC_CONFIG_FILES(lpro.ros)
DATA_DIR="$prefix/share/lpro"

AC_OUTPUT

AS_ECHO(["
gdep settings:
  Roswell exectuable: ${ROSWELL}
  Data directory:     ${DATA_DIR}
  Package manager:    ${PKG_MANAGER}
  Package database:   ${PKG_DB}
"])
