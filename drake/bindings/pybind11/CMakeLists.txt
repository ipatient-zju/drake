set(PYDRAKE_INSTALL_DIR lib/python${PYTHON_VERSION_MAJOR}.${PYTHON_VERSION_MINOR}/dist-packages/pydrake)

if(APPLE)
  string(REPLACE "-Wl,-undefined -Wl,error" "" CMAKE_MODULE_LINKER_FLAGS ${CMAKE_MODULE_LINKER_FLAGS})
else()
  string(REPLACE "-Wl,--no-undefined" "" CMAKE_MODULE_LINKER_FLAGS ${CMAKE_MODULE_LINKER_FLAGS})
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-shadow")
include_directories("${NUMPY_INCLUDE_DIRS}")

pybind11_add_module(_pydrake_common pydrake_common.cc)
target_link_libraries(_pydrake_common PRIVATE drakeCommon)
target_compile_options(_pydrake_common PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_common DESTINATION ${PYDRAKE_INSTALL_DIR})

pybind11_add_module(_pydrake_rbtree pydrake_rbtree.cc)
target_link_libraries(_pydrake_rbtree PRIVATE drakeRBM drakeMultibodyParsers Eigen3::Eigen)
target_compile_options(_pydrake_rbtree PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_rbtree DESTINATION ${PYDRAKE_INSTALL_DIR})

pybind11_add_module(_pydrake_autodiffutils pydrake_autodiffutils.cc)
target_link_libraries(_pydrake_autodiffutils PRIVATE drakeRBM drakeMultibodyParsers Eigen3::Eigen)
target_compile_options(_pydrake_autodiffutils PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_autodiffutils DESTINATION ${PYDRAKE_INSTALL_DIR})

pybind11_add_module(_pydrake_ik pydrake_ik.cc)
target_link_libraries(_pydrake_ik PRIVATE drakeIK Eigen3::Eigen)
target_compile_options(_pydrake_ik PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_ik DESTINATION ${PYDRAKE_INSTALL_DIR}/solvers)

pybind11_add_module(_pydrake_symbolic pydrake_symbolic.cc)
target_link_libraries(_pydrake_symbolic PRIVATE drakeOptimization Eigen3::Eigen)
target_compile_options(_pydrake_symbolic PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_symbolic DESTINATION ${PYDRAKE_INSTALL_DIR})

pybind11_add_module(_pydrake_mathematicalprogram pydrake_mathematicalprogram.cc)
target_link_libraries(_pydrake_mathematicalprogram PRIVATE drakeOptimization Eigen3::Eigen)
target_compile_options(_pydrake_mathematicalprogram PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_mathematicalprogram DESTINATION ${PYDRAKE_INSTALL_DIR}/solvers)

pybind11_add_module(_pydrake_ipopt pydrake_ipopt.cc)
target_link_libraries(_pydrake_ipopt PRIVATE drakeOptimization)
set_target_properties(_pydrake_ipopt PROPERTIES OUTPUT_NAME "ipopt")
target_compile_options(_pydrake_ipopt PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_ipopt DESTINATION ${PYDRAKE_INSTALL_DIR}/solvers)

pybind11_add_module(_pydrake_parsers pydrake_parsers.cc)
target_link_libraries(_pydrake_parsers PRIVATE drakeMultibodyParsers)
set_target_properties(_pydrake_parsers PROPERTIES OUTPUT_NAME "parsers")
target_compile_options(_pydrake_parsers PRIVATE "-fvisibility=default")
install(TARGETS _pydrake_parsers DESTINATION ${PYDRAKE_INSTALL_DIR})
