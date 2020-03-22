---
title: linux
description: CMakeList.txt的写法
date: 2016-11-30 16:05:14 +08:00
tags: linux
category: linux
---

### CMakeList


```
CMakeList 总入口

PROJECT(项目名称)
SET(PROJECT_ROOT_PATH "${CMAKE_SOURCE_DIR}/../")           #工程的根目录，即test
SET(EXECUTABLE_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/bin/")     #可执行生成后存放的目录
SET(LIBRARY_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/lib/")        #静态库生成后存放的目录
INCLUDE_DIRECTORIES("${PROJECT_ROOT_PATH}/include/")       #告诉CMake头文件在哪里？
LINK_DIRECTORIES("${CMAKE_SOURCE_DIR}/lib/")               #告诉CMake静态库在哪里？
ADD_SUBDIRECTORY(src)                                      #多目录，把src目录加进来，src

#src目录下的CMakeList.txt，这个CMake只是简单地把main目录和hello目录链接起来：
ADD_SUBDIRECTORY(main)
ADD_SUBDIRECTORY(hello)

hello静态库：
FILE(GLOB SOURCE_1 "${PROJECT_ROOT_PATH}/hello/*.cpp")     #告诉CMake源文件在哪里？
ADD_LIBRARY(hello STATIC ${SOURCE_1})                      #告诉CMake生成的是一个静态库

main可执行文件：
FILE(GLOB SOURCE_1 "${PROJECT_ROOT_PATH}/main/*.cpp")      #告诉CMake源文件在哪里？
ADD_EXECUTABLE(main ${SOURCE_1})                           #告诉CMake生成一个main可执行文件
TARGET_LINK_LIBRARIES(main hello)                          #告诉CMake静态库在哪里？

```
