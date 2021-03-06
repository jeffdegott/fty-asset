cmake_minimum_required(VERSION 3.13)
cmake_policy(VERSION 3.13)

project(fty-asset-server
    VERSION 1.0.0
)

##############################################################################################################
find_package(fty-cmake PATHS ${CMAKE_BINARY_DIR}/fty-cmake)
##############################################################################################################


##############################################################################################################

file(GLOB_RECURSE SOURCES_FILES src/*.cc)

etn_target(exe ${PROJECT_NAME}
    SOURCES
        ${SOURCES_FILES}

    INCLUDE_DIRS
        src
        src/topology
        src/topology/db
        src/topology/msg
        src/topology/persist
        src/topology/shared
        src/asset
        src/asset/conversion
        include
        
    USES_PRIVATE
        fty-asset
        cxxtools
        fty_common_logging
        fty_common_db
        fty_common
        fty_proto
        fty_common_mlm
        fty_common_dto
        fty_asset_activator
        fty_common_messagebus
        tntdb
        czmq
        mlm
        crypto
        protobuf
        uuid
)

#install stystemd config

configure_file(fty-asset.service.in
  "${PROJECT_BINARY_DIR}/fty-asset.service" @ONLY)

install(FILES
  "${PROJECT_BINARY_DIR}/fty-asset.service"
  DESTINATION "${CMAKE_INSTALL_SYSCONFDIR}/systemd/system/"
)


##############################################################################################################

