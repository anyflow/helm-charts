# Prometheus `values.yaml`

## Chart Repository

- https://prometheus-community.github.io/helm-charts
- **README.md** : <https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus>

## ArgoCD application manifest (for `kic-st`)

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: kic-st-prometheus
spec:
	project: cluster
	source:
		repoURL: 'https://prometheus-community.github.io/helm-charts'
		targetRevision: 23.4.0
		chart: prometheus
	destination:
		namespace: ns-cluster
		name: kic-st-cluster
	sources:
		- repoURL: 'https://prometheus-community.github.io/helm-charts'
			targetRevision: 23.4.0
			helm:
				valueFiles:
					- $values/prometheus/kic-st.values.yaml
			chart: prometheus
		- repoURL: 'http://gitea.lgthinq.com/cluster/helm-charts.git'
			targetRevision: main
			ref: values
```