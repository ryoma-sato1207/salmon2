include(${CMAKE_SOURCE_DIR}/cmakefiles/create_test.cmake)

if (USE_MPI)
  find_package(MPI REQUIRED)
  set(TEST_MPI_NPROC 4)
  set(TEST_COMMAND "${MPIEXEC} ${MPIEXEC_NUMPROC_FLAG} ${TEST_MPI_NPROC} ${CMAKE_BINARY_DIR}/${TARGET_NAME}")
else ()
  set(TEST_COMMAND "${CMAKE_BINARY_DIR}/${TARGET_NAME}")
endif ()
message(STATUS "testing command: ${TEST_COMMAND}")

add_custom_target("check_test_requirements" COMMAND ${CMAKE_CTEST_COMMAND} DEPENDS ${TARGET_NAME})
add_custom_target("test_preparations" ALL
                  COMMAND ${CMAKE_COMMAND} -E cmake_echo_color --cyan "generate ctest scripts"
                  COMMAND ${CMAKE_COMMAND} -E copy_directory "${CMAKE_CURRENT_SOURCE_DIR}/pseudo"  "${CMAKE_CURRENT_BINARY_DIR}/pseudo"
                  COMMAND ${CMAKE_COMMAND} -E copy_directory "${CMAKE_SOURCE_DIR}/samples"         "${CMAKE_BINARY_DIR}/samples"
                  COMMAND ${CMAKE_COMMAND} -E copy_directory "${CMAKE_SOURCE_DIR}/src/ttm/example" "${CMAKE_BINARY_DIR}/example")

# test directories
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/101_C2H2_gs")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/102_C2H2_rt_response")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/103_C2H2_rt_pulse")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/104_C2H2_gs_op")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/105_C2H2_rt_response_rp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/111_bulk_Si_gs_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/112_bulk_Si_rt_response_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/113_bulk_Si_rt_pulse_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/116_bulk_Si_rt_response_dp_kp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/117_bulk_Si_rt_response_dp_op")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/118_bulk_Si_gs_dp_ffte")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/119_bulk_Si_rt_response_dp_ffte")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/121_bulk_Si_gs_temperature_dp_op")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/122_bulk_Si_rt_response_temperature_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/123_periodic_H2O_gs_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/124_periodic_H2O_md_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/125_periodic_H2O_opt_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/126_periodic_H2O_dft_md_dp")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/127_periodic_H2O_gs_dp_scalapack")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/128_periodic_H2O_gs_dp_eigenexa")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/131_bulk_Si_nonorthogonal_lattice")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/132_bulk_Si_nonorthogonal_lattice_rt")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/141_bulk_Si_singlescale")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/151_bulk_Si_multiscale")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/152_bulk_Si_multiscale_restart")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/161_Jellium_isolated_gs")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/162_Jellium_isolated_rt_response")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/163_Jellium_periodic_gs")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/164_Jellium_periodic_rt_response")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/201_gs_restart")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/202_rt_checkpoint_single")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/203_rt_restart_single")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/204_rt_checkpoint_self")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/205_rt_restart_self")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/206_gs_wf_slice")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/207_rt_wf_slice")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/301_classicEM_isolated_lr")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/302_classicEM_periodic_lr")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/303_classicEM_isolated_pulse_ttm")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/401_bulk_Si_gs_dp_libxc_pz")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/410_bulk_Si_gs_initial_density")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/411_bulk_Si_gs_symmetry")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/412_bulk_Si_gs_symmetry_yyn")
add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/413_bulk_Si_rt_response_symmetry_yyn")
