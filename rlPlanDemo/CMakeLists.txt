cmake_minimum_required(VERSION 2.8.11)

project(rlPlanDemo)

find_package(RL COMPONENTS SG REQUIRED)
find_package(Qt4 REQUIRED)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib-debug)
    set(LIB_INSTALL_DIR ${CMAKE_SOURCE_DIR}/lib-debug)
    set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin-dbg)
else()
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/lib)
    set(LIB_INSTALL_DIR ${CMAKE_SOURCE_DIR}/lib)
    set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)
endif()

if(CMAKE_SIZEOF_VOID_P EQUAL 4)
        add_definitions(-DEIGEN_DONT_ALIGN)
endif(CMAKE_SIZEOF_VOID_P EQUAL 4)

    set(
		HDRS
		ConfigurationDelegate.h
		ConfigurationModel.h
		ConfigurationSpaceScene.h
		ConfigurationSpaceThread.h
		MainWindow.h
		PlannerModel.h
		Thread.h
		Viewer.h
	)
	
	set(
		SRCS
		ConfigurationDelegate.cpp
		ConfigurationModel.cpp
		ConfigurationSpaceScene.cpp
		ConfigurationSpaceThread.cpp
		MainWindow.cpp
		PlannerModel.cpp
		rlPlanDemo.cpp
		Thread.cpp
		Viewer.cpp
	)
	
	qt4_wrap_cpp(
		MOC_SRCS
		ConfigurationDelegate.h
		ConfigurationSpaceScene.h
		ConfigurationSpaceThread.h
		MainWindow.h
		Thread.h
		Viewer.h
		OPTIONS
		-DBOOST_TT_HAS_OPERATOR_HPP_INCLUDED
	)
	
	add_executable(
                rlPlanDemo
		${HDRS}
		${SRCS}
		${MOC_SRCS}
	)
	
	target_compile_definitions(
                rlPlanDemo
                PUBLIC
                "" ${QT_DEFINITIONS}
	)
	
	target_include_directories(
                rlPlanDemo
		PUBLIC
		${OPENGL_INCLUDE_DIR}
		${QT_INCLUDES}
	)
	
	target_link_libraries(
                rlPlanDemo
                ${QT_QTCORE_LIBRARY}
                ${QT_QTGUI_LIBRARY}
                ${QT_QTOPENGL_LIBRARY}
                ${RL_LIBRARIES}
                /usr/lib/x86_64-linux-gnu/libSoQt.so
                /usr/lib/x86_64-linux-gnu/libBulletDynamics.so
                /usr/lib/libode.so
                /usr/lib/libsolid.so
                /usr/lib/x86_64-linux-gnu/mesa/libGL.so

	)
