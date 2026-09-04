# CMake snippet for OSAL core test

set(TEST_MODULE_FILES
  ut_oscore_binsem_test.c
  ut_oscore_misc_test.c
  ut_oscore_queue_test.c
  ut_oscore_select_test.c
  ut_oscore_countsem_test.c
  ut_oscore_mutex_test.c
  ut_oscore_task_test.c
  ut_oscore_test.c
)

# Skip in Docker/non-native environments: OS_TaskCreate fails configuring a
# custom stack under colima on macOS (OS_Posix_InternalTaskCreate_Impl invalid argument)
if (EXISTS "/.dockerenv" OR NOT CMAKE_SYSTEM_NAME STREQUAL "Linux")
  message(STATUS "Skipping osal_core_UT (Docker or non-Linux environment)")
else()
  add_osal_ut_exe(osal_core_UT ${TEST_MODULE_FILES})
endif()

