

部署密钥 和杉支付一样复用联动 deploy-key  flux-source-git-umfpaydeploykey

### rbac授权：

#### zhongzf-dev-rbac.yaml
```
---
apiVersion: v1
kind: ServiceAccount
metadata:
  namespace: zhongzf-dev
  name: service-discovery-account
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: zhongzf-dev
  name: service-discovery-role
rules:
- apiGroups: ["", "extensions", "apps"] # "" indicates the core API group
  resources: ["configmaps", "pods", "services", "endpoints", "secrets"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: zhongzf-dev
  name: service-discovery-binding
subjects:
- kind: ServiceAccount
  name: service-discovery-account
  apiGroup: ""
roleRef:
  kind: Role
  name: service-discovery-role
  apiGroup: ""


```
#### zhongzf-test-rbac.yaml
```
---
apiVersion: v1
kind: ServiceAccount
metadata:
  namespace: zhongzf-test
  name: service-discovery-account
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: zhongzf-test
  name: service-discovery-role
rules:
- apiGroups: ["", "extensions", "apps"] # "" indicates the core API group
  resources: ["configmaps", "pods", "services", "endpoints", "secrets"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: zhongzf-test
  name: service-discovery-binding
subjects:
- kind: ServiceAccount
  name: service-discovery-account
  apiGroup: ""
roleRef:
  kind: Role
  name: service-discovery-role
  apiGroup: ""


```
