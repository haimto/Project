```
Please make sure to write the commands you are writing as a separate document 
and send all of your solutions to a repository that you own.
Please send me the repo - make sure it’s public.
```

# Part 1
1. Deploy a pod named nginx-pod using the `nginx:alpine` image.
Name: nginx-pod-yourname
Image: nginx:alpine

`
kubectl run nginx-pod-haim --image=nginx:alpine --restart=Never
`

2. Deploy a messaging pod using the `redis:alpine` image with the labels set to `tier=msg`.
Pod Name: messaging
Image: redis:alpine
Labels: tier=msg

`
kubectl run messaging --image=redis:alpine --labels=tier=msg --restart=Never

`

3. Create a namespace named `apx-x998-yourname`

`
kubectl create namespace apx-x998-haim
`

4. Get the list of nodes in JSON format and store it in a file at /tmp/nodes-yourname

`
kubectl get nodes -o json > /tmp/nodes-haim
`

5. Create a service messaging-service to expose the messaging application within the cluster on port 6379.
        a. Use imperative commands - kubectl
        b. Service: messaging-service
        c. Port: 6379
        d. Type: ClusterIp
        e. Use the right labels
`
kubectl expose pod messaging --name=messaging-service --port=6379 --target-port=6379 --type=ClusterIP --labels=tier=msg
`

6. Create a service messaging-service to expose the messaging application within the cluster on port 6379.
        a. Service: messaging-service
        b. Port: 6379
        c. Type: ClusterIp
        d. Use the right labels
`
kubectl ...
`

7. Create a deployment named hr-web-app using the image kodekloud/webapp-color with 2 replicas
        a. Name: hr-web-app
        b. Image: kodekloud/webapp-color
        c. Replicas: 2
`
kubectl create deployment hr-web-app --image=kodekloud/webapp-color --replicas=2
`

8. Create a static pod named static-busybox on the master node that uses the busybox image and the command sleep 1000
        a. Name: static-busybox
        b. Image: busybox

`
kubectl run static-busybox --image=busybox --command -- sleep 1000
`

9. Create a POD in the finance-yourname namespace named temp-bus with the image redis:alpine
        a. Name: temp-bus
        b. Image Name: redis:alpine

`
kubectl create namespace finance-haim

apiVersion: v1
kind: Pod
metadata:
  name: temp-bus
  namespace: finance-haim
spec:
  containers:
  - name: temp-bus-container
    image: redis:alpine
	
	kubectl apply -f temp-bus-pod.yaml
`

10. Create a Persistent Volume with the given specification
        a. Volume Name: pv-analytics
        b. Storage: 100Mi
        c. Access modes: ReadWriteMany
        d. Host Path: /pv/data-analytics

`
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
  capacity:
    storage: 100Mi
  accessModes:
    - ReadWriteMany
  hostPath:
    path: /pv/data-analytics
	
	
`

11. Create a Pod called redis-storage-yourname with image: redis:alpine 
	with a Volume of type emptyDir that lasts for the life of the Pod. specs:.
        a. Pod named 'redis-storage-yourname' 
        b. Pod 'redis-storage-yourname' uses Volume type of emptyDir
        c. Pod 'redis-storage-yourname' uses volumeMount with mountPath = /data/redis

`
apiVersion: v1
kind: Pod
metadata:
  name: redis-storage-haim
spec:
  containers:
  - name: redis-container
    image: redis:alpine
    volumeMounts:
    - name: redis-data
      mountPath: /data/redis
  volumes:
  - name: redis-data
    emptyDir: {}
`

12. Create this pod and attached it a persistent volume called pv-1
        a. Make sure the PV mountPath is hostbase : /data

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: use-pv
  name: use-pvspec-yourname
  containers:
  - image: nginx
    name: use-pv
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
apiVersion: v1
kind: Pod
metadata:
  name: use-pvspec-haim
  labels:
    run: use-pv
spec:
  containers:
  - image: nginx
    name: use-pv
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
  - name: pv-volume
    hostPath:
      path: /data
      type: Directory

`
amswer-12.yaml
`
<<<<<<< HEAD
<<<<<<< HEAD

13. Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. 
=======
=======
>>>>>>> parent of 9985019 (answer example)
    13. Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. 
>>>>>>> parent of 9985019 (answer example)
<BR>	Record the version. 
<BR>	Next upgrade the deployment to version 1.17 using rolling update. 
<BR>	Make sure that the version upgrade is recorded in the resource annotation.
<BR>        a. Deployment : nginx-deploy. Image: nginx:1.16
<BR>        b. Image: nginx:1.16
<BR>        c. Task: Upgrade the version of the deployment to 1:17
<BR>        d. Task: Record the changes for the image upgrade

`
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-deploy
        image: nginx:1.16
kubectl annotate deployment nginx-deploy kubernetes.io/change-cause="Initial deployment with nginx:1.16"
kubectl edit deployment nginx-deploy
changed image to 1.17 and saved
kubectl annotate deployment nginx-deploy kubernetes.io/change-cause="Image upgrade to nginx:1.17"

`
<<<<<<< HEAD
<<<<<<< HEAD

14. Create an nginx pod called nginx-resolver using image nginx, 
=======
=======
>>>>>>> parent of 9985019 (answer example)
    14. Create an nginx pod called nginx-resolver using image nginx, 
>>>>>>> parent of 9985019 (answer example)
	expose it internally with a service called nginx-resolver-service. 
	Test that you are able to look up the service and pod names from within the cluster. 
	Use the image: busybox:1.28 for dns lookup. 
	Record results in /root/nginx-yourname.svc and /root/nginx-yourname.pod
`
apiVersion: v1
kind: Pod
metadata:
  name: nginx-resolver
  labels:
    app: nginx
spec:
  containers:
    - name: nginx-container
      image: nginx
	  
	  apiVersion: v1
kind: Service
metadata:
  name: nginx-resolver-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
	  
	  apiVersion: v1
kind: Pod
metadata:
  name: busybox
spec:
  containers:
    - name: busybox-container
      image: busybox:1.28
      command: [ "/bin/sh", "-c", "sleep 3600" ]
	  
kubectl exec -it busybox -- nslookup nginx-resolver-service > /root/nginx-yourname.svc
kubectl exec -it busybox -- nslookup nginx-resolver > /root/nginx-yourname.pod

`
<<<<<<< HEAD
<<<<<<< HEAD

15. Create a static pod on node01 called nginx-critical with image nginx. 
=======
=======
>>>>>>> parent of 9985019 (answer example)
    15. Create a static pod on node01 called nginx-critical with image nginx. 
>>>>>>> parent of 9985019 (answer example)
	Create this pod on node01 and make sure that it is recreated/restarted automatically in case of a failure.

`
apiVersion: v1
kind: Pod
metadata:
  name: nginx-critical
spec:
  containers:
    - name: nginx
      image: nginx
  restartPolicy: Always
  
  
`


16. Create a pod called multi-pod with two containers.
	Container 1, name: alpha, image: nginx
	Container 2: beta, image: busybox, command sleep 4800.
        a. Environment Variables:
            i. container 1:
            ii. name: alpha

            iii. Container 2:
            iv. name: beta


`
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  containers:
    - name: alpha
      image: nginx
      env:
        - name: name
          value: alpha
    - name: beta
      image: busybox
      command: ["sleep", "4800"]
      env:
        - name: name
          value: beta
`

