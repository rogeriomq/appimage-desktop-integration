SET(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt5 COMPONENTS Gui Widgets)

add_executable(user_apps_monitor
    main.cpp
    $<TARGET_OBJECTS:appimage_dektop_integration>
    Monitor.h
    Monitor.cpp
    )

target_include_directories(user_apps_monitor
    PRIVATE ${libappimage_INCLUDE_DIRECTORIES}
    PRIVATE ${CMAKE_SOURCE_DIR}/src/core
    )

target_link_libraries(user_apps_monitor libappimage Qt5::Core)

add_dependencies(user_apps_monitor libappimage)

install(TARGETS user_apps_monitor RUNTIME DESTINATION bin COMPONENT user-apps-monitor)
install(FILES org.appimage.user_app_monitor.desktop DESTINATION /etc/xdg/autostart COMPONENT user-apps-monitor)