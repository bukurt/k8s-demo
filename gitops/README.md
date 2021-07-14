## GitOps Demos
# Create ArgoCD App of Apps pattern

```
cat <<EOF | kubectl apply -f -
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: argocd-apps
  namespace: argocd
spec:
  destination:
    namespace: demo-gitops
    server: 'https://kubernetes.default.svc'
  source:
    path: gitops/argocd-apps
    repoURL: 'https://github.com/kurtburak/k8s-demo.git'
    targetRevision: HEAD
  project: default
  syncPolicy:
    syncOptions:
    - CreateNamespace=true
    automated:
      prune: true
      selfHeal: false
EOF
```

# Create ArgoCD application definiton yaml
```
cat <<EOF> argocd-apps/http-echo.yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: http-echo
  namespace: argocd
spec:
  destination:
    namespace: demo
    server: 'https://kubernetes.default.svc'
  source:
    path: gitops/apps
    repoURL: 'https://github.com/kurtburak/k8s-demo.git'
    targetRevision: HEAD
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
EOF
```

# Push Application manifest to repository

```
git add argocd-apps/http-echo.yaml
git commit -m "http-echo applicaiton deployment"
git push
````

# Update Applicaiton
````
vi apps/deployment-http-echo.yaml
git add apps/deployment-http-echo.yaml
git commit -m "http-echo application updated!"
git push
```