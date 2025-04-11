 helm repo add bitnami https://charts.bitnami.com/bitnami

helm install postgresql bitnami/postgresql --namespace databases --create-namespace \
--set global.defaultStorageClass=longhorn \
--set global.postgresql.auth.enablePostgresUser=true \
--set global.postgresql.auth.postgresPassword="Gr@ssat0" \
--set global.postgresql.auth.username="sonarqube" \
--set global.postgresql.auth.password="D13g0anna" \
--set global.postgresql.auth.database="sonarqube" \
--set architecture="replication" \
--set replication.numSynchronousReplicas=2 \
--set primary.service.type="LoadBalancer"

 \
--set primary.service.loadBalancerIP="10.22.0.210"


helm install sonarqube --namespace development bitnami/sonarqube  --create-namespace \
--set global.defaultStorageClass=longhorn \
--set sonarqubeUsername="diego" \
--set sonarqubePassword="d13g0anna" \
--set sonarqubeEmail="diego.grassato@gmail.com" \
--set postgresql.enabled=false \
--set externalDatabase.host=postgresql-primary.databases.svc.cluster.local \
--set externalDatabase.user=postgres \
--set externalDatabase.password=Gr@ssat0 \
--set externalDatabase.database=sonarqube \
--set externalDatabase.port=5432 \
--set service.type=ClusterIP \
--set ingress.enabled=true \
--set ingress.ingressClassName=traefik \
--set ingress.hostname=sonar.dtux.local \
--set plugins.install[0]="sonar-go" \
--set plugins.install[1]="sonar-java" \
--set plugins.install[2]="sonarjs"


helm install sonarqube --namespace development bitnami/sonarqube  --create-namespace \
--set sonarqubeUsername="diego" \
--set sonarqubePassword="d13g0anna" \
--set sonarqubeEmail="diego.grassato@gmail.com" \
--set postgresql.enabled=false \
--set externalDatabase.port=5432 \
--set service.type=ClusterIP \
--set ingress.enabled=true \
--set ingress.ingressClassName=traefik \
--set ingress.hostname=sonar.dtux.local \
--set plugins.install[0]="sonar-go" \
--set plugins.install[1]="sonar-java" \
--set plugins.install[2]="sonarjs"