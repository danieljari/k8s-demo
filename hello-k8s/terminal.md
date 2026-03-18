Deployment 


Deployments

Here's the Deployment manifest for our demo app:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo
  labels:
    app: demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
        - name: demo
          image: cloudnatived/demo:hello
          ports:
          - containerPort: 8888



Port and image name is the important part of this ^


Using kubectl apply

Try the following commands in this directory:

kubectl apply -f k8s/deployment.yaml
deployment.apps "demo" created
After a few seconds, a demo pod should be running:

kubectl get pods --selector app=demo
NAME                    READY     STATUS    RESTARTS   AGE
demo-6d99bf474d-z9zv6   1/1       Running   0          2m
failed:

SOLUTION:
minikube delete
minikube start

# point minikube to the docker-environment 
eval $(minikube docker-env)

# see if control-pane is ready 
kubectl get nodes

Service resources

Suppose you want to make a network connection to a Pod (such as our example application). How do you do that? You could find out the Pod's IP address and connect directly to that address and the app's port number. But the IP address may change when the Pod is restarted, so you'll have to keep looking it up to make sure it's up to date.

Worse, there may be multiple replicas of the Pod, each with different addresses. Every other application which needs to contact the Pod would have to maintain a list of those addresses, which doesn't sound like a great idea.

Fortunately, there's a better way: a Service resource gives you a single, unchanging IP address or DNS name which will be automatically routed to any matching Pod.

Here's the YAML manifest of the Service for our demo app:

apiVersion: v1
kind: Service
metadata:
  name: demo
  labels:
    app: demo
spec:
  ports:
  - port: 8888
    protocol: TCP
    targetPort: 8888
  selector:
    app: demo
  type: ClusterIP
You can see that it looks somewhat similar to the Deployment resource we showed earlier. However, the kind is Service, instead of Deployment, and the spec just includes a list of ports, plus a selector and a type.


#apply the manifest

kubectl apply -f service.yaml

kubectl port-forward service/demo 9999:8888

error: timed out waiting for the condition

solution:

kubectl get pods
No resources found in default namespace.

k8s % kubectl apply -f .

deployment.apps/demo created
service/demo unchanged


k8s % kubectl get pods  

NAME                    READY   STATUS    RESTARTS   AGE
demo-858bd446c4-n5pzm   1/1     Running   0          5s


kubectl port-forward service/demo 9999:8888

Forwarding from 127.0.0.1:9999 -> 8888
Forwarding from [::1]:9999 -> 8888

Means:
In your earlier docker run command, you were just mapping one port to one process. Here, if Pod A crashes, the Serviceis smart enough to immediately send your port-forward traffic to Pod B or Pod C without you even noticing.

http://localhost:9999/

clean up:

kubectl delete -f k8s/

