# NutanixKarbon
---------------
Performing a Karbon demo shouldn't be hard. Anyone can do this. In fact, that's the point behind Karbon, it's so easy, anyone can demo it. You don't have to be an expert.

## What do I do???
------------------
Too easy. Go through the motions of creating a cluster:
- Select Development Cluster
- Ensure that you select the cluster you want to deploy to
- Select the Node Network that has internet access
- Inform the client that Flannel is the default network provider for Karbon's internal communication
- Very important to put in your cluster login information

After creation, download a new KubeConfig file. Understand that this is only live for 24 hours and will need to be redownloaded.



## Deployement Steps
--------------------
The three items you can deploy are showing common use cases. Nothing too 'deep divy'

1. Deploy Kubernetes Dashboard
![alt text](https://d33wubrfki0l68.cloudfront.net/349824f68836152722dab89465835e604719caea/6e0b7/images/docs/ui-dashboard.png)
"Dashboard is a web-based Kubernetes user interface. You can use Dashboard to deploy containerized applications to a Kubernetes cluster, troubleshoot your containerized application, and manage the cluster resources. You can use Dashboard to get an overview of applications running on your cluster, as well as for creating or modifying individual Kubernetes resources (such as Deployments, Jobs, DaemonSets, etc)." [Web UI Website](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

...after that's done
```
Kubectl proxy 
```
(This will start the proxy server for you to open in a window browers.)
Don't go to 127.0.0.1, but rather go here:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

2. Deploy and Scale Nginx container
Note: Take a few moments before running each command. Containers take time to build.

```
kubectl create deployment --image nginx my-nginx
kubectl get pods
kubectl get deployment
kubectl scale deployment --replicas 2 my-nginx
kubectl get pods
kubectl expose deployment my-nginx --port=80  type=NodePort
kubectl get services
```

3. Deploy Cluster WITH yaml files

Clone files to desired directory, then execute said command in that same directory.
Note: You HAVE to execute the command from INSIDE the directory. Anything else will result in Mathurin and Silva laughing at you.
```
kubectl apply -k .
```
...after a few seconds
```
kubectl get pods
```
