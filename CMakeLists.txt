cmake_minimum_required(VERSION 3.8)

project(libimguizmo VERSION 1.0.0 
                    DESCRIPTION "set of single file C/C++ libraries"
                    LANGUAGES C CXX)

# selects new opengl
if (POLICY CMP0072)
  cmake_policy (SET CMP0072 NEW)
endif(POLICY CMP0072)

set(CMAKE_CXX_STANDARD          17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS        OFF)

find_package(Git REQUIRED)
if (NOT EXISTS ${LIBTFD_DIR}/CMakeLists.txt)
    execute_process(COMMAND ${GIT_EXECUTABLE}
        submodule update --recursive
        WORKING_DIRECTORY ${PROJECT_SOURCE_DIR})
endif()

add_subdirectory("dependencies/imgui")

set(INCLUDE_DIRS
    "."
)

set(SRC_FILES 
    "GraphEditor.cpp"
    "ImCurveEdit.cpp"
    "ImGradient.cpp"
    "ImGuizmo.cpp"
    "ImSequencer.cpp"
)

add_library(imguizmo STATIC ${SRC_FILES})
target_include_directories(imguizmo PUBLIC ${INCLUDE_DIRS})
target_link_libraries(imguizmo PUBLIC imgui)
target_link_libraries(imguizmo PUBLIC ${CMAKE_DL_LIBS})
