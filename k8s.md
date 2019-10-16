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

kubectl edit pod myapp-pod

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

\*\* Configuration

\*\*\* Commands and Arguments

To edit a pod:

1. kubectl edit pod <pod name> => Some fields are not editable, on saving it saves the current file in another folder, for
   exampe: /tmp/kubectl-edit-ccvrq.yaml
   kubectl delete pod webapp
   kubectl create -f /tmp/kubectl-edit-ccvrq.yaml

2. kubectl get pod webapp -o yaml > my-new-pod.yaml
   kubectl delete pod webapp
   kubectl create -f my-new-pod.yaml

To edit a deployment:
kubectl edit deployment my-deployment

\*\*\* ConfigMaps

kubectl create configmap <config-name> --from-literal=<key>=<value>
kubeclt create configmap app-config --from-literal=APP_COLOR=blue

kubeclt create configmap <config-name> --from-file<path-to-file>
kubectl create configmap app-config --from-file=app_config.properties

view configmaps:
kubectl get configmaps

describe configmaps:
kubectl describe configmaps

In pod-definition.yaml -> add below spec:
enVFrom: - configMapRef:
name: app-config
In config-map.yaml -> add below metadatza: name: app-config

\*\*\* Secrets

kubectl create secret generic <secret-name> --from-literal=<key>=<value>
kubectl create -f secret generic app-secret --from-literal=DB_Host=mysql --from-literal=DB_User=root --from-literal=DB_Password=password

kubectl create secret generic <secret-name> --from-file=<path-to-file>
kubectl create secret generic app-secret --from-file=app_secret.properties

kubectl create -f secret-data.yaml
=> you must specified secrets into a hash format
echo -n 'mysql' | base64

kubectl get secrets
To get the number of secrets, look at the DATA field

kubeclt describe secrets
=> hide secrets
kubectl get secret app-secret -o yaml
=> show secrets
echo -n 'bXlzcWw=' | base64 --decode

\*\*\*\* Secrets in Pods
envFrom:

- secretRef:
  name: app-secret

\*\*\*\* Secrets in Pods as Volumes
volumes:

- name: app-secret-volume
  secret:
  secretName: app-secret

=> creates a file for each secret

\*\*\* Security Context

spec:
containers:

- name:securityContext:
  > > runAsUser: 1000
  > > capabilities:
  > >
  > > > > add: ["MAC_ADMIN"]

get the user
kubectl exec ubuntu-sleeper whoami
