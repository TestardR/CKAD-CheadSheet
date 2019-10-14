\*\* Core Concepts

\*\* Configuration

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
