# konvoy-k8s-check

## Ansible command

ansible-playbook check-kubernetes.yaml -i /root/konvoy-deploy/konvoy_v1.6.0/inventory.yaml --extra-vars '{"image_registries_with_auth":[],"default_image_registry":"","default_image_registry_mirrors":{},"provisioner":"","minimum_inclusive_kubernetes_version":"1.16.0","maximum_exclusive_kubernetes_version":"1.19.0"}' --extra-vars @/root/konvoy-deploy/konvoy_v1.6.0/cluster.yaml


## kube-scheduler check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<master ip> -l 'component in (kube-scheduler)' -o jsonpath={.items[0].status.phase}

## kube-apiserver check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<master ip> -l 'component in (kube-apiserver)' -o jsonpath={.items[0].status.phase}

## kube-controller-manager check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<master ip> -l 'component in (kube-controller-manager)' -o jsonpath={.items[0].status.phase}

## calico check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<node ip> -l 'k8s-app in (calico-node, calico-route-reflector)' -o jsonpath={.items[0].status.phase}

## kube-proxy check (running or error)
kubectl --kubeconfig /etc/kubernetes/admin.conf get pods -n kube-system --field-selector status.podIP=<node ip> -l 'k8s-app in (kube-proxy)' -o jsonpath={.items[0].status.phase}

## coredns check (개수)
kubectl --kubeconfig /etc/kubernetes/admin.conf get deploy coredns -n kube-system -o jsonpath={.status.availableReplicas}

## 노드 정보
kubectl --kubeconfig /etc/kubernetes/admin.conf get nodes -o wide

