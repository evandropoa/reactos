
add_definitions(-D_WINE)
spec2def(msvfw32.dll msvfw32.spec ADD_IMPORTLIB)

list(APPEND SOURCE
    mciwnd.c
    msvideo_main.c
    drawdib.c
    precomp.h
    ${CMAKE_CURRENT_BINARY_DIR}/msvfw32_stubs.c)

add_library(msvfw32 MODULE
    ${SOURCE}
    rsrc.rc
    ${CMAKE_CURRENT_BINARY_DIR}/msvfw32.def)

set_module_type(msvfw32 win32dll)
target_link_libraries(msvfw32 wine)
add_importlibs(msvfw32 winmm comctl32 user32 gdi32 advapi32 msvcrt kernel32 ntdll)
add_pch(msvfw32 precomp.h SOURCE)
add_cd_file(TARGET msvfw32 DESTINATION reactos/system32 FOR all)
set_wine_module_FIXME(msvfw32) # CORE-5743: No ARRAY_SIZE macro
