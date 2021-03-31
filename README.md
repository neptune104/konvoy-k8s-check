# konvoy-k8s-check



## 각 kube-scheduler check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=110.45.156.165 -l 'component in (kube-scheduler)' -o jsonpath={.items[0].status.phase}

##각  kube-apiserver check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=110.45.156.165 -l 'component in (kube-apiserver)' -o jsonpath={.items[0].status.phase}

## 각 kube-controller-manager check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=110.45.156.165 -l 'component in (kube-controller-manager)' -o jsonpath={.items[0].status.phase}

## 각 서버별 calico check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<노드 아이피> -l 'k8s-app in (calico-node, calico-route-reflector)' -o jsonpath={.items[0].status.phase}

###각 서버별 kube-proxy check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<노드 아이피> -l 'k8s-app in (kube-proxy)' -o jsonpath={.items[0].status.phase}

###각 서버별 coredns check (개수)
kubectl --kubeconfig /etc/kubernetes/admin.conf get deploy coredns -n kube-system -o jsonpath={.status.availableReplicas}

###노드 정보
kubectl --kubeconfig /etc/kubernetes/admin.conf get nodes -o wide
