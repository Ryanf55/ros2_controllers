cmake_minimum_required(VERSION 3.16)
project(path_following_controllers LANGUAGES CXX)

if(CMAKE_CXX_COMPILER_ID MATCHES "(GNU|Clang)")
  add_compile_options(-Wall -Wextra -Wconversion)
endif()


find_package(ament_cmake REQUIRED)
find_package (Eigen3 3.3 REQUIRED CONFIG)
# find_package(backward_ros REQUIRED)
# foreach(Dependency IN ITEMS ${THIS_PACKAGE_INCLUDE_DEPENDS})
#   find_package(${Dependency} REQUIRED)
# endforeach()

# generate_parameter_library(joint_trajectory_controller_parameters
#   src/joint_trajectory_controller_parameters.yaml
#   include/joint_trajectory_controller/validate_jtc_parameters.hpp
# )

add_library(npfg_controller
  src/npfg.cpp
)
target_compile_features(npfg_controller PUBLIC cxx_std_20)
target_include_directories(npfg_controller PUBLIC
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/${PROJECT_NAME}>
)
target_link_libraries(npfg_controller PUBLIC
  Eigen3::Eigen
)
# ament_target_dependencies(joint_trajectory_controller PUBLIC ${THIS_PACKAGE_INCLUDE_DEPENDS})

# # Causes the visibility macros to use dllexport rather than dllimport,
# # which is appropriate when building the dll but not consuming it.
# target_compile_definitions(joint_trajectory_controller PRIVATE "JOINT_TRAJECTORY_CONTROLLER_BUILDING_DLL" "_USE_MATH_DEFINES")
# pluginlib_export_plugin_description_file(controller_interface joint_trajectory_plugin.xml)

if(BUILD_TESTING)
  find_package(ament_cmake_gmock REQUIRED)
  find_package(controller_manager REQUIRED)
#   find_package(ros2_control_test_assets REQUIRED)

#   ament_add_gmock(test_trajectory test/test_trajectory.cpp)
#   target_link_libraries(test_trajectory joint_trajectory_controller)

#   ament_add_gmock(test_trajectory_controller
#     test/test_trajectory_controller.cpp)
#   set_tests_properties(test_trajectory_controller PROPERTIES TIMEOUT 220)
#   target_link_libraries(test_trajectory_controller
#     joint_trajectory_controller
#   )

#   ament_add_gmock(test_load_joint_trajectory_controller
#     test/test_load_joint_trajectory_controller.cpp
#   )
#   target_link_libraries(test_load_joint_trajectory_controller
#     joint_trajectory_controller
#   )
#   ament_target_dependencies(test_load_joint_trajectory_controller
#     controller_manager
#     control_toolbox
#     realtime_tools
#     ros2_control_test_assets
#   )

#   ament_add_gmock(test_trajectory_actions
#     test/test_trajectory_actions.cpp
#   )
#   set_tests_properties(test_trajectory_actions PROPERTIES TIMEOUT 300)
#   target_link_libraries(test_trajectory_actions
#     joint_trajectory_controller
#   )
endif()


install(
  DIRECTORY include/
  DESTINATION include/${PROJECT_NAME}
)
install(TARGETS
    npfg_controller
  EXPORT export_{PROJECT_NAME}
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)

ament_export_targets(export_{PROJECT_NAME} HAS_LIBRARY_TARGET)
# ament_export_dependencies(${THIS_PACKAGE_INCLUDE_DEPENDS})
ament_package()
