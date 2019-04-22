#Autoscaling

The Horizontal Pod Autoscaler automatically scales the number of pods in a replication controller, deployment or replica set based on observed CPU utilization (or, with custom metrics support, on some other application-provided metrics). Note that Horizontal Pod Autoscaling does not apply to objects that can’t be scaled, for example, DaemonSets.


```
kubectl apply -f hpa-example.yml


```

To generate load to auto scale pod

```
kubectl run -i --tty busybox --image=busybox --restart=Never -- sh

```
