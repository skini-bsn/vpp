# Copyright (c) 2018 Cisco and/or its affiliates.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at:
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

unset (VAPICLIENT_LIB)
unset (ACL_FILE)
unset (NAT_FILE)
unset (L2E_FILE)
unset (GBP_FILE)
unset (IGMP_FILE)
unset (VOM_SOURCES)
unset (VOM_HEADERS)

find_library(VAPICLIENT_LIB NAMES vapiclient REQUIRED)
find_path(VAPICLIENT_INCLUDE_DIR NAMES vapi/vapi.hpp)

if(NOT VAPICLIENT_INCLUDE_DIR OR NOT VAPICLIENT_LIB)
  message(FATAL_ERROR "Cannot find vapiclient library and/or headers")
endif()

include_directories(${VAPICLIENT_INCLUDE_DIR})
include_directories(${CMAKE_SOURCE_DIR})

find_file(ACL_FILE NAMES acl.api.vapi.hpp PATH_SUFFIXES vapi)
find_file(NAT_FILE NAMES nat.api.vapi.hpp PATH_SUFFIXES vapi)
find_file(L2E_FILE NAMES l2e.api.vapi.hpp PATH_SUFFIXES vapi)
find_file(GBP_FILE NAMES gbp.api.vapi.hpp PATH_SUFFIXES vapi)
find_file(IGMP_FILE NAMES igmp.api.vapi.hpp PATH_SUFFIXES vapi)

if(ACL_FILE)
  list(APPEND VOM_SOURCES
    acl_binding_cmds.cpp
    acl_binding.cpp
    acl_ethertype_cmds.cpp
    acl_ethertype.cpp
    acl_l2_rule.cpp
    acl_l3_rule.cpp
    acl_list_cmds.cpp
    acl_list.cpp
    acl_types.cpp
  )
endif()

if(NAT_FILE)
  list(APPEND VOM_SOURCES
    nat_static.cpp
    nat_static_cmds.cpp
    nat_binding.cpp
    nat_binding_cmds.cpp
  )
endif()

if (L2E_FILE)
  list(APPEND VOM_SOURCES
    l2_emulation_cmds.cpp
    l2_emulation.cpp
  )
endif()

if(GBP_FILE)
  list(APPEND VOM_SOURCES
    gbp_recirc_cmds.cpp
    gbp_recirc.cpp
    gbp_subnet_cmds.cpp
    gbp_subnet.cpp
    gbp_endpoint_cmds.cpp
    gbp_endpoint.cpp
    gbp_endpoint_group_cmds.cpp
    gbp_endpoint_group.cpp
    gbp_contract_cmds.cpp
    gbp_contract.cpp
  )
endif()

if (IGMP_FILE)
  list(APPEND VOM_SOURCES
    igmp_binding_cmds.cpp
    igmp_binding.cpp
    igmp_listen_cmds.cpp
    igmp_listen.cpp
  )
endif()

list(APPEND VOM_SOURCES
  types.cpp
  api_types.cpp
  arp_proxy_binding_cmds.cpp
  arp_proxy_binding.cpp
  arp_proxy_config_cmds.cpp
  arp_proxy_config.cpp
  bond_group_binding_cmds.cpp
  bond_group_binding.cpp
  bond_interface_cmds.cpp
  bond_interface.cpp
  bond_member.cpp
  bridge_domain_cmds.cpp
  bridge_domain.cpp
  bridge_domain_arp_entry.cpp
  bridge_domain_arp_entry_cmds.cpp
  bridge_domain_entry_cmds.cpp
  bridge_domain_entry.cpp
  client_db.cpp
  cmd.cpp
  connection.cpp
  dhcp_client_cmds.cpp
  dhcp_client.cpp
  hw_cmds.cpp
  hw.cpp
  inspect.cpp
  interface_cmds.cpp
  interface.cpp
  interface_factory.cpp
  interface_ip6_nd_cmds.cpp
  interface_span_cmds.cpp
  interface_span.cpp
  interface_types.cpp
  ip_punt_redirect_cmds.cpp
  ip_punt_redirect.cpp
  ip_unnumbered_cmds.cpp
  ip_unnumbered.cpp
  l2_binding_cmds.cpp
  l2_binding.cpp
  l2_xconnect_cmds.cpp
  l2_xconnect.cpp
  l3_binding_cmds.cpp
  l3_binding.cpp
  lldp_binding_cmds.cpp
  lldp_binding.cpp
  lldp_global_cmds.cpp
  lldp_global.cpp
  logger.cpp
  neighbour.cpp
  neighbour_cmds.cpp
  object_base.cpp
  om.cpp
  pipe.cpp
  pipe_cmds.cpp
  prefix.cpp
  ra_config.cpp
  ra_prefix.cpp
  route.cpp
  route_cmds.cpp
  route_domain.cpp
  route_domain_cmds.cpp
  sub_interface_cmds.cpp
  sub_interface.cpp
  tap_interface.cpp
  tap_interface_cmds.cpp
  vxlan_tunnel_cmds.cpp
  vxlan_tunnel.cpp
)

if(ACL_FILE)
  list(APPEND VOM_HEADERS
    acl_binding.hpp
    acl_ethertype.hpp
    acl_l2_rule.hpp
    acl_l3_rule.hpp
    acl_list.hpp
    acl_types.hpp
  )
endif()

if(NAT_FILE)
  list(APPEND VOM_HEADERS
    nat_static.hpp
    nat_binding.hpp
  )
endif()

if(L2E_FILE)
  list(APPEND VOM_HEADERS
    l2_emulation.hpp
  )
endif()

if(GBP_FILE)
  list(APPEND VOM_HEADERS
    gbp_endpoint.hpp
    gbp_endpoint_group.hpp
    gbp_subnet.hpp
    gbp_recirc.hpp
    gbp_contract.hpp
  )
endif()

if(IGMP_FILE)
  list(APPEND VOM_HEADERS
    igmp_binding.hpp
    igmp_listen.hpp
  )
endif()

list(APPEND VOM_HEADERS
  arp_proxy_binding.hpp
  arp_proxy_config.hpp
  bond_group_binding.hpp
  bond_interface.hpp
  bond_member.hpp
  bridge_domain.hpp
  bridge_domain_arp_entry.hpp
  bridge_domain_entry.hpp
  client_db.hpp
  cmd.hpp
  connection.hpp
  dhcp_client.hpp
  dump_cmd.hpp
  enum_base.hpp
  event_cmd.hpp
  hw.hpp
  inspect.hpp
  interface.hpp
  interface_cmds.hpp
  interface_ip6_nd.hpp
  interface_span.hpp
  ip_punt_redirect.hpp
  ip_unnumbered.hpp
  l2_binding.hpp
  l2_xconnect.hpp
  l3_binding.hpp
  lldp_binding.hpp
  lldp_global.hpp
  logger.hpp
  neighbour.hpp
  object_base.hpp
  om.hpp
  pipe.hpp
  prefix.hpp
  ra_config.hpp
  ra_prefix.hpp
  route.hpp
  route_domain.hpp
  rpc_cmd.hpp
  singular_db.hpp
  singular_db_funcs.hpp
  sub_interface.hpp
  tap_interface.hpp
  types.hpp
  api_types.hpp
  vxlan_tunnel.hpp
)

add_definitions(-Wall -Werror -std=gnu++11)

add_vpp_library(vom
  SOURCES ${VOM_SOURCES}

  INSTALL_HEADERS ${VOM_HEADERS}

  LINK_LIBRARIES ${VAPICLIENT_LIB} Threads::Threads boost_thread
    ${BOOST_SYSTEM_LIB} ${BOOST_FILESYSTEM_LIB} ${BOOST_ASIO_LIB} m rt

  COMPONENT libvom
)
