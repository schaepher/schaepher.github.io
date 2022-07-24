
要先有以下镜像才能开启 k8s：

REPOSITORY                                                       TAG                                              IMAGE ID            CREATED             SIZE
docker/desktop-storage-provisioner                               v1.1                                             e704287ce753        4 months ago        41.8MB
docker/desktop-vpnkit-controller                                 v1.0                                             79da37e5a3aa        5 months ago        36.6MB
docker/desktop-kubernetes                                        kubernetes-v1.16.5-cni-v0.7.5-critools-v1.15.0   a86647f0b376        6 months ago        279MB
k8s.gcr.io/kube-apiserver                                        v1.16.5                                          fc838b21afbb        6 months ago        159MB
k8s.gcr.io/kube-proxy                                            v1.16.5                                          0ee1b8a3ebe0        6 months ago        82.7MB
k8s.gcr.io/kube-controller-manager                               v1.16.5                                          441835dd2301        6 months ago        151MB
k8s.gcr.io/kube-scheduler                                        v1.16.5                                          b4d073a9efda        6 months ago        83.5MB
docker/kube-compose-controller                                   v0.4.25-alpha1                                   129151cdf35f        9 months ago        35.6MB
docker/kube-compose-api-server                                   v0.4.25-alpha1                                   989749268895        9 months ago        50.7MB
docker/kube-compose-installer                                    v0.4.25-alpha1                                   2a71ac5a1359        9 months ago        42.3MB
quay.io/kubernetes-ingress-controller/nginx-ingress-controller   0.26.1                                           29024c9c6e70        10 months ago       483MB
k8s.gcr.io/etcd                                                  3.3.15-0                                         b2756210eeab        11 months ago       247MB
k8s.gcr.io/coredns                                               1.6.2                                            bf261d157914        11 months ago       44.1MB
k8s.gcr.io/pause                                                 3.1                                              da86e6ba6ca1        2 years ago         742kB