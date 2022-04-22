odoo-spawner
====
If you want to deploy Odoo_ inside Kubernetes_ (minikube) and have **multiple** instance of it inside your cluster follow this instructions.
I am using Odoo community edition chart provided by bitnami_.

**requirements**

You need to install the following before we can start.
* Install Docker_
* Install minikube_
* Install kubectl_
* Install helm_

After installing the required software we need to create a new Kubernetes cluster:

``minikube start --profile my-cluster``

here I named it ``my-cluster`` but you can use your own.
Then we start Kubernetes dashboard:

``minikube dashboard -p my-cluster``

the Odoo service defined in the bitnami chart is of type ``LoadBalancer``, so we need to run the following command to be able to access the Odoo url:
``minikube tunnel -p my-cluster``

.. _Odoo: https://www.odoo.com/
.. _Kubernetes: https://kubernetes.io/ 
.. _Docker: https://docs.docker.com/get-docker/
.. _minikube: https://minikube.sigs.k8s.io/docs/start/
.. _kubectl: https://kubernetes.io/docs/tasks/tools/
.. _helm: https://helm.sh/docs/intro/install/
.. _bitnami: https://bitnami.com/stack/odoo/helmclone the repository containging the Odoo chart:

1. clone the repository containging the Odoo chart:
``git clone https://github.com/bitnami/charts.git``

2. change directory to where Odoo chart is loacted:
``cd ./charts/bitnami/odoo``

3. this chart has some depencies like PostgreSQL, run this command to get them:
``helm dependency update``

4. now we need to create the helm pachake for Odoo:
``helm package .``

depending on the current version of the chart it will create a file named like this:
``odoo-21.2.8.tgz``

Now if you want to run a new instance of Odoo inside your Kubernetes run the following command:
``helm install fshahy ./odoo-21.2.8.tgz``

note that I used ``fshahy`` as my installation name.
Off course you can use any other nameand have multiple instances od Odoo running inside your Kubernetes.
