# Setup keycloak in Minikube Kubernetes cluster

## Deploying keycloak application
```sh
kubectl apply -f keycloak.yaml
```
> Note: Before starting the deployment change `KC_DB_*` parameters appropriately. You can follow  [Configure Database in k8s](#database-setup-in-kubernetes-cluster)

## Adding ingress rule to access keycloack
```sh
kuectl apply -f keycloak-ingress.yaml
```
> Note: Assuming minikbue IP as 192.168.49.2

## Configuring storages for keycloak
A postgresql database is used to store persistent data and infinispan database server will be used store cache data.

### Database setup in Kubernetes cluster

To setup database [bitnami/postgresql](https://artifacthub.io/packages/helm/bitnami/postgresql) helm chart is used with values in keycloak-postgresql-values.yaml file.

```sh
helm install psql --values keycloak-postgres-values.yaml bitnami/postgresql
```

### Setup infinispan in Kubernetes cluster

To setup infinispan [openshift/infinispan] (https://artifacthub.io/packages/helm/openshift/infinispan) helm chart is used.

```sh
helm install infinispan openshift/infinispan
```

// TODO: Connecting infinispan with keycloak