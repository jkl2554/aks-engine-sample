[aks-engine sample]
https://github.com/Azure/aks-engine/blob/master/docs/tutorials/quickstart.md

[api model(cluster definitions)]
https://github.com/Azure/aks-engine/blob/master/docs/topics/clusterdefinitions.md  
  
aks engine 설치
```
//windows chocolatey 설치필요.
choco install aks-engine
```


sample aks-engine api-model(kubernets.json)
``` 
{
  "apiVersion": "vlabs",
  "properties": {
    "masterProfile": {
      "count": 1,
      "dnsPrefix": "",
      "vmSize": "Standard_D2_v3"
    },
    "agentPoolProfiles": [
      {
        "name": "agentpool1",
        "count": 2,
        "vmSize": "Standard_D2_v3"
      }
    ],
    "linuxProfile": {
      "adminUsername": "azureuser",
      "ssh": {
        "publicKeys": [
          {
            "keyData": ""
          }
        ]
      }
    }
  }
}
```
deploy 
```
aks-engine deploy --resource-group <resource group name> \
         --location koreacentral \
         --api-model .\kubernetes.json \
         --dns-prefix <prefix name>
```
Connect
`_output/<prefix name>`폴더

![image.png](/images/Items.png)

kubeconfig 설정
```
//for windows powershell
$env:KUBECONFIG="./_output/<prefix name>/kubeconfig/kubeconfig.koreacentral.json"
//for linux shell script
export KUBECONFIG="./_output/<prefix name>/kubeconfig/kubeconfig.koreacentral.json"
//연결 확인
kubectl get nodes
//example output
//NAME                                 STATUS   ROLES    AGE   VERSION
//k8s-agentpool1-33557086-vmss000000   Ready    agent    15m   v1.18.16
//k8s-agentpool1-33557086-vmss000001   Ready    agent    15m   v1.18.16
//k8s-master-33557086-0                Ready    master   15m   v1.18.16
```
