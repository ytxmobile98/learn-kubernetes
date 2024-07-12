# Overview

## Container evolution

![Container evolution](./images/Container_Evolution.svg)

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