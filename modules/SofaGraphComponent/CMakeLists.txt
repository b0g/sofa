cmake_minimum_required(VERSION 2.8)
project(SofaGraphComponent)

set(HEADER_FILES

    initGraphComponent.h
    AddFrameButtonSetting.h
    AddRecordedCameraButtonSetting.h
    AttachBodyButtonSetting.h
    BackgroundSetting.h
    FixPickedParticleButtonSetting.h
    MouseButtonSetting.h
    SofaDefaultPathSetting.h
    StatsSetting.h
    ViewerSetting.h
    Gravity.h
    PauseAnimation.h
    PauseAnimationOnEvent.h
    RequiredPlugin.h
    InteractingBehaviorModel.h

    )

set(SOURCE_FILES

    initGraphComponent.cpp
    AddFrameButtonSetting.cpp
    AddRecordedCameraButtonSetting.cpp
    AttachBodyButtonSetting.cpp
    BackgroundSetting.cpp
    FixPickedParticleButtonSetting.cpp
    MouseButtonSetting.cpp
    SofaDefaultPathSetting.cpp
    StatsSetting.cpp
    ViewerSetting.cpp
    Gravity.cpp
    PauseAnimation.cpp
    PauseAnimationOnEvent.cpp
    RequiredPlugin.cpp

    )

set(GROUP_BASE_DIR "..")

add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries( ${PROJECT_NAME} SofaSimulationTree)
target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>")
target_include_directories(${PROJECT_NAME} PUBLIC "$<BUILD_INTERFACE:${SOFAGENERAL_BUILD_INCLUDE_DIR}>")

set( SOFAGRAPHCOMPONENT_COMPILER_FLAGS "-DSOFA_BUILD_GRAPH_COMPONENT")

set_target_properties( ${PROJECT_NAME} PROPERTIES DEBUG_POSTFIX "_d" )
set_target_properties( ${PROJECT_NAME} PROPERTIES VERSION ${SOFAGENERAL_VERSION} )
set_target_properties( ${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "${SOFAGRAPHCOMPONENT_COMPILER_FLAGS}"  )
set_target_properties( ${PROJECT_NAME} PROPERTIES PUBLIC_HEADER "${HEADER_FILES}" )

install(TARGETS ${PROJECT_NAME}
        COMPONENT SofaGeneral_libraries
        EXPORT    SofaGeneralTargets
        RUNTIME DESTINATION "${SOFAGENERAL_INSTALL_BIN_DIR}"
        LIBRARY DESTINATION "${SOFAGENERAL_INSTALL_LIB_DIR}"
        ARCHIVE DESTINATION "${SOFAGENERAL_INSTALL_LIB_DIR}"
        PUBLIC_HEADER DESTINATION "${SOFAGENERAL_INSTALL_INCLUDE_DIR}/${PROJECT_NAME}"
)
