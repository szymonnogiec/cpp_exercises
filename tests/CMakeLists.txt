cmake_minimum_required(VERSION 3.8)
project(loggi_tests)

add_subdirectory("${CMAKE_SOURCE_DIR}/extern/googletest" "extern/googletest")

#The next line is optional, but keeps your CACHE cleaner
mark_as_advanced(
        BUILD_GMOCK BUILD_GTEST BUILD_SHARED_LIBS
        gmock_build_tests gtest_build_samples gtest_build_tests
        gtest_disable_pthreads gtest_force_shared_crt gtest_hide_internal_symbols
)

set_target_properties(gtest PROPERTIES FOLDER extern)
set_target_properties(gtest_main PROPERTIES FOLDER extern)
set_target_properties(gmock PROPERTIES FOLDER extern)
set_target_properties(gmock_main PROPERTIES FOLDER extern)

macro(package_add_test TESTNAME)
    add_executable(${TESTNAME} ${ARGN})
    target_link_libraries(${TESTNAME} gtest gmock gtest_main)
    add_test(NAME ${TESTNAME} COMMAND ${TESTNAME})
    set_property(TARGET ${TESTNAME} PROPERTY CXX_STANDARD 17)
    set_target_properties(${TESTNAME} PROPERTIES FOLDER tests)
endmacro()

package_add_test(cpp_excercises_tests
        lf_test.cpp
        math_test.cpp)