# Kubernetes components

![Kubernetes components](./images/components-of-kubernetes.svg)

## Control Plane components

> The control plane's components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a Deployment's replicas field is unsatisfied).
>
> Control plane components can be run on any machine in the cluster. However, for simplicity, setup scripts typically start all control plane components on the same machine, and do not run user containers on this machine.

* **kube-apiserver**: The API server which exposes the Kubernetes API; frontend of the Kubernetes control plane.
* **etcd**: A consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data.
* **kube-scheduler**: Watches for newly created Pods with no assigned node, and selects a node for them to run on.
* **kube-controller-manager**: Runs controller processes.
* **cloud-controller-manager**: Embeds cloud-specific control logic; lets you link your cluster into your cloud provider's API.

## Node components

> Node components run on every node, maintaining running pods and providing the Kubernetes runtime environment.

* **kubelet**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
* **kube-proxy**: A network proxy that runs on each node in your cluster, maintaining network rules which allow network communication to your Pods from network sessions inside or outside of your cluster.
* **Container runtime**: A fundamental component that empowers Kubernetes to run containers effectively; responsible for managing the execution and lifecycle of containers within the Kubernetes environments.

## Addons

> Addons use Kubernetes resources (DaemonSet, Deployment, etc) to implement cluster features. Because these are providing cluster-level features, namespaced resources for addons belong within the kube-system namespace.
>
> More info: <https://kubernetes.io/docs/concepts/cluster-administration/addons/>

Selected addons:

* **DNS**: A DNS server serving the DNS records for Kubernetes services.
* **Web UI (Dashboard)**: The web-based UI for Kubernetes clusters.
* **Container resource monitoring**: Records generic time-series metrics about containers in a central database, and provides a UI for browsing that data.
* **Cluster-level logging**: Responsible for saving container logs to a central log store with search / browsing interface.
* **Network plugins**: Implement the container network interface (CNI) specification; responsible for allocating IP addresses to pods and enabling communications between them within the cluster.