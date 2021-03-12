set(WEBVIEW_HEADERS_PATH C:/Users/Tobi/Downloads/microsoft.web.webview2.1.0.705.50/build/native/include)
#set(WEBVIEW_LIBRARIES_PATH C:/Users/Tobi/Downloads/microsoft.web.webview2.1.0.705.50/build/native/x64)
set(WEBVIEW_LIBRARIES_PATH ${CMAKE_CURRENT_SOURCE_DIR}/dll/x64)

cmake_minimum_required(VERSION 3.17)
project(webview)

set(CMAKE_CXX_STANDARD 17)
set(TARGET_NAME webview_test)

add_library(webview SHARED IMPORTED)
set_target_properties(webview PROPERTIES
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/dll/x64/webview.dll
        IMPORTED_IMPLIB ${CMAKE_CURRENT_SOURCE_DIR}/dll/x64/webview.lib
        LINKER_LANGUAGE C)

add_library(WebView2Loader SHARED IMPORTED)
set_target_properties(WebView2Loader PROPERTIES
        IMPORTED_LOCATION ${WEBVIEW_LIBRARIES_PATH}/WebView2Loader.dll
        IMPORTED_IMPLIB ${WEBVIEW_LIBRARIES_PATH}/WebView2Loader.lib
        LINKER_LANGUAGE C)


add_executable(${TARGET_NAME} WIN32 main.cc)
target_link_libraries(${TARGET_NAME} PRIVATE webview WebView2Loader)
#target_include_directories(${TARGET_NAME} PRIVATE ${WEBVIEW_HEADERS_PATH})
target_include_directories(${TARGET_NAME} PRIVATE ${WEBVIEW_HEADERS_PATH})