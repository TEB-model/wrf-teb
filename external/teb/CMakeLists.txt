# WRF-TEB (https://github.com/teb-model/wrf-teb).
# Copyright 2018-2020 D. Meyer. Licensed under the MIT License.

include(ExternalProject)

if (DEFINED TEB_DIR)
    set(dir_options
        SOURCE_DIR ${TEB_DIR}
        BUILD_ALWAYS 1
        )
else()
    set(dir_options
        GIT_REPOSITORY https://github.com/teb-model/teb
        # TODO revert to tag after new release is out
        GIT_TAG 23ca2c7b3561bbebcfa51f7fdd07f002bd6fc4ca
        )
endif()

ExternalProject_Add(teb-project
    ${dir_options}
    INSTALL_COMMAND ""
    CMAKE_ARGS
        -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
        -DCMAKE_Fortran_COMPILER=${CMAKE_Fortran_COMPILER}
        -DCMAKE_Fortran_FLAGS_DEBUG=${CMAKE_Fortran_FLAGS_DEBUG}
        -DCMAKE_Fortran_FLAGS_RELEASE=${CMAKE_Fortran_FLAGS_RELEASE}
        -DCMAKE_Fortran_FLAGS=${CMAKE_Fortran_FLAGS}
        -DUSE_REAL8=${USE_REAL8}
        -DBUILD_SHARED_LIBS=ON
    BUILD_BYPRODUCTS <BINARY_DIR>/${CMAKE_SHARED_LIBRARY_PREFIX}teb${CMAKE_SHARED_LIBRARY_SUFFIX}
)

ExternalProject_Get_Property(teb-project binary_dir)

add_library(teb INTERFACE)
add_dependencies(teb teb-project)
target_include_directories(teb INTERFACE ${binary_dir}/mod)
set(libteb_path ${binary_dir}/${CMAKE_SHARED_LIBRARY_PREFIX}teb${CMAKE_SHARED_LIBRARY_SUFFIX})
target_link_libraries(teb INTERFACE ${libteb_path})
install(FILES ${libteb_path} DESTINATION lib)
