add_library(bluetooth INTERFACE)

target_sources(bluetooth INTERFACE
 ${CMAKE_CURRENT_LIST_DIR}/hc_05.c
)

target_include_directories(bluetooth INTERFACE ${CMAKE_CURRENT_LIST_DIR})
