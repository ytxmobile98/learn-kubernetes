# Running automated tasks with a CronJob

> Reference: https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/

## Before you begin

You need the following items:

* A cluster with at least _two nodes_ that are _not acting as control plane hosts_
* `kubectl` command line tool configured to communicate with your cluster

If you do not have a cluster, you can create one by using [minikube](https://minikube.sigs.k8s.io/docs/tutorials/multi_node/), or use one of these Kubernetes playgrounds:

* [Killercoda](https://killercoda.com/playgrounds/scenario/kubernetes)
* [Play with Kubernetes](https://labs.play-with-k8s.com/)

## Creating a CronJob

1. Configure a simple demonstration task that runs every minute:

    ```yaml
    apiVersion: batch/v1
    kind: CronJob
    metadata:
    name: hello
    spec:
    schedule: "* * * * *"
    jobTemplate:
        spec:
        template:
            spec:
            containers:
            - name: hello
                image: busybox:1.28
                imagePullPolicy: IfNotPresent
                command:
                - /bin/sh
                - -c
                - date; echo Hello from the Kubernetes cluster
            restartPolicy: OnFailure
    ```

    Run the example:

    ```bash
    kubectl create -f https://k8s.io/examples/application/job/cronjob.yaml
    ```

    Sample output:

    ```
    cronjob.batch/hello created
    ```

2. After creating the cron job, get its status:

    ```bash
    kubectl get cronjob hello
    ```

    Sample output:

    ```
    NAME    SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
    hello   * /1 * * * *    False     0        <none>          1s
    ```

    The output shows that the cron job has not scheduled or run any jobs yet. Watch for the job to be created in around one minute:

    ```bash
    kubectl get jobs --watch
    ```

    Sample output:

    ```
    NAME               COMPLETIONS   DURATION   AGE
    hello-4111706356   0/1                      0s
    hello-4111706356   0/1           0s         0s
    hello-4111706356   1/1           5s         5s
    ```

    Then you see one running job scheduled by the "hello" cron job. You can stop watching the job and view the cron job again to see that it scheduled the job:

    ```bash
    kubectl get cronjob hello
    ```

    Sample output:

    ```
    NAME    SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
    hello   */1 * * * *   False     0        50s             75s
    ```

    Here the cron job `hello` successfully scheduled a job at the time specified in `LAST SCHEDULE`. There are currently 0 active jobs, meaning that the job has completed or failed.
3. Find the jobs that the last scheduled job created and view the standard output of one of the pods:

    > **Note**: The job name is different from the pod name.

    ```bash
    # Replace "hello-4111706356" with the job name in your system
    pods=$(kubectl get pods --selector=job-name=hello-4111706356 --output=jsonpath={.items[*].metadata.name})
    ```

    Show the pod log:

    ```bash
    kubectl logs $pods
    ```

    The output is similar to this:

    ```
    Fri Feb 22 11:02:09 UTC 2019
    Hello from the Kubernetes cluster
    ```

## Deleting a CronJob

When you no longer need a CronJob, you can delete it:

```bash
kubectl delete cronjob hello
```

This acction removes all the jobs and pods it created and stops it from creating additional jobs.

See more: [garbage collection](https://kubernetes.io/docs/concepts/architecture/garbage-collection/)