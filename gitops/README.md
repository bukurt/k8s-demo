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
    namespace: demo
    server: 'https://kubernetes.default.svc'
  source:
    path: gitops/argocd-apps
    repoURL: 'https://github.com/kurtburak/k8s-demo.git'
    targetRevision: HEAD
  project: default
  syncPolicy:
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