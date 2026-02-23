# SCTASK0032608 [개발][Observability SaaS] AKS Node 스펙 변경 요청
요청사항
현재: Standard_F4s_v2 사양으로  5/5, maxPods 250  (현재 노드 메모리 Pressure 상태)
변경: B4as_v2 사양으로 2/3, maxPods110 (사용자요청)
---------------------------------------------------------------------------------------------------------------------
[AS-IS]
userpool01
Count: min5/max5 (CA 활성화)
Standard F4s v2 (4 vcpus, 8 GiB memory)
Availability zones: Zone 1, Zone 2, Zone 3

[TO-BE]
userpool
Count: min2/max3 (CA 활성화)
SKU: Standard B4as_v2 (4 vcpus, 16 GiB memory) 
Availability zones: Zone 1, Zone 2, Zone 3

# 사전 작업
1. 기존 노드풀(userpool01) 정보 백업
$ az aks nodepool show --resource-group $RESOURCE_GROUP _NAME --cluster-name $CLUSTER_NAME --name $NODEPOOL_NAME

az aks nodepool add `
   --resource-group $RESOURCE_GROUP_NAME `
   --cluster-name $CLUSTER_NAME `
   --name $NODE_POOL_NAME `
   --mode $NODE_POOL_MODE `
   --node-vm-size $VM_SKU `
   --node-count $NODE_COUNT `
   --max-pods $MAX_PODS `
   --os-sku $OS_SKU `
   --enable-cluster-autoscaler `
   --min-count $MIN_SIZE `
   --max-count $MAX_SIZE `
   --node-osdisk-type $NODE_DISK_TYPE `
   --node-osdisk-size $NODE_DISK_SIZE `
   --enable-encryption-at-host `
   --zones 1 2 3

# 본 작업
1. 신규 노드풀(userpool) 생성

2. 기존 노드풀(userpool01) Stop

3. 전체 pod 상태점검

4. 기존 노드풀(userpool01) 삭제

