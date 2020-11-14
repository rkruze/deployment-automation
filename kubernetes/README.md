# Kubernetes Helm Chart

This is the Helm Chart for [Redpanda](https://vectorized.io). A Helm Chart is a collection of files used to describe a set of Kubernetes resources, and may be used to deploy and manage Redpanda in a cloud such as AWS or GCP.

## Local Installation

For development purposes, it can be installed locally on Linux or Mac OS.

* The containers Kubernetes uses are typically Docker ones, so install that first: https://docs.docker.com/get-docker/
* To create a Kubernetes cluster, you need a tool such as kind. The install instructions are here: https://kind.sigs.k8s.io/. (minikube is also popular but it is only good for single-node clusters.)
* To run commands against the cluster you need kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
* Clone this repository (`deployment-automation`).

## Local Usage

- Navigate to this folder (`kubernetes`)
- Run `kind create cluster`
- Run `helm install ./redpanda --generate-name`. This will read the Helm Chart in the redpanda folder and deploy the Redpanda Docker image (the latest from Docker Hub) to pods. It will give you the name of the deployment, e.g. `redpanda-1605313023`.
- Run `kubectl get deployments`. This will show how many replicas in the cluster were successful in starting up and are available.
- Run `kubectl get pods`. This shows the pods (groups of containers) that are running. You will see pod names, e.g. `redpanda-1605313023-866cf7484b-vn4w5`.
- To see the log for Redpanda on one of the pods, run  `kubectl logs <pod-name>`.
- For troubleshooting, this command is also useful: `kubectl describe pod <pod-name>`.
- To clean up, run `kubectl delete deploy  <deployment-name>`. The cluster will still be running, just without Redpanda.
- To experiment, edit the `redpanda/values.yaml` file, and run `helm install ./redpanda --generate-name` again.