ECS is AWS managed container orchestrator.

A cluster is the underlying resources that the container are gong to run on.

ecs task definition file --> blueprint that describes how container should launch. It can contain all of the configuration for more than 1 container. 

A task is an instance of a task definition. It's a running container with settings defined in the task definitions.

ECS services --> a service ensures that a certain number of tasks are running at all times. restarts containers that have exited/crashed. It also monitors the ecs instances, if it fails, the Service will restart task o n a working EC2 instance.

The Load Balancer can be assigned to route external traffic to the service. 

