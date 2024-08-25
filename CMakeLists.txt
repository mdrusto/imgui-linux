#project(imgui LANGUAGES C CXX)


set(IMGUI_DIR ${CMAKE_CURRENT_SOURCE_DIR})
add_library(imgui STATIC)

target_sources(
		imgui
		PRIVATE
			glad/glad.c
			imgui_demo.cpp
			imgui_draw.cpp
			imgui_tables.cpp
			imgui_widgets.cpp
			imgui.cpp
		
		PRIVATE
			backends/imgui_impl_opengl2.cpp
			backends/imgui_impl_glfw.cpp
			imgui_stdlib.cpp
		)

target_include_directories(
		imgui
		PUBLIC
			${IMGUI_DIR}
			backends
			${OPENGL_INCLUDE_DIRS}
			${GLFW_INCLUDE_DIRS}
		)

set(OpenGL_GL_PREFERENCE GLVND)

set(GLFW_DEPS pthread)

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)
find_package(GLEW REQUIRED)

target_link_libraries(imgui PUBLIC OpenGL::GL glfw)
