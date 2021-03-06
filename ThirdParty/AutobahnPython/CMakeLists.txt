vtk_module_impl()
vtk_module_export("")

option(VTK_USE_SYSTEM_AUTOBAHN "Use system Autobahn Python package" OFF)
mark_as_advanced(VTK_USE_SYSTEM_AUTOBAHN)

if(NOT VTK_USE_SYSTEM_AUTOBAHN)
  find_package(PythonInterp)

  include(vtkPythonPackages)

  # Extract path where python module should be copied
  get_property(pymodule_build_dir GLOBAL PROPERTY VTK_PYMODULE_BUILD_DIR)
  get_property(pymodule_install_dir GLOBAL PROPERTY VTK_PYMODULE_INSTALL_DIR)

  set(AutobahnPython_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/autobahn")
  set(AutobahnPython_BINARY_DIR "${pymodule_build_dir}/autobahn")

  build_python_package("AutobahnPython" ${AutobahnPython_SOURCE_DIR}
    ${AutobahnPython_BINARY_DIR})

  install(DIRECTORY ${AutobahnPython_BINARY_DIR}
    DESTINATION "${pymodule_install_dir}"
    COMPONENT Runtime)
endif()
