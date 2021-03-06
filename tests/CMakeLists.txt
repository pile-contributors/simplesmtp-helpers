# ============================================================================
#
# This file hosts all tests.
#
# If INCLUDE_PILE_SOURCES_DIRECTLY is ON then SIMPLESMTP_SOURCES and
# SIMPLESMTP_HEADERS are defined we add them to the executable. SIMPLESMTP_LIBRARY
# is empty.
#
# On the other hand if INCLUDE_PILE_SOURCES_DIRECTLY is
# OFF then SIMPLESMTP_SOURCES and SIMPLESMTP_HEADERS are empty and we link
# against SIMPLESMTP_LIBRARY that is now the name of the target that
# builds the library.
#
# ============================================================================

find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

if (NOT INCLUDE_PILE_SOURCES_DIRECTLY)
    set (SIMPLESMTP_LIBRARY simplesmtp)
endif()

add_executable(test_basic
    ${SIMPLESMTP_SOURCES}
    ${SIMPLESMTP_HEADERS}
    ${USERMSG_SOURCES}
    ${USERMSG_HEADERS}
    basic.cc)

target_link_libraries(test_basic
    ${GTEST_BOTH_LIBRARIES}
    ${SIMPLESMTP_LIBRARY}
    ${USERMSG_LIBRARY})

qt5_use_modules(test_basic Core Network Gui)

add_test(
    NAME test_basic
    COMMAND $<TARGET_FILE:test_basic>)
