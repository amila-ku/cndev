---
title: Evaluate Options for Writing a Kubernetes Operator
date: 2000-04-01T22:00:00+00:00
hero: "/images/hero-6.jpg"
excerpt: Kubernetes Operator
timeToRead: 3
authors: []

---
![](https://miro.medium.com/max/794/1*7hJmglcnZMq9z8JC9TLS6Q.png =794x419)

Deploying an application generally involves packaging as a container and creating kubernetes manifests for deployment, but even after being deployed someone would have to manage operations of the application. Kubernetes Operator is a way to package deploy and operate an application. Application in Kubernetes is managed using kubernetes api and kubectl, to efficiently manage stateful applications in kubernetes needs a way to extend the functionality of Kubernetes API cohesively. Operators are a runtime that manages these stateful applications by extending API functionality.

There are multiple options available now to build an Operator, these frameworks can be grouped as below.

**controller-runtime**

* [kubebuilder](https://book.kubebuilder.io/)
* [operator-sdk](https://coreos.com/operators/)

**Other**

* [**meta-controller**](https://metacontroller.app/)
* [**rook-operatorkit**](https://github.com/rook/operator-kit)
* [**kopf**](https://github.com/zalando-incubator/kopf)

**client-go**

* [**sample-controller**](https://github.com/kubernetes/sample-controller)

**shell-operator**

Out of all these options **shell-operator** is available as an option to execute event driven scripts in a kubernetes cluster. MetaController is a add on that can be installed on kubernetes to make it possible to write controllers as a script. Kopf is a python alternative option to using _Go._ But all these frameworks are to make controller building easier by hiding the kubernetes api, which is not great if you want to have full control in your controller.

Sample Controller would be a good option if you know allout about controllers and operators and willing to do all the scaffolding on your own. This would easily end up as very time consuming and lot of head scratching moments.

_Kubebuilder and Operator-sdk_ are based on the controller-runtime. But Operator-sdk also has helm and Ansible based alternative implementation options as well. Since Kubebuilder and and Operator-sdk are the frameworks that provides basic scaffolding for an operator so we can focus more on operator logic without loosing access to kubernetes apis.

Creating a basic operator scaffolding is easy with both frameworks, First step is to generate the project structure.

**Kubebuilder**

Kubebuilder installation details is available [here](https://book.kubebuilder.io/quick-start.html#installation).

Generating project

    kubebuilder init --domain cndev.io

domain should be a valid domain name you own

Add a custom resource api

    kubebuilder create api --group loadtests --version v1 --kind LocustLoadTest

group will be used as custom resource definition versioning along with version number, kind is used to set CRD kind.

to build and install the operator

    make installmake run

**OperatorSDK**

installation instructions is available [here](https://github.com/operator-framework/operator-sdk/blob/master/doc/user/install-operator-sdk.md).

generating a project

    operator-sdk new podset-operator --type=go --repo=/projects/

Add a custom resource

    operator-sdk add api --api-version=app.example.com/v1alpha1 --kind=PodSet

build the operator

    operator-sdk build quay.io/example/podset-operator

So far this was only about how to create the generate operator structure and add new api scaffolding in a project. I will explore more on implementing some functionality using both the frameworks in my next article.

Reference:

[https://github.com/operator-framework/operator-sdk](https://github.com/operator-framework/operator-sdk "https://github.com/operator-framework/operator-sdk")

[https://github.com/kubernetes-sigs/kubebuilder](https://github.com/kubernetes-sigs/kubebuilder "https://github.com/kubernetes-sigs/kubebuilder")

[https://www.youtube.com/watch?v=uf97lOApOv8&list=PLj6h78yzYM2PpmMAnvpvsnR4c27wJePh3&index=205](https://www.youtube.com/watch?v=uf97lOApOv8&list=PLj6h78yzYM2PpmMAnvpvsnR4c27wJePh3&index=205 "https://www.youtube.com/watch?v=uf97lOApOv8&list=PLj6h78yzYM2PpmMAnvpvsnR4c27wJePh3&index=205")