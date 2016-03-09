include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
)

set(
    Screenbackend_SRCS
    modules/Screen/backend.cpp
    modules/Screen/mytype.cpp
    modules/Screen/screen.cpp
)

add_library(Screenbackend MODULE
    ${Screenbackend_SRCS}
)

set_target_properties(Screenbackend PROPERTIES
         LIBRARY_OUTPUT_DIRECTORY Screen)

qt5_use_modules(Screenbackend Gui Qml Quick)

# Copy qmldir file to build dir for running in QtCreator
add_custom_target(Screenbackend-qmldir ALL
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/modules/Screen/qmldir ${CMAKE_CURRENT_BINARY_DIR}/Screen
    DEPENDS ${QMLFILES}
)

# Install plugin file
install(TARGETS Screenbackend DESTINATION ${QT_IMPORTS_DIR}/Screen/)
install(FILES   modules/Screen/qmldir DESTINATION ${QT_IMPORTS_DIR}/Screen/)

