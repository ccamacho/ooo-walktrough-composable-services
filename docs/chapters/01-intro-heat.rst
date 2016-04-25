The Heat orchestration service
------------------------------

Template-based orchestration engine for OpenStack resources
(Storage, Networking, Images, Instances, applications, *).

Templates create stacks -> Collection of resources.



resources:
    config:
        type: OS::Heat::SoftwareConfig
        properties
    #Encapsulates the config that you want to apply

    deployment:
        type: OS::Heat::SoftwareDeployment
    #This will trigger the config resource, what to deploy and where to deploy it.



