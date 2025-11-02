cmake_minimum_required(VERSION 3.15)
project(LightJS_Installer)

# Informazioni di base del pacchetto
set(CPACK_PROJECT_NAME "LightJS")
set(CPACK_PACKAGE_NAME "LightJS")
set(CPACK_PACKAGE_VERSION "1.0.0")
set(CPACK_PACKAGE_VENDOR "LightJS Project")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "LightJS CLI and runtime")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "LightJS")

# File e directory da includere nell’installer
install(FILES
    "${CMAKE_SOURCE_DIR}/light.exe"
    DESTINATION .
)
install(DIRECTORY
    "${CMAKE_SOURCE_DIR}/third_party"
    DESTINATION .
)

# Configurazione CPack/NSIS
set(CPACK_GENERATOR "NSIS")
set(CPACK_NSIS_DISPLAY_NAME "LightJS")
set(CPACK_NSIS_HELP_LINK "https://github.com/alb0084/lightjs-cli")
set(CPACK_NSIS_URL_INFO_ABOUT "https://github.com/alb0084/lightjs-cli")
set(CPACK_NSIS_CONTACT "support@lightjs.local")
set(CPACK_NSIS_MODIFY_PATH ON)

# Collegamento sul desktop
set(CPACK_NSIS_CREATE_ICONS_EXTRA
  "CreateShortCut '$DESKTOP/LightJS.lnk' '$INSTDIR/light.exe'"
)

# Percorso esplicito del makensis locale (solo per il tuo utente)
set(CPACK_NSIS_EXECUTABLE "D:/Programmi/NSIS/makensis.exe")

include(InstallRequiredSystemLibraries)
include(CPack)
