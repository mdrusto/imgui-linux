project(imgui LANGUAGES C CXX)


set(IMGUI_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_library(imgui STATIC)

target_sources(
		imgui
		PRIVATE
			${IMGUI_DIR}/glad/glad.c
			${IMGUI_DIR}/imgui_demo.cpp
			${IMGUI_DIR}/imgui_draw.cpp
			${IMGUI_DIR}/imgui_tables.cpp
			${IMGUI_DIR}/imgui_widgets.cpp
			${IMGUI_DIR}/imgui.cpp
		
		PRIVATE
			${IMGUI_DIR}/backends/imgui_impl_opengl2.cpp
			${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
		)

target_include_directories(
		imgui
		PUBLIC
			${IMGUI_DIR}
			${IMGUI_DIR}/backends
			${OPENGL_INCLUDE_DIRS}
			${GLFW_INCLUDE_DIRS}
		)

set(OpenGL_GL_PREFERENCE GLVND)

set(GLFW_DEPS pthread)

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(GLEW REQUIRED)

target_link_libraries(imgui PUBLIC OpenGL::GL glfw)
