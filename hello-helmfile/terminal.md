201~200~Helmfile

it’s own thing: 


helmfile version

▓▓▓ helmfile

  Version            v1.4.2
    Git Commit         "brew"
      Build Date         14 Mar 26 01:44 CET (4 days ago)
        Commit Date        14 Mar 26 01:44 CET (4 days ago)
          Dirty Build        no
            Go version         1.26.1
              Compiler           gc
                Platform           darwin/arm64


                hello-helmfile % helm plugin install https://github.com/databus23/helm-diff --verify=false
                WARNING: Skipping plugin signature verification
                Downloading https://github.com/databus23/helm-diff/releases/latest/download/helm-diff-macos-arm64.tgz
                Preparing to install into /Users/danieljari/Library/helm/plugins/helm-diff
                Installed plugin: diff

                Helmfile apply

                Listing releases matching ^prometheus$
                prometheus	prometheus	1       	2026-03-18 13:03:10.196779 +0100 CET	deployed	prometheus-28.13.03v3.10.0    


                What Is Prometheus?

                Prometheus is a monitoring and alerting system designed for cloud-native environments, especially Kubernetes.

                It collects metrics (numerical time-series data) from applications and infrastructure, stores them, and allows you to:

                 Query performance data

                 Create alerts

                 Visualize system health

                  Debug issues

                  It is one of the most common monitoring tools in Kubernetes environments.



                  shows pods in every namespace in the cluster.

                  get pods -A
                  shows services in every namespace in the cluster.
                  kubectl get svc -A

                  kubectl port-forward -n prometheus svc/prometheus-server 9090:80



                  http://localhost:9090

                  
