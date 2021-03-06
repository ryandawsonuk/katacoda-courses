OpenFaaS can be installed using Helm. Helm is a package manager for Kubernetes that was previously installed and ready for your instructions.

A common Helm _chart_ is predefined for installing OpenFaaS. Popular incubating and stable charts appear in the [curated Helm chart repository](https://github.com/kubernetes/charts) and there are plans to move OpenFaaS there. For now, a `repo add` command will allow Helm to find the OpenFaaS chart.

`helm repo add openfaas https://openfaas.github.io/faas-netes/`{{execute}}

Install the OpenFaaS operator chart referenced from that repository.

`helm upgrade openfaas --install openfaas/openfaas --namespace openfaas --set functionNamespace=openfaas-fn --set operator.create=true --set basic_auth=true --set rbac=false --set faasIdler.dryRun=false --set faasIdler.inactivityDuration=10s`{{execute}}

The dryRun property is set to false so we can explore scaling near the end of this course.

Watch the 6 deployments for OpenFaaS become _Available_. The _Available_ status column turns from 0 to 1 as each deployment is initialized.

`watch kubectl get deployments --namespace=openfaas`{{execute}}

The installation is complete once all the Deployments have reached an _Available_ state of 1. Use this ```clear```{{execute interrupt}} to ctrl-c and clear the shell or press ctrl-c to break out of the watch.

These instructions have been adopted from the [openfaas-operator](https://github.com/openfaas-incubator/openfaas-operator).