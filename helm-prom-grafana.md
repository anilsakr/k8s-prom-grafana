# Using Helm to set up Prometheus and Grafana on your Kubernetes cluster

## Installing helm 3 from Script
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
## we need to define the public Kubernetes chart repository in the Helm configuration:
```bash
helm repo add stable https://kubernetes-charts.storage.googleapis.com
```
## Create a new namespace called monitoring:
```bash
kubectl create ns monitoring
```
## Install the Prometheus Operator chart in the monitoring namespace of the cluster:
```bash
helm install stable/prometheus-operator --generate-name --namespace monitoring
kubectl get pods -n monitoring 
```
## Let’s now access the Prometheus & Grafana dashboards and see for ourselves what we get. We will be using the Kubernetes proxy to access it. The Kube proxy allows us to securely tunnel connections to Prometheus using TLS via the Kube API server.
```bash
kubectl get pod -n monitoring
kubectl port-forward -n monitoring prometheus-prometheus-prometheus-oper-prometheus-0 9090
kubectl get pod -n monitoring|grep grafana
kubectl port-forward -n monitoring prometheus-grafana-85b4dbb556-8v8dw 3000
```
##we need the credentials to log into Grafana. For that, we would get the username and password from the secret that Helm installed for us:
#search the grafana credentials in yml file and decode by using echo cHJvbS1vcGVyYXRvcg== | base64 -d
```bash
kubectl get secret -n monitoring
kubectl get secret -n monitoring prometheus-operator-1598859762-grafana -o yaml
```
