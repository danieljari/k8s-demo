201~200~Helm 3.0 

Updated Helm:

Helm version
v4.1.3


ls k8s/demo
Chart.yaml             prod-values.yaml staging-values.yaml    templates
values.yaml

Clean up using: 
kubectl delete all --selector app=demo
No resource found

helm install demo ./k8s/demo

NAME: demo
LAST DEPLOYED: Wed Mar 18 12:15:59 2026
NAMESPACE: default
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
TEST SUITE: None


describe deployment is looking at the Blueprints and the Manager, while describe pod is looking at a Specific Worker on the site.

kubectl get pods

NAME                   READY   STATUS    RESTARTS   AGE
demo-9987d94f6-tmm5x   1/1     Running   0          9m47s

kubectl get deploy

NAME   READY   UP-TO-DATE   AVAILABLE   AGE
demo   1/1     1            1           10m


kubectl describe pod demo-9987d94f6-tmm5x  

Events:
  Type    Reason     Age   From               Message
    ----    ------     ----  ----               -------
      Normal  Scheduled  11m   default-scheduler  Successfully assigned default/demo-9987d94f6-tmm5x to minikube
        Normal  Pulled     11m   kubelet            spec.containers{demo}: Container image "cloudnatived/demo:hello" already present on machine and can be accessed by the pod
          Normal  Created    11m   kubelet            spec.containers{demo}: Container created
            Normal  Started    11m   kubelet            spec.containers{demo}: Container started

            kubectl describe deploy demo


            Name:                   demo
            Namespace:              default
            CreationTimestamp:      Wed, 18 Mar 2026 12:15:59 +0100
            Labels:                 app.kubernetes.io/managed-by=Helm
            Annotations:            deployment.kubernetes.io/revision: 1
                                    meta.helm.sh/release-name: demo
                                                            meta.helm.sh/release-namespace: default
                                                            Selector:               app=demo
                                                            Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
                                                            StrategyType:           RollingUpdate
                                                            MinReadySeconds:        0
                                                            RollingUpdateStrategy:  25% max unavailable, 25% max surge
                                                            Pod Template:
                                                              Labels:  app=demo
                                                                         environment=development
                                                                           Containers:
                                                                              demo:
                                                                                  Image:      cloudnatived/demo:hello
                                                                                      Port:       8888/TCP
                                                                                          Host Port:  0/TCP
                                                                                              Environment:
                                                                                                    environment:  development
                                                                                                        Mounts:         <none>
                                                                                                          Volumes:          <none>
                                                                                                            Node-Selectors:   <none>
                                                                                                              Tolerations:      <none>
                                                                                                              Conditions:
                                                                                                                Type           Status  Reason
                                                                                                                  ----           ------  ------
                                                                                                                    Available      True    MinimumReplicasAvailable
                                                                                                                      Progressing    True    NewReplicaSetAvailable
                                                                                                                      OldReplicaSets:  <none>
                                                                                                                      NewReplicaSet:   demo-9987d94f6 (1/1 replicas created)
                                                                                                                      Events:
                                                                                                                        Type    Reason             Age   From                   Message
                                                                                                                          ----    ------             ----  ----                   -------
                                                                                                                            Normal  ScalingReplicaSet  13m   deployment-controller  Scaled up replica set demo-9987d94f6 from 0 to 1
