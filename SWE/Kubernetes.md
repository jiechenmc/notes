You can access the **ClusterIP** of the service directly! It's not an interface on the host nodes but kube-proxy will automatically forward the packets to one of the pods in its service. Kube-proxy will use IPTables to accomplish this.

You can access **Pod IPs** directly too. However, it is an interface on the host nodes.

You can also resolve curl http://monitor-nx-monitor-kube-pr-prometheus.monitor.svc.cluster.local:9090 by using the dns server in the cluster (reference its cluster IP).

Related Talk: https://www.youtube.com/watch?v=cUGXu2tiZMc