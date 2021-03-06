set(IRODS_PLUGIN_TARGET msi_atomic_apply_metadata_operations)

add_library(${IRODS_PLUGIN_TARGET} MODULE libmsi_atomic_apply_metadata_operations.cpp)

target_compile_definitions(${IRODS_PLUGIN_TARGET} PRIVATE ENABLE_RE
                                                          ${IRODS_COMPILE_DEFINITIONS}
                                                          IRODS_ENABLE_SYSLOG)

set_property(TARGET ${IRODS_PLUGIN_TARGET} PROPERTY CXX_STANDARD ${IRODS_CXX_STANDARD})

target_include_directories(${IRODS_PLUGIN_TARGET} PRIVATE ${CMAKE_BINARY_DIR}/lib/core/include
                                                          ${CMAKE_SOURCE_DIR}/lib/core/include
                                                          ${CMAKE_SOURCE_DIR}/lib/api/include
                                                          ${CMAKE_SOURCE_DIR}/server/drivers/include
                                                          ${CMAKE_SOURCE_DIR}/server/api/include
                                                          ${CMAKE_SOURCE_DIR}/server/core/include
                                                          ${CMAKE_SOURCE_DIR}/server/icat/include
                                                          ${CMAKE_SOURCE_DIR}/server/re/include
                                                          ${IRODS_EXTERNALS_FULLPATH_BOOST}/include
                                                          ${IRODS_EXTERNALS_FULLPATH_FMT}/include)

target_link_libraries(${IRODS_PLUGIN_TARGET} PRIVATE irods_server
                                                     irods_common
                                                     ${IRODS_EXTERNALS_FULLPATH_BOOST}/lib/libboost_filesystem.so
                                                     ${IRODS_EXTERNALS_FULLPATH_BOOST}/lib/libboost_system.so
                                                     ${IRODS_EXTERNALS_FULLPATH_FMT}/lib/libfmt.so)

install(TARGETS ${IRODS_PLUGIN_TARGET}
        LIBRARY DESTINATION ${IRODS_PLUGINS_DIRECTORY}/microservices
        COMPONENT ${IRODS_PACKAGE_COMPONENT_SERVER_NAME})
