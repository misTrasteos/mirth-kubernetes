# Context
PoC about running NextGen Connect (formerly Mirth Connect) inside a Kubernetes Cluster

## How to
```
kubectl apply -f deployment.yaml
```
```
kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
mirth-deployment-74f6df559d-kzkjj   1/1     Running   0          108s
```

```bash
kubectl logs -f mirth-deployment-74f6df559d-kzkjj
```
```log
INFO  2021-05-03 14:57:01,058 [Main Server Thread] com.mirth.connect.server.Mirth: Mirth Connect 3.11.0 (Built on April 6, 2021) server successfully started.
INFO  2021-05-03 14:57:01,062 [Main Server Thread] com.mirth.connect.server.Mirth: This product was developed by NextGen Healthcare (https://www.nextgen.com) and its contributors (c)2005-2021.
INFO  2021-05-03 14:57:01,064 [Main Server Thread] com.mirth.connect.server.Mirth: Running OpenJDK 64-Bit Server VM 11.0.11 on Linux (4.19.128-microsoft-standard, amd64), derby, with charset UTF-8.
INFO  2021-05-03 14:57:01,065 [Main Server Thread] com.mirth.connect.server.Mirth: Web server running at http://10.244.0.8:8080/ and https://10.244.0.8:8443/
```

```
kubectl port-forward mirth-deployment-74f6df559d-kzkjj 8443
```
After this port-forwarding we will be able to connect to Mirth Connect Dashboard using Mirth Connect Administrator Launcher.

# Links

* [NextGen Connect Integration Engine](https://www.nextgen.com/products-and-services/integration-engine)
* [NextGen Connect Integration Engine Downloads](https://www.nextgen.com/products-and-services/nextgen-connect-integration-engine-downloads)
* [NextGen Docker hub](https://hub.docker.com/r/nextgenhealthcare/connect)

# TODO
* This is not a very usable Mirth instance, as it will lose all its channels when the pod is restarted.
    * `StatefulSet`, `Persistent Volumes`, or connection to a MySQL instance is needed.
* Secrets for mysql password    