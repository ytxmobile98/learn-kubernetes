# The Kubernetes API

## API Server

The **API server** exposes an HTTP API, enabling end users, different parts of clusters, and external components to communicate with each other.

The **Kubernetes API** lets you query and manipulate the state of API objects in Kubernetes (e.g. Pods, Namespaces, ConfigMaps, and Events). Most operations can be performed using the `kubectl` command-line interface, or other command line tools such as `kubeadm`, or by making REST HTTP calls to the APIs directly.

## The Discovery API

The **Discovery API** provides a list of all group versions and resources supported by Kubernetes, including these resources:

* Name
* Cluster or namespaced scope
* Endpoint URL and supported verbs
* Alternative names
* Group, version, kind

The **Discovery API** is available in both **aggregated** and **unaggregated** forms:

* **Aggregated**: All resources are supported by a cluster through the two endpoints (`/api` and `/apis`). They can drastically reduce the requests sent to fetch the discovery data from the cluster.
* **Unaggregated**: Discovery is published in levels, with the root endpoints publishing discovery information for downstream documents. Additional requests are needed to obtain the discovery document for each group version at `/apis/<group>/<version>`, which advertises the list of resources served under a _particular group version_. These endpoints are used by `kubectl` to fetch the list of resources supported by a cluster.

## OpenAPI V2 & V3

The Kubernetes API server provides aggregated APIs in both **OpenAPI V2** and **OpenAPI V3** formats.

* **OpenAPI V2**: served through the `/openapi/v2` endpoint.
* **OpenAPI V3**: served through the `/openapi/v3` endpoint.