#  Copyright (c) Microsoft Corporation. All rights reserved.
#  Licensed under the MIT License.

cmake_minimum_required(VERSION 3.10)

project(HelloWorld_HighLevelApp C)

azsphere_configure_tools(TOOLS_REVISION "20.10")
azsphere_configure_api(TARGET_API_SET "7")

add_executable(${PROJECT_NAME} main.c)
target_link_libraries(${PROJECT_NAME} applibs gcc_s c)

find_path(
    SAMPLE_HW_DEFNS_DIR
    NAMES sample_appliance.json
    PATHS "../HardwareDefinitions/mt3620_rdb" "../../../HardwareDefinitions/mt3620_rdb"
    NO_DEFAULT_PATH NO_CMAKE_FIND_ROOT_PATH)

azsphere_target_hardware_definition(${PROJECT_NAME} TARGET_DIRECTORY "${SAMPLE_HW_DEFNS_DIR}" TARGET_DEFINITION "sample_appliance.json")

azsphere_target_add_image_package(${PROJECT_NAME})
