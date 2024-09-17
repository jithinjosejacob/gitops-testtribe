# Steps to setup gitops tests

https://docs.testkube.io/articles/argocd-integration

Utilize Testkube cloud for testing

1) Make sure that Docker is up and running, also enable Kubernetes from docker desktop


```
testkube pro init --agent-token=tkcagnt_68f6ca6a8329a62f9120a6545b91f0 --org-id=tkcorg_50d024467b3c0756 --env-id=tkcenv_481d83275cdfb8d7
```

```
testkube set context --org-id tkcorg_50d024467b3c0756 --env-id tkcenv_481d83275cdfb8d7 -c cloud  -k tkcapi_04dca01b2a96b2146834ca5100f8ba
```

2) 

```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

```
kubectl port-forward svc/argocd-server -n argocd 8081:443
```

Navigate to ArgoCD using ```https://localhost:8081/applications```

Sync the changes in ArgoCD

2) Verify that Agent status turns green in TestKube

jithinjosejacob-personal-env

3) Make sure that app is running fine in cluster

```kubectl get svc -n default hello-kubernetes-service```

4) Test Execution and Results

```testkube dashboard```

```testkube get tests```

```testkube run test hello-kubernetes```

```testkube dashboard```

https://app.testkube.io/organization/tkcorg_50d024467b3c0756/environment/tkcenv_481d83275cdfb8d7/dashboard/tests/hello-kubernetes
