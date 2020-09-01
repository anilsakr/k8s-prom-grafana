# k8s-prom-grafana

## Quick start

To quickly start all the things just do this:
```bash
kubectl apply \
  --filename https://raw.githubusercontent.com/anilsakr/k8s-prom-grafana/master/manifest-all.yaml
```
This will create the namespace `monitoring` and bring up all components in there.
To shut down all components again you can just delete that namespace:
```bash
kubectl delete namespace monitoring
```

## Default Dashboards

If you want to re-import the default dashboards from this setup run this job:
```bash
  kubectl apply \
  --filename https://raw.githubusercontent.com/anilsakr/k8s-prom-grafana/master/import-dashboard-job.yaml
```

In case the job already exists from an earlier run, delete it before:
```bash
kubectl --namespace monitoring delete job grafana-import-dashboards
```
To access grafana you can use port forward functionality
```bash
kubectl port-forward --namespace monitoring service/grafana 3000:3000
```
And you should be able to access grafana on `http://localhost:3000/login`
Now, we need the credentials to log into Grafana, use the default credentials,
`username: admin`, `password: admin`

## More Dashboards

See grafana.net for some example [dashboards](https://grafana.net/dashboards) and [plugins](https://grafana.net/plugins).

- Configure [Prometheus](https://grafana.net/plugins/prometheus) data source for Grafana.<br/>
`Grafana UI / Data Sources / Add data source`
  - `Name`: `prometheus`
  - `Type`: `Prometheus`
  - `Url`: `http://prometheus:9090`
  - `Add`

- Import [Prometheus Stats](https://grafana.net/dashboards/2):<br/>
  `Grafana UI / Dashboards / Import`
  - `Grafana.net Dashboard`: `https://grafana.net/dashboards/2`
  - `Load`
  - `Prometheus`: `prometheus`
  - `Save & Open`

- Import [Kubernetes cluster monitoring](https://grafana.net/dashboards/162):<br/>
  `Grafana UI / Dashboards / Import`
  - `Grafana.net Dashboard`: `https://grafana.net/dashboards/162`
  - `Load`
  - `Prometheus`: `prometheus`
  - `Save & Open`
  
  
  ## Credit
  [giantswarm/prometheus](https://github.com/giantswarm/prometheus)
  
