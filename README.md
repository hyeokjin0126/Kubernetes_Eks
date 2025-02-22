```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
  name: <클러스터 이름>
  region: <리전>
  version: "<클러스터 버전>"
cloudWatch:
  clusterLogging:
    enableTypes: ["*"]
iam:
  withOIDC: true
  serviceAccounts:
  - metadata:
      name: aws-load-balancer-controller
      namespace: kube-system
    wellKnownPolicies:
      awsLoadBalancerController: true
addons:
- name: vpc-cni
  version: latest
- name: coredns
  version: latest
- name: kube-proxy
  version: latest
vpc:
  id: <VPC 아이디>
  subnets:
    public:
      ap-northeast-2a-pub: { id: <서브넷 아이디> }
      ap-northeast-2b-pub: { id: <서브넷 아이디> }
    private:
      ap-northeast-2a-priv: { id: <서브넷 아이디> }
      ap-northeast-2b-priv: { id: <서브넷 아이디> }
managedNodeGroups:
  - name: <노드그룹 이름>
    labels: { key: value }
    instanceName: <노드 이름>
    instanceType: <노드 인스턴스 타입>
    minSize: 2
    maxSize: 2
    desiredCapacity: 2
    privateNetworking: true
    subnets:
     - ap-northeast-2a-priv
     - ap-northeast-2b-priv
    iam:
      withAddonPolicies:
        imageBuilder: true
        autoScaler: true
        awsLoadBalancerController: true
        cloudWatch: true
```

```
eksctl create cluster -f cluster.yaml
```
