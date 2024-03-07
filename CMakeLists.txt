cmake_minimum_required(VERSION 3.10)
project(ImGui)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

file(GLOB_RECURSE IMGUI_SRC
     "${PROJECT_SOURCE_DIR}/imconfig.h"
     "${PROJECT_SOURCE_DIR}/imgui.h"
     "${PROJECT_SOURCE_DIR}/imgui.cpp"
     "${PROJECT_SOURCE_DIR}/imgui_draw.cpp"
     "${PROJECT_SOURCE_DIR}/imgui_internal.h"
     "${PROJECT_SOURCE_DIR}/imgui_tables.cpp"
     "${PROJECT_SOURCE_DIR}/imgui_widgets.cpp"
     "${PROJECT_SOURCE_DIR}/imstb_rectpack.h"
     "${PROJECT_SOURCE_DIR}/imstb_textedit.h"
     "${PROJECT_SOURCE_DIR}/imstb_truetype.h"
     "${PROJECT_SOURCE_DIR}/imgui_demo.cpp")

add_library(ImGui STATIC ${IMGUI_SRC})

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    target_compile_definitions(ImGui PRIVATE HZ_DEBUG)
    set_target_properties(ImGui PROPERTIES DEBUG_POSTFIX d)
elseif(CMAKE_BUILD_TYPE STREQUAL "Release")
    target_compile_definitions(ImGui PRIVATE HZ_RELEASE)
elseif(CMAKE_BUILD_TYPE STREQUAL "Dist")
    target_compile_definitions(ImGui PRIVATE HZ_DIST)
endif()