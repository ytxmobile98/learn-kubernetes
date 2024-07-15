# Overview

## Container evolution

![Container evolution](../../../images/Container_Evolution.svg)

* **Traditional deployment**
    * Applications ran directly on physical servers
    * No resource boundaries – leads to allocation issues
    * Not scalable – resources were underutilized on each physical server; hard to maintain many physical servers
* **Virtualized deployment**
    * Allows running multiple virtual machines on a single physical server's CPU; each VM is a full machine running all components – including its operating systems – on top of the virtualized hardware
    * Applications are isolated between VMs, which provides security by preventing information from being freely accessed by different applications
    * Allows for better resource utilization, scalability, and reduction of hardware costs
* **Container deployment**
    * Similar to VMs, but more lightweight – different applications share the same operating system (OS), but still have their own file systems, share of CPU, memory, process space, and more
    * Decoupled from the underlying infrastructure; portable across clouds and OS distributions
    * **Benefits**:
        * Agile application creation and deployment
        * Continuous development, integration, and deployment
        * Dev and Ops separation of concerns
        * Observability
        * Environmental consistency across development, testing, and production
        * Cloud and OS distribution portability
        * Application-centric management
        * Loosely coupled, distributed, elastic, liberated micro-services
        * Resource isolation
        * Resource utilization

## Why you need Kubernetes and what it can do

Kubernetes provides you with:

* Service discovery and balancing
* Storage orchestration
* Automated rollouts and rollbacks
* Automatic bin packing
* Self-healing
* Secret and configuration management
* Batch execution
* Horizontal scaling
* IPv4/IPv6 dual-stack
* Designed for extensibility

## What Kubernetes is not

Kubernetes:

* Does not limit the types of applications supported
* Does not deploy source code and does not build your application
* Does not provide application-level services, such as middleware (for example, message buses), data-processing frameworks (for example, Spark), databases (for example, MySQL), caches, nor cluster storage systems (for example, Ceph) as built-in services
* Does not indicate logging, monitoring, or alerting solutions
* Does not provide nor mandate a configuration language/system (for example, Jsonnet)
* Does not provide nor adopt any comprehensive machine configuration, maintenance, management, or self-healing systems
* Is not a mere orchestration system, but instead eliminates the need for orchestration