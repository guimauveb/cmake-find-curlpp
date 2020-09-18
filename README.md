# CMake cURLpp find_package script 

**A CMake script using LibFindMacros.cmake to look for the cURLpp library in an environment**

### Usage

1. In your project folder add the **cmake** directory cloned from this repo
```
~/project_folder/
|-- include
|   |-- header.hxx        
|-- source
|   |-- source.cxx
|-- cmake
|   |-- FindCURLPP.cmake        
|   |-- LibFindMacros.cmake        
|-- CMakeLists.txt
|-- main.cxx
|-- README.md

```
2. Add the following code to your CMakeLists.txt
```
cmake_minimum_required(VERSION 3.10)
project(Project)
#...
# cURLpp requires libcurl to be installed
message(STATUS "Looking for curl...")
find_package(CURL REQUIRED)

if (CURL_FOUND)
    message(STATUS "Found curl version: ${CURL_VERSION_STRING}")
    message(STATUS "Using curl version: ${CURL_INCLUDE_DIRS}")
    message(STATUS "Using curl libraries: ${CURL_LIBRARIES}\n")
    list(APPEND Project_INCLUDE_DIRS ${CURL_INCLUDE_DIRS})
else()
    message(FATAL_ERROR "Could not find curl.")
endif()


message(STATUS "Looking for curlpp...")
find_package(CURLPP REQUIRED)

if (CURLPP_FOUND)
    message(STATUS "Found curlpp version: ${CURLPP_VERSION}")
    message(STATUS "Using curlpp include dir: ${CURLPP_INCLUDE_DIR}")
    message(STATUS "Using curlpp libraries: ${CURLPP_LIBRARY}\n")
    list(APPEND Project_INCLUDE_DIRS ${CURLPP_INCLUDE_DIR})
else()
    message(FATAL_ERROR "Could not find curlpp.")
endif()

target_link_libraries(Project ${CURL_LIBRARIES})
target_link_libraries(Project ${CURLPP_LIBRARY})
```
