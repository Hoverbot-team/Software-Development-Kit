add_library(exampleplugin SHARED ExamplePlugin.cpp)

# Link the SDK interface target to get include paths
target_link_libraries(exampleplugin PRIVATE SDKInterface)

# Set output directory to place the compiled .so files together
set_target_properties(exampleplugin PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/plugins
    PREFIX "lib"
)
