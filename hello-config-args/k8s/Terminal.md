201~200~Config-args


1. What you can learn (The 3 Key Concepts)

The ConfigMap (The "Settings" File)

Think of a ConfigMap as a .env file or a settings menu. By keeping the greeting Salut here, you can change the app's behavior without ever having to rebuild the Docker image.

Environment Variable Injection

In the env: section, you aren't just typing a value. You are telling Kubernetes: "Go look at the ConfigMap named demo-config, find the key greeting, and put whatever is inside it into a variable called GREETING."

Arguments with Variables ($(GREETING))

The args: section shows how to pass those variables into your application's startup command. The syntax $(GREETING)is special—it tells Kubernetes to swap that placeholder for the actual value of the environment variable before the app starts.



kubectl get configmap demo-config -o yaml

apiVersion: v1
data:
  greeting: Salut
  kind: ConfigMap
  metadata:
    annotations:
        kubectl.kubernetes.io/last-applied-configuration: |
              {"apiVersion":"v1","data":{"greeting":"Salut"},"kind":"ConfigMap","metadata":{"annotations":{},"name":"demo-config","namespace":"default"}}
                creationTimestamp: "2026-03-18T17:00:12Z"
                  name: demo-config
                    namespace: default
                      resourceVersion: "598"
                        uid: 4d8374ff-e2b1-4e12-b863-31281b89afd3


                        and then you can edit:

                        edit configmap demo-config
                        configmap/demo-config edited

                        Update:

                        kubectl rollout restart deployment demo
                        deployment.apps/demo restarted

                        Rollback:

                        kubectl rollout history deployment demo

                        deployment.apps/demo 
                        REVISION  CHANGE-CAUSE
                        1         <none>
                        2         <none>

                        kubectl rollout history deployment demo --revision=1 
                        deployment.apps/demo with revision #1
                        Pod Template:
                          Labels:	app=demo
                          	pod-template-hash=5c68b54bb8
                          	  Containers:
                          	     demo:
                          	         Image:	cloudnatived/demo:hello-config-args
                          	             Port:	8888/TCP
                          	                 Host Port:	0/TCP
                          	                     Args:
                          	                           -greeting
                          	                                 $(GREETING)
                          	                                     Environment:
                          	                                           GREETING:	<set to the key 'greeting' of config map 'demo-config'>	Optional: false
                          	                                               Mounts:	<none>
                          	                                                 Volumes:	<none>
                          	                                                   Node-Selectors:	<none>
                          	                                                     Tolerations:	<none>

                          	                                                     Check expected in ConfigMap (cm) value:
                          	                                                     kubectl get cm demo-config -o jsonpath='{.data.greeting}'
                          	                                                     Salut%  
