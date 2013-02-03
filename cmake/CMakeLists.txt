# For build tree configuration.
get_target_property( JsonCpp_LIBRARY json LOCATION )
set( JsonCpp_INCLUDE ${JsonCpp_SOURCE_DIR}/include )
configure_file( "${JsonCpp_SOURCE_DIR}/cmake/JsonCppConfig.cmake.in"
  "${JsonCpp_BINARY_DIR}/JsonCppConfig.cmake"
  )

# For install configuration.
if(WIN32)
  get_filename_component( JsonCpp_INSTALL_LIBRARY
    ${JsonCpp_LIBRARY} NAME_WE
    )
  set( JsonCpp_LIBRARY_RELEASE ${CMAKE_INSTALL_PREFIX}/lib/${JsonCpp_INSTALL_LIBRARY}.lib )
  set( JsonCpp_LIBRARY_DEBUG ${CMAKE_INSTALL_PREFIX}/lib/${JsonCpp_INSTALL_LIBRARY}${CMAKE_DEBUG_POSTFIX}.lib )
  set( JsonCpp_LIBRARIES "optimized;${JsonCpp_LIBRARY_RELEASE};debug;${JsonCpp_LIBRARY_DEBUG}" )
else(WIN32)
  get_filename_component( JsonCpp_INSTALL_LIBRARY
    ${JsonCpp_LIBRARY} NAME
    )
  set( JsonCpp_LIBRARIES ${CMAKE_INSTALL_PREFIX}/lib/${JsonCpp_INSTALL_LIBRARY} )
endif(WIN32)  

set( JsonCpp_INCLUDE ${CMAKE_INSTALL_PREFIX}/include )
configure_file( "${JsonCpp_SOURCE_DIR}/cmake/JsonCppConfig.cmake.in"
  "${JsonCpp_BINARY_DIR}/InstallFiles/JsonCppConfig.cmake"
  )
install(FILES
  "${JsonCpp_BINARY_DIR}/InstallFiles/JsonCppConfig.cmake"
  DESTINATION .
  COMPONENT Development
  )
