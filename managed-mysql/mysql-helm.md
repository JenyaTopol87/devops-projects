helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install my-mysql bitnami/mysql \
  --set auth.rootPassword=your-root-password \
  --set auth.database=wordpress \
  --set auth.username=wordpress \
  --set auth.password=your-password \
  --namespace your-namespace
externalDatabase:
  host: my-mysql.your-namespace.svc.cluster.local
  user: wordpress
  password: your-password
  database: wordpress
helm upgrade --install my-wordpress your-wordpress-chart-directory/ \
  --set externalDatabase.host=my-mysql.your-namespace.svc.cluster.local \
  --set externalDatabase.user=wordpress \
  --set externalDatabase.password=your-password \
  --set externalDatabase.database=wordpress \
  --namespace your-namespace
