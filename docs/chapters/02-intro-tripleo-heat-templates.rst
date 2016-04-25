TripleO Heat Templates
----------------------


TripleO -> Deploy OpenStack using OpenStack. Then, THT will describe
a template or a set of nested templates to orchestrate how the resources
should be deployed and configured to have an OpenStack cloud.

Let's describe some THT nested features for Neutron services.

In: tripleo-heat-templates/overcloud.yaml

::

                ---> #Reference to a custom Heat resource
                |    #to create the network architecture, defined in:
                |    #tripleo-heat-templates/overcloud-resource-registry-puppet.yaml
  resources:    |    #the network resource will point to network/networks.yaml
    Networks:   |
      type: OS::TripleO::Network  ---> # Also nested resources can be defined,
                                  |    # in this case, the RedisVipPort will be
    RedisVirtualIP:               |    # defined in network/ports/ctlplane_vip.yaml
      depends_on: Networks        |
      type: OS::TripleO::Network::Ports::RedisVipPort
      properties:
        ControlPlaneIP: {get_attr: [ControlVirtualIP, fixed_ips, 0, ip_address]}
        ControlPlaneNetwork: {get_param: NeutronControlPlaneID}
        PortName: redis_virtual_ip
        NetworkName: {get_param: [ServiceNetMap, RedisNetwork]}
        ServiceName: redis


The most relevant part is that all custom resources for T-H-T are defined
in: tripleo-heat-templates/overcloud-resource-registry-puppet.yaml and from
there, links to the actual yaml configuration files.





