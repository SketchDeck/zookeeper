## Setup

This repo is our Zookeeper docker source. 

It is automatically built by Semaphore, then pushed to AWS ECS repo.

To get it running on ECS, you need to create a new task definition pointing at your newer image in the repo (they are tagged by Semaphore build number). Then set the service to have zero tasks of the old task definition, then set the service to have one task of the new task definition.

To debug ssh into the ec2 instance and docker log the process


## Running

This Docker image contains Zookeeper 3.5.1-rc2 which features dynamic host reconfiguration. Upon start, it attempts to join an existing cluster.

The syntax to start a container is like this:

  `docker run --net host --name [name] containersol/zookeeper [id] [ip]`
  
where 
  - `id` = id of the zookeeper node (known internally as myid)
  - `ip` = ip address of a node of the existing cluster
  
The `id` is mandatory, the `ip` is optional.

The `--net host` is needed for zookeepers on different hosts to be able to contact each other.
