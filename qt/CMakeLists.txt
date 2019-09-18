cmake_minimum_required(VERSION 3.5)
project(drone_detect)

#qt
find_package(Qt5 COMPONENTS Widgets REQUIRED)

#qt调用moc uic rcc
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTRCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

#opencv
find_package(OpenCV)

#区分debug和release

#项目目录分层

#添加库目录
link_directories(${CMAKE_SOURCE_DIR}/lib)
#添加依赖库
if(WIN32)
#windows系统
link_libraries("kejian_dll.lib" "ConsoleApplication1.lib")
endif(WIN32)

#遍历头文件 源文件 UI文件 资源文件
file(GLOB HEAD_FILES "*.h")
file(GLOB SOURCE_FILES "*.cpp")
file(GLOB FORM_FILES "*.ui")
file(GLOB RESOURCE_FILES "*.qrc")

#添加附加包含目录
include_directories(${CMAKE_SOURCE_DIR}/include 
					${CMAKE_SOURCE_DIR}/include/hongwai
					${CMAKE_SOURCE_DIR}/include/kejian)

#生成可执行文件
add_executable(drone_detect ${HEAD_FILES} ${SOURCE_FILES} ${FORM_FILES} ${RESOURCE_FILES})

#依赖库
target_link_libraries(drone_detect Qt5::Widgets ${OpenCV_LIBS})

#安装目录
install(TARGETS drone_detect 
		RUNTIME DESTINATION ${CMAKE_SOURCE_DIR}/bin
		LIBRARY DESTINATION ${CMAKE_SOURCE_DIR}/lib
		ARCHIVE DESTINATION ${CMAKE_SOURCE_DIR}/lib)