\*\* Core Concepts

\*\*\* Cluster 
kubectl cluster-info

\*\*\* Pods
kubectl run nginx --image nginx
kubectl get pods
kubectl get pods -o wide
cat > pod-definition.yaml
vi pod-definition.yaml
kubectl create -f pod-definition.yaml
kubectl describe pod myapp-pod

1. If you are given a pod definition file, edit that file and use it to create a new pod.

2. If you are not given a pod definition file, you may extract the definition to a file using the below command:
kubectl get pod <pod-name> -o yaml > pod-definition.yaml
=> Then edit the file to make the necessary changes, delete and re-create the pod.

3. Use the kubectl edit pod <pod-name> command to edit pod properties.
kubectl edit pod myapp-pod

\*\*\* Replicaset
kubectl create -f rc-definition.yaml
kubectl get replicationcontroller
kubectl get rs
kubectl describe replicaset 

Set the number of replicas inside de replicas-definition.yaml file, then : 
kubectl replace -f replicaset-definition.yaml

Using the filname to increase the number of replicas will not result in increasing its number inside the file
kubectl scale --replicas=6 -f replicaset-definition.yaml

kubectl scale --replicas=6 replicaset myapp-replicaset

kubectl get rs new-replica-set -o yaml > new-replica-set.yaml

\*\*\* Deployments
kubectl create -f deployment-definition.yaml
automatically creates replicaset

\*\*\* Commands and Arguments

\*\*\* ConfigMaps

imperative:
kubectl create configmap <config-name> ==from-literal=<key>=<value>

kubeclt create configmap <config-name> ==from-file<path-to-file>

declarative:
kubeclt create \ app-config --from-literal=APP_COLOR=blue

kubectl create configmap \ app-config --from-file=app_config.properties

view configmaps:
kubectl get configmaps

describe configmaps:
kubectl describe configmaps


\*\* Configuration


