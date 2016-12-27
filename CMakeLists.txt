#
# project: fips-nfd

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup()
    fips_project(fips-nfd)
endif()

if (FIPS_ANDROID OR FIPS_NACL OR FIPS_EMSCRIPTEN)
	message(ERROR Platform not supported)
endif() # CMAKE_TOOLCHAIN_FILE

#-[ libs ]---------------------------------------------------------------------

fips_begin_lib(nfd)
    fips_include_directories(nfd/src/include nfd/src)
    fips_files(nfd/src/nfd_common.c)

    if (FIPS_WINDOWS)
        fips_files(nfd/src/nfd_win.cpp)
    elseif (FIPS_MACOS)
        fips_files(nfd/src/nfd_cocoa.m)
        #fips_frameworks_osx(CoreFoundation CoreServices) # need test
    elseif (FIPS_LINUX)
        fips_files(nfd/src/nfd_gtk.cpp)
        # `pkg-config --cflags gtk+-3.0` # find libs
    else()
        message(ERROR Platform not supported)
    endif()
fips_end_lib()

#-[ execs ]---------------------------------------------------------------------

fips_ide_group(Tests)
fips_begin_app(nfd-opendialog cmdline)
    fips_files(nfd/test/test_opendialog.c)
    fips_deps(nfd)
fips_end_app()

fips_begin_app(nfd-opendialogmultiple cmdline)
    fips_files(nfd/test/test_opendialogmultiple.c)
    fips_deps(nfd)
fips_end_app()

fips_begin_app(nfd-pickfolder cmdline)
    fips_files(nfd/test/test_pickfolder.c)
    fips_deps(nfd)
fips_end_app()

fips_begin_app(nfd-savedialog cmdline)
    fips_files(nfd/test/test_savedialog.c)
    fips_deps(nfd)
fips_end_app()

#-------------------------------------------------------------------------------
