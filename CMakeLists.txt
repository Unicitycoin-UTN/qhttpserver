# Set cmake minimum requirements
cmake_minimum_required(VERSION 3.12)

# Set CXX project
project(QHttpServer LANGUAGES CXX)

# Set CXX Standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find QT5
find_package(Qt5 COMPONENTS Core Network REQUIRED)

# Enable Qt MOC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

# Create main library
add_library(QHttpServer STATIC
    http-parser/http_parser.h
    http-parser/http_parser.cpp
    src/qhttpconnection.cpp
    src/qhttpconnection.h
    src/qhttprequest.cpp
    src/qhttprequest.h
    src/qhttpresponse.cpp
    src/qhttpresponse.h
    src/qhttpserver.cpp
    src/qhttpserver.h
    src/qhttpserverapi.h
    src/qhttpserverfwd.h
)

# Link dependencies
target_link_libraries(QHttpServer
PRIVATE
    Qt::Core
    Qt::Network
)

# Define include directories
target_include_directories(QHttpServer
PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/http-parser
)