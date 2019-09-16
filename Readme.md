
# Singapore Enablement

## Github / Git Installation

All required materials for this training is in GitHub. We need to clone the repository and begin our lab.

We begin by installing git and the installation guide is available [here.][GH]

Please check if Git is installed correctly by providing the below inputs 

```
% git --version
git version 2.22.0
```

Please proceed to clone this Github repo:

```
% git clone https://github.com/koushik82/SingaporeEnablement.git
```

## Docker Installation

Docker is your container runtime and this is crucial to run any containers or any development work on your laptop. 

- For Mac [Users][DM]

```
% docker --version

Docker version 19.03.1, build 74b1e89
```

## Kind Installation

Next we move on KinD installation. Documentation is available [here.][KD]
KinD which is Kubernetes IN Docker - local clusters for testing Kubernetes. GitHub page available [here.][KQS]

#### On MacOS / Linux:

```
curl -Lo ./kind https://github.com/kubernetes-sigs/kind/releases/download/v0.5.1/kind-$(uname)-amd64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind
```

#### On Windows:

```
curl.exe -Lo kind-windows-amd64.exe https://github.com/kubernetes-sigs/kind/releases/download/v0.5.1/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
```

## Kubernetes CLI

We also need to able to interact with our clusters for which we would need the kubernetes CLI

```
brew install kubernetes-cli
```

For Linux and Windows users I would recommend taking a look at this [document.][KCLI] 

## Cluster Creation

kind create cluster --config config3 --name lioncity 

## Cluster Add On

### Octant

A web-based, highly extensible platform for developers to better understand the complexity of Kubernetes clusters. More Documentation available [here.][OT]  

```
brew install octant
```

Download a Pre-built Binary (Linux, macOS, Windows)
Open the releases page from a browser and download the latest tarball or zip file.

Extract the tarball or zip where X.Y is the release version:

```
$ tar -xzvf ~/Downloads/octant_0.X.Y_Linux-64bit.tar.gz
octant_0.X.Y_Linux-64bit/README.md
octant_0.X.Y_Linux-64bit/octant
```

#### Verify it runs:

```
$ ./octant_0.X.Y_Linux-64bit/octant version
```

### Prometheus Operator

Prometheus Operator creates/configures/manages Prometheus clusters atop Kubernetes. 

```
% kubectl apply -f prometheus-operator/
```

The Prometheus Operator for Kubernetes provides easy monitoring definitions for Kubernetes services and deployment and management of Prometheus instances.

Once installed, the Prometheus Operator provides the following features:

Create/Destroy: Easily launch a Prometheus instance for your Kubernetes namespace, a specific application or team easily using the Operator.

Simple Configuration: Configure the fundamentals of Prometheus like versions, persistence, retention policies, and replicas from a native Kubernetes resource.

Target Services via Labels: Automatically generate monitoring target configurations based on familiar Kubernetes label queries; no need to learn a Prometheus specific configuration language.

### WeaveScope

Monitoring, visualisation & management for Docker & Kubernetes

```
kubectl apply -f weave-scope/
```

Weave Scope automatically generates a map of your application, enabling you to intuitively understand, monitor, and control your containerized, microservices-based application.

## Useful commands: 

Some useful commands during the lab:

```
export KUBECONFIG="$(kind get kubeconfig-path --name="lioncity")"
kubectl port-forward grafana-598f68c777-llvjg 3000:3000 -n monitoring
kubectl port-forward  weave-scope-app-7b66cc6bf9-c9v2w 4040:4040 -n weave
kubectl -n emojivoto port-forward svc/web-svc 8080:80
kubectl -n namespace port-forward $(kubectl -n namespace get pod -l app=appname -o jsonpath='{.items[0].metadata.name}') port:port &
```

[GH]: https://www.atlassian.com/git/tutorials/install-git
[DM]: https://docs.docker.com/docker-for-mac/
[KD]: https://github.com/kubernetes-sigs/kind
[KCLI]: https://kubernetes.io/docs/tasks/tools/install-kubectl/#before-you-begin
[KQS]: https://github.com/kubernetes-sigs/kind
[OT]: https://github.com/vmware/octant
