## Tekton CI/CD Demo
# Create Tekton Tasks
```
kubectl apply \
  -f buildpack-demo/01-buildpacks.yaml \
  -f buildpack-demo/02-git-clone.yaml \
  -f buildpack-demo/03-kubernetes-actions.yaml
```
# Create Persistent Volumes Claims 

`kubectl apply -f buildpack-demo/04-resources-pvc.yaml`


# Create Secret for Image Registry

`kubectl apply -f buildpack-demo/05-auth.yaml`

# Create Image Resource and Pipeline

`kubectl apply -f buildpack-demo/06-pipeline.yaml`

# Create PipelineRun and watch progress

```
kubectl apply -f buildpack-demo/07-run.yaml
tkn pipelinerun logs --last -f
```

# Check Pod and application is up
```
kubectl get pods -w
kubectl port-forward svc/demo-app 8888:8080
```

# Update source code and re-run pipeline

```
vi ../apps/java-maven/src/main/resources/templates/index.html
tkn pipelinerun delete buildpacks-test-pipeline-run
kubectl apply -f buildpack-demo/07-run.yaml
```

# Confirm new pod creation and applicaiton is updated
```
kubectl get pods -w
kubectl port-forward svc/demo-app 8888:8080
```
