```bash

$ minikube start \
--image-mirror-country='cn' \
--driver='hyperkit' \
--memory='4g' \
--logtostderr \
--iso-url=https://github.com/kubernetes/minikube/releases/download/v1.32.0/minikube-v1.32.0-amd64.iso

$ helm repo add chaos-mesh https://charts.chaos-mesh.org

$ helm search repo chaos-mesh

# download chaos-mesh chart
$ helm pull chaos-mesh/chaos-mesh

# Default to /var/run/docker.sock
$ helm install \
chaos-mesh \
chaos-mesh/chaos-mesh \
-n=chaos-mesh \
--version 2.6.3 \
--debug \
--dry-run

$ helm install \
chaos-mesh \
./chaos-mesh \
-n=chaos-mesh \
--version 2.6.3 \
--debug \
--dry-run

## CRD
awschaos.chaos-mesh.org
azurechaos.chaos-mesh.org
blockchaos.chaos-mesh.org
dnschaos.chaos-mesh.org
gcpchaos.chaos-mesh.org
httpchaos.chaos-mesh.org
iochaos.chaos-mesh.org
jvmchaos.chaos-mesh.org
kernelchaos.chaos-mesh.org
networkchaos.chaos-mesh.org
physicalmachinechaos.chaos-mesh.org
podchaos.chaos-mesh.org
podhttpchaos.chaos-mesh.org
podiochaos.chaos-mesh.org
podnetworkchaos.chaos-mesh.org
stresschaos.chaos-mesh.org
timechaos.chaos-mesh.org

physicalmachines.chaos-mesh.org
remoteclusters.chaos-mesh.org
schedules.chaos-mesh.org
statuschecks.chaos-mesh.org
workflownodes.chaos-mesh.org
workflows.chaos-mesh.org

$ kubectl -n chaos-mesh get pods
NAME                                        READY   STATUS    RESTARTS   AGE
chaos-controller-manager-7dd77cdfc4-22c9p   1/1     Running   0          5m55s
chaos-controller-manager-7dd77cdfc4-4xsl6   1/1     Running   0          5m55s
chaos-controller-manager-7dd77cdfc4-xtb2q   1/1     Running   0          5m55s
chaos-daemon-vz5vq                          1/1     Running   0          5m55s
chaos-dashboard-54c7d9d-9845q               1/1     Running   0          5m55s
chaos-dns-server-6d777f574f-j5rdt           1/1     Running   0          5m55s

$ kubectl -n chaos-mesh get services
NAME                            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                                 AGE
chaos-daemon                    ClusterIP   None            <none>        31767/TCP,31766/TCP                     6m3s
chaos-dashboard                 NodePort    10.99.11.108    <none>        2333:31266/TCP,2334:31587/TCP           6m3s
chaos-mesh-controller-manager   ClusterIP   10.97.131.110   <none>        443/TCP,10081/TCP,10082/TCP,10080/TCP   6m3s
chaos-mesh-dns-server           ClusterIP   10.101.78.188   <none>        53/UDP,53/TCP,9153/TCP,9288/TCP         6m3s
$

$ kubectl -n chaos-mesh get services chaos-dashboard -o yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    meta.helm.sh/release-name: chaos-mesh
    meta.helm.sh/release-namespace: chaos-mesh
    prometheus.io/port: "2334"
    prometheus.io/scrape: "true"
  creationTimestamp: "2024-03-12T08:53:47Z"
  labels:
    app.kubernetes.io/component: chaos-dashboard
    app.kubernetes.io/instance: chaos-mesh
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: chaos-mesh
    helm.sh/chart: chaos-mesh-2.6.3
  name: chaos-dashboard
  namespace: chaos-mesh
  resourceVersion: "535"
  uid: a3dd535a-54cc-42e0-9cef-5a39b5454bf2
spec:
  clusterIP: 10.99.11.108
  clusterIPs:
  - 10.99.11.108
  externalTrafficPolicy: Cluster
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - name: http
    nodePort: 31266
    port: 2333
    protocol: TCP
    targetPort: 2333
  - name: metric
    nodePort: 31587
    port: 2334
    protocol: TCP
    targetPort: 2334
  selector:
    app.kubernetes.io/component: chaos-dashboard
    app.kubernetes.io/instance: chaos-mesh
    app.kubernetes.io/name: chaos-mesh
  sessionAffinity: None
  type: NodePort
status:
  loadBalancer: {}
$

$ minikube ip
192.168.73.144
$

http://192.168.73.144:31266

http://192.168.73.144:31587/metrics


```

