cmake_minimum_required(VERSION 3.5)
project(fast-radial-solvers VERSION 0.1)

find_package(Matlab)
find_package(Eigen3)

file(GLOB SRC_FILES solvers/*.cpp fullsolvers/*.cpp)
foreach(F IN LISTS SRC_FILES)
    get_filename_component(F_out ${F} NAME_WE F_out)
    message(STATUS "${F} -> ${F_out}")
    matlab_add_mex(NAME ${F_out} SRC ${F})
    target_link_libraries(${F_out} Eigen3::Eigen)
    target_include_directories(${F_out} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
endforeach()
