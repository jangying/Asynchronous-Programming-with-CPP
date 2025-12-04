# Output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BINARY_DIR}/Chapter_10)

# Set C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if(POLICY CMP0167)
  cmake_policy(SET CMP0167 NEW)
endif()

if (WIN32)
  add_definitions(-D_WIN32_WINNT=0x0A00) 
endif()
if(MSVC)
    add_compile_options(/MD)
endif()

# Include Boost::Cobalt
find_package(Boost REQUIRED COMPONENTS thread container cobalt)

# Include Boost directories
include_directories(${Boost_INCLUDE_DIRS})

# Create executable for each cpp file
file(GLOB SOURCES "*.cpp")
foreach(SOURCE ${SOURCES})
    get_filename_component(EXECUTABLE_NAME ${SOURCE} NAME_WE)
    add_executable(${EXECUTABLE_NAME} ${SOURCE})
    target_link_libraries(${EXECUTABLE_NAME} ${Boost_LIBRARIES})
endforeach()
