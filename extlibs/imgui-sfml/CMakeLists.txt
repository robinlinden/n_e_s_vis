include(FetchContent)

FetchContent_Declare(
  imgui-sfml
  GIT_REPOSITORY https://github.com/eliasdaler/imgui-sfml.git
  GIT_TAG        f5aec785a9f6e942d94551313fa359d6d0d094a9
)

FetchContent_GetProperties(imgui-sfml)
if(NOT imgui-sfml_POPULATED)
    FetchContent_Populate(imgui-sfml)
endif()

find_package(OpenGL COMPONENTS OpenGL REQUIRED)

add_library(imgui-sfml
            ${ImGui_SOURCES}
            ${ImGui_HEADERS}
            ${imgui-sfml_SOURCE_DIR}/imgui-SFML.h
            ${imgui-sfml_SOURCE_DIR}/imconfig-SFML.h
            ${imgui-sfml_SOURCE_DIR}/imgui-SFML.cpp)
target_include_directories(imgui-sfml SYSTEM PUBLIC ${ImGui_ROOT} ${imgui-sfml_SOURCE_DIR})
target_link_libraries(imgui-sfml PUBLIC OpenGL::GL sfml-graphics sfml-window sfml-system)
target_compile_definitions(imgui-sfml PUBLIC -DIMGUI_USER_CONFIG="imconfig-SFML.h")
