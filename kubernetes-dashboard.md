### 创建

wget  https:\/\/raw.githubusercontent.com\/kubernetes\/dashboard\/v2.0.0-beta6\/aio\/deploy\/recommended.yaml

### 修改

kind: Service

apiVersion: v1

metadata:

labels:

k8s-app: kubernetes-dashboard

name: kubernetes-dashboard

namespace: kubernetes-dashboard

spec:

type: NodePort      \# 改成NodePort

ports:

* port: 443

  targetPort: 8443

  nodePort: 31001   \# 指定nodePort端口

  selector:

  k8s-app: kubernetes-dashboard


### 创建

kubectl apply -f   recommended.yaml

### 获取token

kubectl -n kube-system describe secret $\(kubectl -n kube-system get secret \| grep aks-dashboard-admin \| awk '{print $1}'\)

### 访问

https:\/\/masterIp: nodePort（谷歌浏览器不能访问）

### 创建完整权限用户

