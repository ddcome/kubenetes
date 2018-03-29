# kubenetes

## 1.网络策略
### 1.1.禁止所有pod之间的通信

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
spec:
  podSelector: {}
  policyTypes:
  - Ingress

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-all
spec:
  podSelector: {}
  ingress:
  - {}
```  

## 网络策略实例

### denyall
```
[*** ~]$ kubectl get networkpolicy np-denyall-zhongyaozhiji -n zhongyaozhiji -o yaml
apiVersion: extensions/v1beta1
kind: NetworkPolicy
metadata:
  creationTimestamp: 2018-03-29T04:53:35Z
  generation: 1
  name: np-denyall-zhongyaozhiji
  namespace: zhongyaozhiji
  resourceVersion: "26581594"
  selfLink: /apis/extensions/v1beta1/namespaces/zhongyaozhiji/networkpolicies/np-denyall-zhongyaozhiji
  uid: 23970025-330d-11e8-ab71-6c92bf21ade4
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

### allowself
```
[*** ~]$ kubectl get networkpolicy np-allowself-zhongyaozhiji -n zhongyaozhiji -o yaml
apiVersion: extensions/v1beta1
kind: NetworkPolicy
metadata:
  creationTimestamp: 2018-03-29T04:53:36Z
  generation: 1
  name: np-allowself-zhongyaozhiji
  namespace: zhongyaozhiji
  resourceVersion: "26581596"
  selfLink: /apis/extensions/v1beta1/namespaces/zhongyaozhiji/networkpolicies/np-allowself-zhongyaozhiji
  uid: 23d54a80-330d-11e8-ab71-6c92bf21ade4
spec:
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          namespace: zhongyaozhiji
  podSelector: {}
  policyTypes:
  - Ingress
```

### allowsomeone
```
[*** ~]$ kubectl get networkpolicy allow-extra-ip-zhongyaozhijiextra-ip-default -n zhongyaozhiji -o yaml
apiVersion: extensions/v1beta1
kind: NetworkPolicy
metadata:
  creationTimestamp: 2018-03-29T04:53:36Z
  generation: 1
  name: allow-extra-ip-zhongyaozhijiextra-ip-default
  namespace: zhongyaozhiji
  resourceVersion: "26581597"
  selfLink: /apis/extensions/v1beta1/namespaces/zhongyaozhiji/networkpolicies/allow-extra-ip-zhongyaozhijiextra-ip-default
  uid: 23e969a8-330d-11e8-ab71-6c92bf21ade4
spec:
  ingress:
  - from:
    - ipBlock:
        cidr: 0.0.0.0/0
  podSelector: {}
  policyTypes:
  - Ingress
```
