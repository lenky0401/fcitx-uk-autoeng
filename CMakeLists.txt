project(fcitx-autoeng-ng)
cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
find_package(Fcitx 4.2.8 REQUIRED)

_fcitx_add_uninstall_target()

set(CMAKE_C_FLAGS "-g -O0 -Wall -Wextra -Wno-sign-compare -Wno-unused-parameter -fvisibility=hidden ${CMAKE_C_FLAGS}")
set(CMAKE_CXX_FLAGS "-g -O0 -Wall -Wextra -Wno-sign-compare -Wno-unused-parameter -fvisibility=hidden ${CMAKE_CXX_FLAGS}")
set(CMAKE_SHARED_LINKER_FLAGS "-Wl,--as-needed ${CMAKE_SHARED_LINKER_FLAGS}")
set(CMAKE_MODULE_LINKER_FLAGS "-Wl,--as-needed ${CMAKE_MODULE_LINKER_FLAGS}")
add_definitions("-D_GNU_SOURCE -DFCITX_HAVE_CONFIG_H")

set(package     fcitx)
set(prefix      ${CMAKE_INSTALL_PREFIX})
set(exec_prefix ${CMAKE_INSTALL_PREFIX})
set(bindir ${exec_prefix}/bin)

if(NOT DEFINED LIB_INSTALL_DIR)
    set(LIB_INSTALL_DIR "${exec_prefix}/lib" CACHE PATH "Library install directory [default=PREFIX/lib/]")
endif()
if(NOT DEFINED LIBDATA_INSTALL_DIR)
    set(LIBDATA_INSTALL_DIR "${LIB_INSTALL_DIR}"  CACHE PATH "Lib data install directory [default=LIB_INSTALL_DIR]")
endif()
if(NOT DEFINED MAN_INSTALL_DIR)
    set(MAN_INSTALL_DIR "${prefix}/share/man"  CACHE PATH "man install directory [default=PREFIX/share/man]")
endif()
if (NOT DEFINED DBUS_SERVICE_DIR)
    set(DBUS_SERVICE_DIR "${CMAKE_INSTALL_PREFIX}/share/dbus-1/services" CACHE PATH "dbus session service directory [default=PREFIX/share/dbus-1/services]")
endif()
if (NOT DEFINED SYSCONFDIR)
    set(SYSCONFDIR "${CMAKE_INSTALL_PREFIX}/etc" CACHE PATH "sys config directory [default=PREFIX/etc/]")
endif()

set(includedir "${CMAKE_INSTALL_PREFIX}/include")
set(libdir ${LIB_INSTALL_DIR})
set(pkgconfdir ${LIBDATA_INSTALL_DIR}/pkgconfig)
set(mandir ${MAN_INSTALL_DIR})
set(addondir ${libdir}/${package} )
set(pkgdatadir ${prefix}/share/${package})
set(configdescdir ${pkgdatadir}/configdesc)
set(addonconfigdir ${pkgdatadir}/addon)
set(imconfigdir ${pkgdatadir}/inputmethod)
set(localedir ${CMAKE_INSTALL_PREFIX}/share/locale)

add_subdirectory(src)
add_subdirectory(data)
