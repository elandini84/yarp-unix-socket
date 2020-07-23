# Copyright (C) 2006-2020 Istituto Italiano di Tecnologia (IIT)
# All rights reserved.
#
# This software may be modified and distributed under the terms of the
# BSD-3-Clause license. See the accompanying LICENSE file for details.

yarp_prepare_plugin(unix_stream
                    CATEGORY carrier
                    TYPE UnixSocketCarrier
                    INCLUDE UnixSocketCarrier.h
                    EXTRA_CONFIG CODE="UNIX_STR"
                    DEPENDS UNIX
                    INTERNAL
                    QUIET)

if(ENABLE_unix_stream)
  yarp_add_plugin(yarp_unix_stream)
  target_sources(yarp_unix_stream PRIVATE UnixSocketCarrier.cpp
                                          UnixSocketCarrier.h
                                          UnixSockTwoWayStream.cpp
                                          UnixSockTwoWayStream.h
                                          UnixSocketLogComponent.cpp
                                          UnixSocketLogComponent.h)
  target_link_libraries(yarp_unix_stream YARP::YARP_os)
#   list(APPEND YARP_${YARP_PLUGIN_MASTER}_PRIVATE_DEPS YARP_os)

  yarp_install(TARGETS yarp_unix_stream
               EXPORT YARP_${YARP_PLUGIN_MASTER}
               COMPONENT ${YARP_PLUGIN_MASTER}
               LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
               ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
               YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR})

  set_property(TARGET yarp_unix_stream PROPERTY FOLDER "Plugins/Carrier")
endif()
