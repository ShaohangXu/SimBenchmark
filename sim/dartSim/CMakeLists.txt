set(CMAKE_CXX_FLAGS_DEBUG
        "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG -Wl,--no-as-needed -O0 -mtune=native")

set(CMAKE_CXX_FLAGS_RELEASE
        "${CMAKE_CXX_FLAGS_RELEASE} -Wl,--no-as-needed -O3 -mtune=native")

# dart (optional)
find_package(DART CONFIG REQUIRED COMPONENTS utils-urdf)
include_directories(${DART_INCLUDE_DIRS})

# source
include_directories(src)

set(DartSim_SRCS
        src/DartWorld.cpp
        src/DartWorld.hpp
        src/DartWorld_RG.cpp
        src/DartWorld_RG.hpp
        src/UserHandle.hpp
        src/object/DartSingleBodyObject.cpp
        src/object/DartSingleBodyObject.hpp
        src/object/DartSphere.cpp
        src/object/DartSphere.hpp
        src/object/DartBox.cpp
        src/object/DartBox.hpp
        src/object/DartCapsule.cpp
        src/object/DartCapsule.hpp
        src/object/DartCheckerBoard.cpp
        src/object/DartCheckerBoard.hpp
        src/object/DartObject.cpp
        src/object/DartObject.hpp
        src/object/DartCylinder.cpp
        src/object/DartCylinder.hpp
        src/object/DartArticulatedSystem.cpp
        src/object/DartArticulatedSystem.hpp)

# library
add_library(DartSimLib ${DartSim_SRCS})
target_link_libraries(DartSimLib
        ${DART_LIBRARIES}
        )

# link
set(DartSimLink
        DartSimLib
        ${BENCHMARK_LINK}
        )

# sub-directories
add_subdirectory(demo)
add_subdirectory(benchmark)