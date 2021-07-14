## Simple Kubernetes Demos
# 1. Create demo namespace

`kubectl create namespace demo`

`kubectl create -f 01-namespace.yaml`

# 2. Create nginx deployment

`kubectl create deployment nginx --image=nginx:1.20-alpine`

`kubectl apply -f 02-nginx-deployment.yaml`

# 3. Expose nginx deployment via service

`kubectl expose deployment nginx --port 80`

`kubectl apply -f 03-nginx-service.yaml`

# 4. Test nginx is running

`kubectl port-forward service/nginx 8080:80`

`curl localhost:8080`
# 5. Create configMap

`kubectl create configmap nginx-config --from-file=hello-plain-text.conf`

`kubectl apply -f 05-nginx-configmap.yaml`

# 6. Configure a configMap as a volumeMount

`kubectl apply -f 06-nginx-deployment-with-configmap.yaml`

# 7. Scale nginx deployment

`kubectl scale deployment nginx --replicas=3`

`kubectl apply -f 07-nginx-deployment-scale.yaml`

# 8. Update nginx image version

`kubectl patch deployment nginx --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"nginx:1.21-alpine"}]'`

`kubectl apply -f 08-nginx-deployment-update.yaml`

# 9. Check current image

`kubectl get pods -o custom-columns=NAME:spec.containers[*].name,IMAGE:spec.containers[*].image`

# 10. Check rollout history

`kubectl rollout history deployment nginx`

`kubectl rollout history deployment nginx --revision 3`

# 11. Rollback to previous revision

`kubectl rollout undo deployment nginx`

`kubectl rollout undo deployment nginx --to-revision 2`



# 

