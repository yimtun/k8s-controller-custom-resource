# Kubernetes Custom Controller - Custom Resource Handling

**Note**: the source code is _verbosely_ commented, so the source is meant to be read and to teach

## What is this?

An example of a custom Kubernetes controller that's only purpose is to watch for the creation, updating, or deletion of all custom resource of type `Network` (in the all namespaces). This was created as an exercise to understand how Kubernetes controllers work and interact with the cluster and resources.

## Running

Clone repo:

```
$ git clone https://github.com/yimtun/k8s-controller-custom-resource
$ cd k8s-controller-custom-resource
$ go mod init k8s-controller-custom-resource
$ go mod tidy
$ git clone -b release-1.31 --single-branch  https://github.com/kubernetes/code-generator.git ../code-generator
$ ./hack/update-codegen.sh 
```

Prepare build environment:

```
```

Build and run:

```
$ go build -o samplecrd-controller .
$ ./samplecrd-controller -kubeconfig=$HOME/.kube/config -alsologtostderr=true
$ go run  main.go controller.go  --kubeconfig=$HOME/.kube/config -alsologtostderr=true
```

You can also use `samplecrd-controller` to create a Deployment and run it in Kubernetes. Note in this case, you don't need to specify `-kubeconfig` in CMD as default `InClusterConfig` will be used.

## Usage

You should create the CRD of Network first:

```
$ kubectl apply -f crd/network.yaml
```

You can then trigger an event by creating a Network API instance:

```
$ kubectl apply -f example/example-network.yaml
```

CURD the Network API instance, and check the logs of controller. 

Enjoy!
