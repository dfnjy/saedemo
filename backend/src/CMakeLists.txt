project (demoserver)

find_package(Protobuf REQUIRED)
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS interface.proto)

include_directories ("${SAE_SOURCE_DIR}/src/saedb")
include_directories("${PROTOBUF_INCLUDE_DIRS}")
include_directories("${CMAKE_CURRENT_BINARY_DIR}")

file (GLOB server_SOURCES "*.hpp" "*.cpp")

add_executable(server ${server_SOURCES} ${PROTO_SRCS} ${PROTO_HDRS})
target_link_libraries(server RpcServer glog ${PROTOBUF_LIBRARY} indexing)