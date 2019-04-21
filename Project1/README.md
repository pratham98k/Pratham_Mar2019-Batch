ls




#Project1
Project 1 is based on java test applicaton deployned on highly avalibe K8s cluster.

#Namespace : 

Namespaces are intended for use in environments with many users spread across multiple teams, or projects. For clusters with a few to tens of users, you should not need to create or think about namespaces at all. Start using namespaces when you need the features they provide.

Namespaces provide a scope for names. Names of resources need to be unique within a namespace, but not across namespaces. Namespaces can not be nested inside one another and each Kubernetes resources can only be in one namespace.

![Image kubernetes_namespaces](http://www.joseluisgomez.com/wp-content/uploads/2017/10/kubernetes_namespaces.png)


#POD:
A pod (as in a pod of whales or pea pod) is a group of one or more containers (such as Docker containers), with shared storage/network, and a specification for how to run the containers. A pod’s contents are always co-located and co-scheduled, and run in a shared context. A pod models an application-specific “logical host” - it contains one or more application containers which are relatively tightly coupled — in a pre-container world, being executed on the same physical or virtual machine would mean being executed on the same logical host.

![POD] (https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)

#Deployment

A Deployment controller provides declarative updates for Pods and ReplicaSets.

You describe a desired state in a Deployment object, and the Deployment controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.    

![Deployments](https://storage.googleapis.com/cdn.thenewstack.io/media/2017/11/3b60b602-picture2mh.png)


#service

A service can be defined as a logical set of pods. It can be defined as an abstraction on the top of the pod which provides a single IP address and DNS name by which pods can be accessed. With Service, it is very easy to manage load balancing configuration. It helps pods to scale very easily.

![Service](https://d33wubrfki0l68.cloudfront.net/e351b830334b8622a700a8da6568cb081c464a9b/13020/images/docs/services-userspace-overview.svg)

#Replica sets

Replica Set ensures how many replica of pod should be running. It can be considered as a replacement of replication controller. The key difference between the replica set and the replication controller is, the replication controller only supports equality-based selector whereas the replica set supports set-based selector.

![Replicaset](http://www.linuxian.com/img/kubernetes_replicasets.png)
 
#Replication controller

Replication Controller is one of the key features of Kubernetes, which is responsible for managing the pod lifecycle. It is responsible for making sure that the specified number of pod replicas are running at any point of time. It is used in time when one wants to make sure that the specified number of pod or at least one pod is running. It has the capability to bring up or down the specified no of pod.

It is a best practice to use the replication controller to manage the pod life cycle rather than creating a pod again and again.


![Replicationcontroller](https://coreos.com/kubernetes/docs/latest/img/controller.svg)

#Differance Btn Replica set & Replication controller.




Replica Set | Replication Controller 
------------|-------------------------
Replica Set supports the new set-based selector. This gives more flexibility. for eg: environment in (production, qa)  This selects all resources with key equal to environment and value equal to production or qa |   Replication Controller only supports equality-based selector. for eg: environment = production This selects all resources with key equal to This selects all resources with key equal to




#DaemonSets

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

Some typical uses of a DaemonSet are:

running a cluster storage daemon, such as glusterd, ceph, on each node.
running a logs collection daemon on every node, such as fluentd or logstash.
running a node monitoring daemon on every node, such as Prometheus Node Exporter, Sysdig Agent, collectd, Dynatrace OneAgent, AppDynamics Agent, Datadog agent, New Relic agent, Ganglia gmond or Instana agent.


![Daemonsets](https://cdn-images-1.medium.com/max/1600/1*QPFPOV-dDiWjL9H_O4_GUw.png)

#Helm

Helm is the first application package manager running atop Kubernetes. It allows describing the application structure through convenient helm-charts and managing it with simple commands.



we are using Azure AKS

In next post I will be explain how to deploy AKS using ARM OR Terraform later.
 

TO create Namespace use below command.


```
prathamesh@Azure:~$ kubectl create namespace dropwizard
namespace/dropwizard created
```

Now, we are installing Nginx ingress using helm 

```
prathamesh@Azure:~$ helm install stable/nginx-ingress --namespace dropwizard --set controller.replicaCount=2
NAME:   queenly-narwhal
LAST DEPLOYED: Fri Apr 19 17:59:33 2019
NAMESPACE: dropwizard
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                                      DATA  AGE
queenly-narwhal-nginx-ingress-controller  1     1s

==> v1/Pod(related)
NAME                                                            READY  STATUS             RESTARTS  AGE
queenly-narwhal-nginx-ingress-controller-99d6d4c46-gr78s        0/1    ContainerCreating  0         1s
queenly-narwhal-nginx-ingress-controller-99d6d4c46-hb5kr        0/1    ContainerCreating  0         1s
queenly-narwhal-nginx-ingress-default-backend-59ddb57d84-wlgfb  0/1    ContainerCreating  0         1s

==> v1/Service
NAME                                           TYPE          CLUSTER-IP    EXTERNAL-IP  PORT(S)                     AGE
queenly-narwhal-nginx-ingress-controller       LoadBalancer  10.0.204.71   <pending>    80:30016/TCP,443:30932/TCP  1s
queenly-narwhal-nginx-ingress-default-backend  ClusterIP     10.0.226.116  <none>       80/TCP                      1s

==> v1/ServiceAccount
NAME                           SECRETS  AGE
queenly-narwhal-nginx-ingress  1        1s

==> v1beta1/ClusterRole
NAME                           AGE
queenly-narwhal-nginx-ingress  1s

==> v1beta1/ClusterRoleBinding
NAME                           AGE
queenly-narwhal-nginx-ingress  1s

==> v1beta1/Deployment
NAME                                           READY  UP-TO-DATE  AVAILABLE  AGE
queenly-narwhal-nginx-ingress-controller       0/2    2           0          1s
queenly-narwhal-nginx-ingress-default-backend  0/1    1           0          1s

==> v1beta1/PodDisruptionBudget
NAME                                      MIN AVAILABLE  MAX UNAVAILABLE  ALLOWED DISRUPTIONS  AGE
queenly-narwhal-nginx-ingress-controller  1              N/A              0                    1s

==> v1beta1/Role
NAME                           AGE
queenly-narwhal-nginx-ingress  1s

==> v1beta1/RoleBinding
NAME                           AGE
queenly-narwhal-nginx-ingress  1s


NOTES:
The nginx-ingress controller has been installed.
It may take a few minutes for the LoadBalancer IP to be available.
You can watch the status by running 'kubectl --namespace dropwizard get services -o wide -w queenly-narwhal-nginx-ingress-controller'

An example Ingress that makes use of the controller:

  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls

prathamesh@Azure:~$
```


List running nginx ingress service.

```
prathamesh@Azure:~$ kubectl get service -l app=nginx-ingress --namespace dropwizard
NAME                                            TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)                      AGE
queenly-narwhal-nginx-ingress-controller        LoadBalancer   10.0.204.71    104.211.209.195   80:30016/TCP,443:30932/TCP   1m
queenly-narwhal-nginx-ingress-default-backend   ClusterIP      10.0.226.116   <none>            80/TCP                       1m
prathamesh@Azure:~$
```

Now we are installing dropwizard sample Java application on same namespace (Dropwizard)
```
prathamesh@Azure:~$ helm install aks-dropwizard --namespace dropwizard
NAME:   eating-zebu
LAST DEPLOYED: Fri Apr 19 18:02:10 2019
NAMESPACE: dropwizard
STATUS: DEPLOYED

RESOURCES:
==> v1/HorizontalPodAutoscaler
NAME                       REFERENCE                              TARGETS        MINPODS  MAXPODS  REPLICAS  AGE
hpa-dropwizard-autoscaler  Deployment/acs-dropwizard-eating-zebu  <unknown>/50%  1        10       0         0s

==> v1/Pod(related)
NAME                                         READY  STATUS             RESTARTS  AGE
acs-dropwizard-eating-zebu-795dcbd4f6-5wrkp  0/1    ContainerCreating  0         0s
acs-dropwizard-eating-zebu-795dcbd4f6-bnmvw  0/1    ContainerCreating  0         0s
acs-dropwizard-eating-zebu-795dcbd4f6-nbr8z  0/1    ContainerCreating  0         0s

==> v1/Service
NAME            TYPE       CLUSTER-IP  EXTERNAL-IP  PORT(S)  AGE
aks-dropwizard  ClusterIP  10.0.55.9   <none>       80/TCP   0s

==> v1beta1/Deployment
NAME                        READY  UP-TO-DATE  AVAILABLE  AGE
acs-dropwizard-eating-zebu  0/3    3           0          0s
```

now we are installing ingress Controller using kubectl apply  to communicate ingress and Application.

```
prathamesh@Azure:~$
prathamesh@Azure:~$ kubectl apply -f aks-dropwizard.yaml
ingress.extensions/aks-dropwizard-ingress created
prathamesh@Azure:~$ kubectl get ingress --namespace dropwizard
NAME                     HOSTS   ADDRESS   PORTS   AGE
aks-dropwizard-ingress   *                 80      11s

```

list all pod in the dropwizard namespace

```
prathamesh@Azure:~$ kubectl get pod --namespace dropwizard
NAME                                                             READY   STATUS    RESTARTS   AGE
acs-dropwizard-eating-zebu-795dcbd4f6-5wrkp                      1/1     Running   0          15m
acs-dropwizard-eating-zebu-795dcbd4f6-bnmvw                      1/1     Running   0          15m
acs-dropwizard-eating-zebu-795dcbd4f6-nbr8z                      1/1     Running   0          15m
queenly-narwhal-nginx-ingress-controller-99d6d4c46-gr78s         1/1     Running   0          17m
queenly-narwhal-nginx-ingress-controller-99d6d4c46-hb5kr         1/1     Running   0          17m
queenly-narwhal-nginx-ingress-default-backend-59ddb57d84-wlgfb   1/1     Running   0          17m
prathamesh@Azure:~$ kubectl delete pod acs-dropwizard-eating-zebu-795dcbd4f6-5wrkp  --namespace dropwizard
pod "acs-dropwizard-eating-zebu-795dcbd4f6-5wrkp" deleted

```

Now test application using Browser, use ingress IP 

![Iamge](https://github.com/pratham98k/Pratham_Mar2019-Batch/blob/master/Project1/app%20in%20Browser.PNG)
