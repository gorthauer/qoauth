project(qoauth)

message(STATUS "Searching qoauth sources and headers")
# Search for source and headers in source directory

find_package(QCA2 REQUIRED)

set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Search for source and headers in source directory
file(GLOB SRC "${SRC_DIR}/*.cpp")
file(GLOB HDR "${SRC_DIR}/*.h")

# This project will generate library
add_library(qoauth SHARED ${SRC} ${HDR})

include_directories(.
	..
	${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_BINARY_DIR}
	${QCA2_INCLUDE_DIR}
)

update_compiler_flags(qoauth)
add_definitions(-DQOAUTH)

target_link_libraries(qoauth
	${QT_LIBRARIES}
	${QCA2_LIBRARIES}
	)

install(TARGETS qoauth
        RUNTIME DESTINATION ${RLIBDIR}
        LIBRARY DESTINATION ${LIBDIR}
        ARCHIVE DESTINATION ${LIBDIR}
)
