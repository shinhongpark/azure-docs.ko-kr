---
title: 일반적인 Azure Kubernetes Service 문제 해결
description: AKS(Azure Kubernetes Service)를 사용 할 때 발생하는 일반적인 문제를 해결하는 방법을 알아봅니다.
services: container-service
ms.topic: troubleshooting
ms.date: 06/20/2020
ms.openlocfilehash: 02ff1581bafe62a092be87d16df51c7ca8c020b4
ms.sourcegitcommit: beacda0b2b4b3a415b16ac2f58ddfb03dd1a04cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2020
ms.locfileid: "97830941"
---
# <a name="aks-troubleshooting"></a>AKS 문제 해결

AKS(Azure Kubernetes Service) 클러스터를 만들거나 관리할 때 경우에 따라 문제가 발생할 수도 있습니다. 이 문서에서는 몇 가지 일반적인 문제 및 문제 해결 단계를 자세히 설명합니다.

## <a name="in-general-where-do-i-find-information-about-debugging-kubernetes-problems"></a>일반적으로 Kubernetes 문제 디버깅에 대한 정보는 어디에서 찾나요?

[Kubernetes 클러스터 문제 해결에 대한 공식 가이드](https://kubernetes.io/docs/tasks/debug-application-cluster/troubleshooting/)를 검색합니다.
pod, 노드, 클러스터 등의 문제 해결과 관련해서 Microsoft 엔지니어가 게시한 [문제 해결 가이드](https://github.com/feiskyer/kubernetes-handbook/blob/master/en/troubleshooting/index.md)도 있습니다.

## <a name="im-getting-a-quota-exceeded-error-during-creation-or-upgrade-what-should-i-do"></a>만들기 또는 업그레이드 동안 "할당량 초과" 오류가 발생합니다. 어떻게 해야 하나요? 

 [더 많은 코어를 요청합니다](../azure-portal/supportability/resource-manager-core-quotas-request.md).

## <a name="im-getting-an-insufficientsubnetsize-error-while-deploying-an-aks-cluster-with-advanced-networking-what-should-i-do"></a>고급 네트워킹을 사용하여 AKS 클러스터를 배포하는 동안 insufficientSubnetSize 오류가 발생합니다. 어떻게 해야 하나요?

이 오류는 리소스를 성공적으로 할당 하기 위해 클러스터에 사용 중인 서브넷의 CIDR 내에 더 이상 사용 가능한 Ip가 없음을 나타냅니다. Kubenet 클러스터의 경우 클러스터의 각 노드에 대 한 충분 한 IP 공간이 요구 사항에 해당 합니다. Azure CNI 클러스터의 경우 클러스터의 각 노드 및 pod에 대해 충분 한 IP 공간이 필요 합니다.
[Pod에 ip를 할당 하려면 Azure CNI 디자인](configure-azure-cni.md#plan-ip-addressing-for-your-cluster)에 대해 자세히 알아보세요.

이러한 오류는 [AKS 진단](concepts-diagnostics.md)에도 표시 되며, 이러한 오류는 서브넷 크기 부족 등의 문제를 사전에 노출 합니다.

다음 3 개의 사례는 서브넷 크기 오류를 초래 합니다.

1. AKS Scale 또는 AKS 노드 풀 크기 조정
   1. Kubenet를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of new nodes requested` .
   1. Azure CNI를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of nodes requested times (*) the node pool's --max-pod value` .

1. AKS Upgrade 또는 AKS 노드 풀 업그레이드
   1. Kubenet를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of buffer nodes needed to upgrade` .
   1. Azure CNI를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of buffer nodes needed to upgrade times (*) the node pool's --max-pod value` .
   
   기본적으로 AKS 클러스터는 최대 서 수 (업그레이드 버퍼) 값을 1로 설정 하지만이 업그레이드 동작은 노드 풀의 최대 서 수 값을 설정 하 여 사용자 지정할 수 있습니다. 그러면 업그레이드를 완료 하는 데 필요한 사용 가능한 Ip 수가 증가 합니다.

1. AKS create 또는 AKS 노드 풀 추가
   1. Kubenet를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of nodes requested for the node pool` .
   1. Azure CNI를 사용 하는 경우 `number of free IPs in the subnet` 이 **보다 작은** 경우입니다 `number of nodes requested times (*) the node pool's --max-pod value` .

새 서브넷을 만들어 다음 완화 방법을 수행할 수 있습니다. 새 서브넷을 만들 수 있는 권한은 기존 서브넷의 CIDR 범위를 업데이트할 수 없기 때문에 완화에 필요 합니다.

1. 작업 목표를 위해 더 큰 CIDR 범위를 사용 하 여 새 서브넷을 다시 작성 합니다.
   1. 원하는 겹치지 않는 새 범위를 사용 하 여 새 서브넷을 만듭니다.
   1. 새 서브넷에 새 노드 풀을 만듭니다.
   1. 이전 서브넷에 있는 이전 노드 풀에서 pod을 드레이닝 합니다.
   1. 이전 서브넷 및 이전 노드 풀을 삭제 합니다.

## <a name="my-pod-is-stuck-in-crashloopbackoff-mode-what-should-i-do"></a>내 Pod가 CrashLoopBackOff 모드에서 중단됩니다. 어떻게 해야 하나요?

Pod가 해당 모드에서 중단되는 이유는 다양할 수 있습니다. 다음을 확인할 수 있습니다.

* `kubectl describe pod <pod-name>`를 사용하여 pod 자체
* `kubectl logs <pod-name>`을 사용하여 로그

Pod 문제를 해결하는 방법에 대한 자세한 내용은 [애플리케이션 디버그](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/#debugging-pods)를 참조하세요.

## <a name="im-receiving-tcp-timeouts-when-using-kubectl-or-other-third-party-tools-connecting-to-the-api-server"></a>`TCP timeouts` `kubectl` API 서버에 연결 하는 또는 기타 타사 도구를 사용 하는 경우를 받고 있습니다.
AKS에는 Slo (서비스 수준 목표) 및 Sla (서비스 수준 계약)를 보장 하기 위해 코어 수에 따라 수직으로 확장 되는 HA 제어 평면이 있습니다. 연결 시간이 초과 되는 경우 아래를 확인 합니다.

- **모든 API 명령이 지속적으로 시간 초과 됩니까?** 매우 적은 경우에는 `tunnelfront` `aks-link` 노드 > 제어 평면 통신을 담당 하는 pod 또는 pod가 실행 중인 상태가 아닐 수 있습니다. 이 pod를 호스트 하는 노드가 과도 하 게 사용 되거나 스트레스 상태에 있지 않은지 확인 합니다. 자신의 [ `system` 노드 풀](use-system-pools.md)로 이동 하는 것이 좋습니다.
- **[AKS 수신 트래픽 제한 문서](limit-egress-traffic.md)에 명시 된 모든 필수 포트, Fqdn 및 ip를 열었습니다.** 그렇지 않으면 여러 명령 호출이 실패할 수 있습니다.
- **현재 IP에 [API Ip 권한 부여 범위가](api-server-authorized-ip-ranges.md)적용 되나요?** 이 기능을 사용 하는 경우 IP가 호출 차단 되는 범위에 포함 되지 않습니다. 
- **클라이언트 또는 응용 프로그램이 API 서버에 대 한 호출을 누수 하나요?** 자주 get 호출 대신 watch를 사용 해야 하며 타사 응용 프로그램이 이러한 호출을 누출 하지 않도록 합니다. 예를 들어 Istio 믹서의 버그로 인해 내부적으로 비밀을 읽을 때마다 새 API 서버 감시 연결이 생성 됩니다. 이 동작은 정기적으로 발생 하므로 감시 연결을 신속 하 게 누적 하 고 결과적으로 API 서버가 크기 조정 패턴에 관계 없이 오버 로드 됩니다. https://github.com/istio/istio/issues/19481
- **투구 배포에 많은 릴리스가 있나요?** 이 시나리오를 사용 하면 tiller는 노드에서 너무 많은 메모리를 사용 하 고 많은 양의를 사용 하 여 `configmaps` API 서버에서 불필요 한 급증을 일으킬 수 있습니다. `--history-max`에서을 구성 `helm init` 하 고 새 투구 3을 활용 하는 것이 좋습니다. 다음 문제에 대 한 자세한 내용: 
    - https://github.com/helm/helm/issues/4821
    - https://github.com/helm/helm/issues/3500
    - https://github.com/helm/helm/issues/4543
- **[차단 되는 노드 간의 내부 트래픽 입니까?](#im-receiving-tcp-timeouts-such-as-dial-tcp-node_ip10250-io-timeout)**

## <a name="im-receiving-tcp-timeouts-such-as-dial-tcp-node_ip10250-io-timeout"></a>을 (를) 받고 있습니다. `TCP timeouts``dial tcp <Node_IP>:10250: i/o timeout`

이러한 시간 제한은 차단 되는 노드 간의 내부 트래픽과 관련 될 수 있습니다. 클러스터의 노드에 대 한 서브넷의 [네트워크 보안 그룹](concepts-security.md#azure-network-security-groups) 등이 트래픽이 차단 되 고 있지 않은지 확인 합니다.

## <a name="im-trying-to-enable-kubernetes-role-based-access-control-kubernetes-rbac-on-an-existing-cluster-how-can-i-do-that"></a>기존 클러스터에서 Kubernetes (역할 기반 액세스 제어) Kubernetes RBAC (역할 기반 액세스 제어)를 사용 하도록 설정 하려고 합니다. 어떻게 하면 되나요?

기존 클러스터에서 Kubernetes (역할 기반 액세스 제어) Kubernetes RBAC (역할 기반 액세스 제어)를 사용 하도록 설정할 수 없습니다. 새 클러스터를 만들 때 설정 해야 합니다. Kubernetes RBAC는 CLI, 포털 또는 이후 버전의 API를 사용할 때 기본적으로 사용 하도록 설정 됩니다 `2020-03-01` .

## <a name="i-cant-get-logs-by-using-kubectl-logs-or-i-cant-connect-to-the-api-server-im-getting-error-from-server-error-dialing-backend-dial-tcp-what-should-i-do"></a>kubectl logs를 사용하여 로그를 가져올 수 없고 API 서버에 연결할 수 없습니다. "서버 오류: 백 엔드 전화 접속 오류가 발생했습니다.: dial tcp…"라는 오류가 발생합니다. 어떻게 해야 하나요?

API 서버에 연결하기 위해 22, 9000 및 1194 포트가 열려 있는지 확인합니다. `kubectl get pods --namespace kube-system` 명령을 사용하여 `tunnelfront` 또는 `aks-link` Pod가 *kube-system* 네임스페이스에서 실행되고 있는지 확인합니다. 실행되지 않으면 pod를 강제로 삭제합니다. 그러면 다시 시작됩니다.

## <a name="im-getting-tls-client-offered-only-unsupported-versions-from-my-client-when-connecting-to-aks-api-what-should-i-do"></a>`"tls: client offered only unsupported versions"`AKS API에 연결할 때 내 클라이언트에서 가져옵니다. 어떻게 해야 합니까?

AKS에서 지원 되는 최소 TLS 버전은 TLS 1.2입니다.

## <a name="im-trying-to-upgrade-or-scale-and-am-getting-a-changing-property-imagereference-is-not-allowed-error-how-do-i-fix-this-problem"></a>업그레이드하거나 크기를 조정하려고 하는 중에 `"Changing property 'imageReference' is not allowed"` 오류가 발생했습니다. 이 문제를 어떻게 해결하나요?

AKS 클러스터 내의 에이전트 노드에서 태그를 수정했기 때문에 이 오류가 발생하는 것일 수 있습니다. MC_* 리소스 그룹에서 리소스의 태그 및 다른 속성을 수정하거나 삭제하면 예기치 않은 결과가 발생할 수 있습니다. AKS 클러스터의 MC_* 그룹 아래에서 리소스를 변경하면 SLO(서비스 수준 목표)가 손상됩니다.

## <a name="im-receiving-errors-that-my-cluster-is-in-failed-state-and-upgrading-or-scaling-will-not-work-until-it-is-fixed"></a>클러스터가 실패 상태에 있고 업그레이드 또는 확장이 수정될 때까지 작동하지 않는다는 오류가 표시됩니다.

*이 문제 해결 지원은 https://aka.ms/aks-cluster-failed 에서 제공합니다.*

여러 가지 이유로 클러스터가 실패 상태로 전환되면 이 오류가 발생합니다. 이전에 실패한 작업을 다시 시도하기 전에 다음 단계에 따라 클러스터 실패 상태를 해결합니다.

1. 클러스터가 `failed` 상태를 벗어날 때까지 `upgrade` 및 `scale` 작업은 성공적으로 수행되지 않습니다. 일반적인 근본 문제 및 해결 방법은 다음과 같습니다.
    * **부족한 컴퓨팅(CRP) 할당량** 을 사용하여 크기를 조정합니다. 해결하려면 먼저 클러스터의 크기를 할당량 내에서 안정적인 목표 상태로 다시 조정합니다. 그런 다음, 초기 할당량 한도를 초과하여 다시 강화하려고 시도하기 전에 [다음 단계에 따라 컴퓨팅 할당량을 늘리도록 요청](../azure-portal/supportability/resource-manager-core-quotas-request.md)합니다.
    * 고급 네트워킹 및 **부족한 서브넷(네트워킹) 리소스** 를 사용하여 클러스터 크기를 조정합니다. 해결하려면 먼저 클러스터의 크기를 할당량 내에서 안정적인 목표 상태로 다시 조정합니다. 그런 다음, 초기 할당량 한도를 초과하여 다시 강화하려고 시도하기 전에 [다음 단계에 따라 리소스 할당량을 늘리도록 요청](../azure-resource-manager/templates/error-resource-quota.md#solution)합니다.
2. 업그레이드 실패의 근본 원인이 해결되면 클러스터가 성공 상태여야 합니다. 성공 상태가 확인되면 원래 작업을 다시 시도합니다.

## <a name="im-receiving-errors-when-trying-to-upgrade-or-scale-that-state-my-cluster-is-being-upgraded-or-has-failed-upgrade"></a>내 클러스터를 업그레이드하고 있거나 업그레이드가 실패한 상태에서 업그레이드하거나 크기를 조정하려고 하면 오류가 발생합니다.

*이 문제 해결 지원은 https://aka.ms/aks-pending-upgrade 에서 제공합니다.*

 클러스터 또는 노드 풀은 동시에 업그레이드 및 크기 조정할 수 없습니다. 대신 동일한 리소스에 대한 다음 요청이 수행되기 전에 대상 리소스에서 각 작업 유형이 완료되어야 합니다. 따라서 활성 업그레이드 또는 크기 조정 작업이 발생하거나 시도되는 경우 작업이 제한됩니다. 

문제를 진단하는 데 도움이 되도록 `az aks show -g myResourceGroup -n myAKSCluster -o table`을 실행하여 클러스터의 자세한 상태를 검색합니다. 결과에 따라 다음을 수행합니다.

* 클러스터가 적극적으로 업그레이드되고 있는 경우 작업이 완료될 때까지 기다립니다. 성공하면 이전에 실패한 작업을 다시 시도합니다.
* 클러스터 업그레이드에 실패한 경우 이전 섹션에서 설명한 단계를 수행합니다.

## <a name="can-i-move-my-cluster-to-a-different-subscription-or-my-subscription-with-my-cluster-to-a-new-tenant"></a>내 클러스터를 다른 구독으로 이동하거나 클러스터가 포함된 내 구독을 새 테넌트로 이동할 수 있나요?

AKS 클러스터를 다른 구독으로 이동하거나 클러스터의 구독을 새 테넌트로 이동한 경우 클러스터 ID 권한이 없으므로 클러스터가 작동하지 않습니다. 이러한 제약으로 인해 **AKS는 구독 또는 테넌트 간에 클러스터를 이동하도록 지원하지 않습니다**.

## <a name="im-receiving-errors-trying-to-use-features-that-require-virtual-machine-scale-sets"></a>가상 머신 확장 집합이 필요한 기능을 사용하려고 시도하는 중에 오류가 발생합니다.

*이 문제 해결 지원은 aka.ms/aks-vmss-enablement에서 제공합니다.*

다음 예와 같이 AKS 클러스터가 가상 머신 확장 집합에 없음을 나타내는 오류가 발생할 수 있습니다.

**AgentPool `<agentpoolname>`에서 자동 크기 조정을 '사용'으로 설정했지만 해당 풀이 Virtual Machine Scale Sets에 없습니다.**

클러스터 자동 크기 조정기 또는 여러 노드 풀과 같은 기능을 사용하려면 `vm-set-type` 가상 머신 확장 집합이 필요합니다.

AKS 클러스터를 올바르게 만들려면 해당 문서의 *시작하기 전에* 단계를 따릅니다.

* [클러스터 자동 크기 조정기 사용](cluster-autoscaler.md)
* [여러 노드 풀 만들기 및 사용](use-multiple-node-pools.md)
 
## <a name="what-naming-restrictions-are-enforced-for-aks-resources-and-parameters"></a>AKS 리소스 및 매개 변수에 적용되는 명명 제한은 어떻게 되나요?

*이 문제 해결 지원은 aka.ms/aks-naming-rules에서 제공합니다.*

명명 제한은 Azure 플랫폼 및 AKS에서 모두 구현됩니다. 리소스 이름 또는 매개 변수에서 이러한 제한 중 하나를 위반하면 다른 입력을 제공하라는 오류가 반환됩니다. 적용되는 일반적인 명명 지침은 다음과 같습니다.

* 클러스터 이름은 1-63자여야 합니다. 허용되는 문자는 문자, 숫자, 대시 및 밑줄입니다. 첫 번째 및 마지막 문자는 문자 또는 숫자여야 합니다.
* AKS Node/*MC_* 리소스 그룹 이름은 리소스 그룹 이름과 리소스 이름을 결합합니다. `MC_resourceGroupName_resourceName_AzureRegion`의 자동 생성 구문은 80자 이하여야 합니다. 필요한 경우 리소스 그룹 이름 또는 AKS 클러스터 이름의 길이를 줄입니다. [노드 리소스 그룹 이름을 사용자 지정할 수도 있습니다](cluster-configuration.md#custom-resource-group-name).
* *dnsPrefix* 는 영숫자 값으로 시작하고 끝나야 하며, 1-54자여야 합니다. 유효한 문자에는 영숫자 값 및 하이픈(-)이 포함됩니다. *dnsPrefix* 에는 마침표(.)와 같은 특수 문자가 포함될 수 없습니다.
* AKS 노드 풀 이름은 모두 소문자여야 하고, Linux 노드 풀의 경우 1-11자이고 Windows 노드 풀의 경우 1-6자여야 합니다. 이름은 문자로 시작해야 하며, 허용되는 문자는 문자와 숫자입니다.
* Linux 노드에 대 한 관리자 사용자 이름을 설정 하는 *관리자 사용자 이름은* 문자로 시작 해야 하 고 문자, 숫자, 하이픈 및 밑줄만 포함할 수 있으며 최대 길이는 64 자입니다.

## <a name="im-receiving-errors-when-trying-to-create-update-scale-delete-or-upgrade-cluster-that-operation-is-not-allowed-as-another-operation-is-in-progress"></a>클러스터를 만들거나, 업데이트하거나, 크기 조정하거나, 삭제하거나, 업그레이드하려고 오류가 발생합니다. 다른 작업이 진행 중이므로 해당 작업이 허용되지 않습니다.

*이 문제 해결 지원은 aka.ms/aks-pending-operation에서 제공합니다.*

이전 작업이 아직 진행 중인 경우 클러스터 작업이 제한됩니다. 클러스터의 자세한 상태를 검색하려면 `az aks show -g myResourceGroup -n myAKSCluster -o table` 명령을 사용합니다. 필요에 따라 사용자 고유의 리소스 그룹과 AKS 클러스터 이름을 사용합니다.

클러스터 상태의 출력에 따라 다음을 수행합니다.

* 클러스터가 *성공* 또는 *실패* 가 아닌 프로비전 상태에 있는 경우 작업(*업그레이드/업데이트/만들기/크기 조정/삭제/마이그레이션*)이 완료될 때까지 기다립니다. 이전 작업이 완료되면 최근의 클러스터 작업을 다시 시도합니다.

* 클러스터에 업그레이드에 실패한 경우 [클러스터가 실패 상태에 있고 업그레이드 또는 확장이 수정될 때까지 작동하지 않는다는 오류가 표시됩니다.](#im-receiving-errors-that-my-cluster-is-in-failed-state-and-upgrading-or-scaling-will-not-work-until-it-is-fixed)에서 설명한 단계를 수행합니다.

## <a name="received-an-error-saying-my-service-principal-wasnt-found-or-is-invalid-when-i-try-to-create-a-new-cluster"></a>새 클러스터를 만들려고 하면 내 서비스 주체가 없거나 잘못되었다는 오류가 발생했습니다.

AKS 클러스터를 만드는 경우 사용자를 대신하여 리소스를 만드는 데 서비스 주체 또는 관리 ID가 필요합니다. AKS는 클러스터를 만들 때 자동으로 새 서비스 주체를 만들거나 기존 서비스 주체를 받을 수 있습니다. 자동으로 만든 서비스 주체를 사용하는 경우 Azure Active Directory에서 이를 모든 지역에 전파해야 성공적으로 만들어집니다. 전파하는 데 너무 오래 걸리면 클러스터에서 사용 가능한 서비스 주체를 찾을 수 없으므로 유효성 검사가 실패합니다. 

이 문제에 사용할 수 있는 해결 방법은 다음과 같습니다.
* 이미 여러 지역에 전파되어 클러스터를 만들 때 AKS에 전달되는 기존 서비스 주체를 사용합니다.
* 자동화 스크립트를 사용하는 경우 서비스 주체 만들기와 AKS 클러스터 만들기 사이의 시간 지연을 추가합니다.
* Azure Portal을 사용하는 경우 만드는 중에 클러스터 설정으로 돌아가서 몇 분 후에 유효성 검사 페이지를 다시 시도합니다.

## <a name="im-getting-aadsts7000215-invalid-client-secret-is-provided-when-using-aks-api-what-should-i-do"></a>`"AADSTS7000215: Invalid client secret is provided."`AKS API를 사용 하는 경우 어떻게 해야 합니까?

이 문제는 서비스 주체 자격 증명이 만료 되었기 때문에 발생 합니다. [AKS 클러스터에 대 한 자격 증명을 업데이트 합니다.](update-credentials.md)

## <a name="i-cant-access-my-cluster-api-from-my-automationdev-machinetooling-when-using-api-server-authorized-ip-ranges-how-do-i-fix-this-problem"></a>API server 권한 있는 IP 범위를 사용 하는 경우 automation/dev 컴퓨터/도구에서 내 클러스터 API에 액세스할 수 없습니다. 이 문제를 어떻게 해결하나요?

이 문제를 해결 하려면 `--api-server-authorized-ip-ranges` 사용 중인 자동화/개발/도구 시스템의 ip 또는 ip 범위를 포함 해야 합니다. [권한 있는 ip 주소 범위를 사용 하 여 API 서버에 대 한 보안 액세스](api-server-authorized-ip-ranges.md)에서 ' 내 IP를 찾는 방법 ' 섹션을 참조 하세요.

## <a name="im-unable-to-view-resources-in-kubernetes-resource-viewer-in-azure-portal-for-my-cluster-configured-with-api-server-authorized-ip-ranges-how-do-i-fix-this-problem"></a>API server 권한 있는 IP 범위로 구성 된 클러스터에 대 한 Azure Portal의 Kubernetes 리소스 뷰어에서 리소스를 볼 수 없습니다. 이 문제를 어떻게 해결하나요?

[Kubernetes 리소스 뷰어에](kubernetes-portal.md) 는 포털을 검색 하는 `--api-server-authorized-ip-ranges` 로컬 클라이언트 컴퓨터 또는 IP 주소 범위에 대 한 액세스 권한이 있어야 합니다. [권한 있는 ip 주소 범위를 사용 하 여 API 서버에 대 한 보안 액세스](api-server-authorized-ip-ranges.md)에서 ' 내 IP를 찾는 방법 ' 섹션을 참조 하세요.

## <a name="im-receiving-errors-after-restricting-egress-traffic"></a>송신 트래픽을 제한한 후에 오류가 발생했습니다.

AKS 클러스터의 송신 트래픽을 제한하는 경우 AKS에 대한 [필수 및 선택적 추천](limit-egress-traffic.md) 아웃바운드 포트/네트워크 규칙 및 FQDN/애플리케이션 규칙이 있습니다. 설정이 이러한 규칙 중 하나와 충돌하면 특정 `kubectl` 명령이 제대로 작동하지 않습니다. AKS 클러스터를 만들 때도 오류가 표시될 수 있습니다.

설정이 필수 또는 선택적 추천 아웃바운드 포트/네트워크 규칙 및 FQDN/애플리케이션 규칙과 충돌하지 않는지 확인합니다.

## <a name="im-receiving-429---too-many-requests-errors"></a>"429-너무 많은 요청" 오류를 받고 있습니다.

Azure (AKS 또는 no)의 kubernetes 클러스터가 잦은 규모를 확대/축소 하거나 클러스터 autoscaler (CA)를 사용 하는 경우 이러한 작업으로 인해 많은 수의 HTTP 호출이 발생 하 여 할당 된 구독 할당량을 초과 하 게 되 면 오류가 발생 합니다. 오류는 다음과 같습니다.

```
Service returned an error. Status=429 Code=\"OperationNotAllowed\" Message=\"The server rejected the request because too many requests have been received for this subscription.\" Details=[{\"code\":\"TooManyRequests\",\"message\":\"{\\\"operationGroup\\\":\\\"HighCostGetVMScaleSet30Min\\\",\\\"startTime\\\":\\\"2020-09-20T07:13:55.2177346+00:00\\\",\\\"endTime\\\":\\\"2020-09-20T07:28:55.2177346+00:00\\\",\\\"allowedRequestCount\\\":1800,\\\"measuredRequestCount\\\":2208}\",\"target\":\"HighCostGetVMScaleSet30Min\"}] InnerError={\"internalErrorCode\":\"TooManyRequestsReceived\"}"}
```

이러한 제한 오류는 [여기](../azure-resource-manager/management/request-limits-and-throttling.md) 와 [여기](../virtual-machines/troubleshooting/troubleshooting-throttling-errors.md) 에 자세히 설명 되어 있습니다.

AKS 엔지니어링 팀의 권장 사항은 많은 향상 된 기능을 포함 하는 1.18 이상 버전을 실행 하 고 있는지 확인 하는 것입니다. 자세한 내용은 [여기](https://github.com/Azure/AKS/issues/1413) 및 [여기](https://github.com/kubernetes-sigs/cloud-provider-azure/issues/247)에서 향상 된 기능을 참조 하세요.

이러한 제한 오류는 구독 수준에서 측정 되며 다음과 같은 경우에도 발생할 수 있습니다.
- GET 요청을 수행 하는 타사 응용 프로그램 (예: 응용 프로그램 모니터링 등)이 있습니다. 이러한 호출의 빈도를 줄이는 것이 좋습니다.
- Virtual machine scale sets를 사용 하는 다양 한 AKS 클러스터/노드 풀이 있습니다. 클러스터 수를 다른 구독으로 분할 해 보세요. 특히, 활성 클러스터 autoscaler 같이 매우 활성 상태 이거나 여러 클라이언트 (예: rancher, terraform 등)가 있는 경우입니다.

## <a name="my-clusters-provisioning-status-changed-from-ready-to-failed-with-or-without-me-performing-an-operation-what-should-i-do"></a>작업을 수행 하거나 사용 하지 않고 클러스터의 프로 비전 상태가 준비에서 실패로 변경 되었습니다. 어떻게 해야 합니까?

작업을 수행 하지 않고 클러스터의 프로 비전 상태가 *준비* 에서 *실패* 로 변경 되 고 클러스터의 응용 프로그램이 계속 실행 되는 경우이 문제는 서비스에서 자동으로 해결할 수 있으며 응용 프로그램에 영향을 주지 않습니다.

클러스터의 프로 비전 상태가 *실패* 로 유지 되거나 클러스터의 응용 프로그램이 작동을 중지 하는 경우 [지원 요청을 제출](https://azure.microsoft.com/support/options/#submit)합니다.

## <a name="my-watch-is-stale-or-azure-ad-pod-identity-nmi-is-returning-status-500"></a>내 watch가 오래 되었거나 Azure AD Pod Id NMI가 상태 500을 반환 합니다.

이 [예에서](limit-egress-traffic.md#restrict-egress-traffic-using-azure-firewall)와 같이 Azure 방화벽을 사용 하는 경우 응용 프로그램 규칙을 사용 하 여 방화벽을 통한 오랜 시간 TCP 연결에 현재 버그가 발생 하 여 (Q1CY21에서 해결 됨) 방화벽에서 이동이 종료 될 수 있으므로이 문제가 발생할 수 있습니다 `keepalives` . 이 문제가 해결 될 때까지 AKS API 서버 IP에 네트워크 규칙 (응용 프로그램 규칙 대신)을 추가 하 여 완화할 수 있습니다.

## <a name="azure-storage-and-aks-troubleshooting"></a>Azure Storage 및 AKS 문제 해결

### <a name="failure-when-setting-uid-and-gid-in-mountoptions-for-azure-disk"></a>`GID`Azure 디스크에 대해 uid와 mountOptions를 설정 하는 동안 오류가 발생 했습니다.

Azure 디스크는 기본적으로 ext4,xfs 파일 시스템을 사용하며, 탑재 시 mountOptions(예: uid=x,gid=x)를 설정할 수 없습니다. 예를 들어 mountOptions uid=999,gid=999를 설정하려고 하면 다음과 같은 오류가 표시됩니다.

```console
Warning  FailedMount             63s                  kubelet, aks-nodepool1-29460110-0  MountVolume.MountDevice failed for volume "pvc-d783d0e4-85a1-11e9-8a90-369885447933" : azureDisk - mountDevice:FormatAndMount failed with mount failed: exit status 32
Mounting command: systemd-run
Mounting arguments: --description=Kubernetes transient mount for /var/lib/kubelet/plugins/kubernetes.io/azure-disk/mounts/m436970985 --scope -- mount -t xfs -o dir_mode=0777,file_mode=0777,uid=1000,gid=1000,defaults /dev/disk/azure/scsi1/lun2 /var/lib/kubelet/plugins/kubernetes.io/azure-disk/mounts/m436970985
Output: Running scope as unit run-rb21966413ab449b3a242ae9b0fbc9398.scope.
mount: wrong fs type, bad option, bad superblock on /dev/sde,
       missing codepage or helper program, or other error
```

이 문제는 다음 옵션 중 하나를 수행하여 완화할 수 있습니다.

* runAsUser에서 uid를 설정하고 fsGroup에서 gid를 설정하여 [Pod에 대한 보안 컨텍스트를 구성](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)합니다. 예를 들어 다음 설정은 모든 파일에 액세스할 수 있도록 Pod 실행을 루트로 설정합니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 0
    fsGroup: 0
```

  >[!NOTE]
  > 이는 gid 및 uid를 기본적으로 root 또는 0으로 탑재하기 때문입니다. gid 또는 uid가 root가 아닌 값(예: 1000)으로 설정된 경우 Kubernetes는 `chown`을 사용하여 해당 디스크 아래의 모든 디렉터리와 파일을 변경합니다. 이 작업을 수행하는 데 시간이 오래 걸릴 수 있으며 디스크를 매우 느리게 탑재할 수 있습니다.

* `chown`InitContainers에서를 사용 하 여 및를 설정 `GID` `UID` 합니다. 다음은 그 예입니다.

```yaml
initContainers:
- name: volume-mount
  image: busybox
  command: ["sh", "-c", "chown -R 100:100 /data"]
  volumeMounts:
  - name: <your data volume>
    mountPath: /data
```

### <a name="azure-disk-detach-failure-leading-to-potential-race-condition-issue-and-invalid-data-disk-list"></a>잠재적 경합 상태 문제 및 잘못된 데이터 디스크 목록이 생성되는 Azure 디스크 분리 오류

Azure 디스크를 분리하지 못하면 지수 백오프를 사용하여 디스크를 분리하기 위해 최대 6회까지 다시 시도합니다. 또한 데이터 디스크 목록에서 약 3분 동안 노드 수준 잠금을 유지합니다. 이 시간 동안 디스크 목록을 수동으로 업데이트하면 노드 수준 잠금을 통해 유지된 디스크 목록이 더 이상 사용되지 않고 노드가 불안정해질 수 있습니다.

이 문제는 다음 Kubernetes 버전에서 해결되었습니다.

| Kubernetes 버전 | 수정 버전 |
|--|:--:|
| 1.12 | 1.12.9 이상 |
| 1.13 | 1.13.6 이상 |
| 1.14 | 1.14.2 이상 |
| 1.15 이상 | 해당 없음 |

이 문제에 대한 수정이 없는 Kubernetes 버전을 사용하고 있고 노드에 사용되지 않는 디스크 목록이 있는 경우 존재하지 않는 모든 디스크를 VM에서 대량 작업으로 분리하여 완화할 수 있습니다. **존재하지 않는 디스크는 개별적으로 분리하지 못할 수 있습니다.**

### <a name="large-number-of-azure-disks-causes-slow-attachdetach"></a>Azure 디스크 수가 많으면 연결/분리 속도가 느려집니다.

단일 노드 VM을 대상으로 하는 Azure 디스크 연결/분리 작업 수가 10개보다 크거나 단일 가상 머신 확장 집합 풀을 대상으로 할 때 3개보다 큰 경우 순차적으로 수행되므로 예상보다 느릴 수 있습니다. 이 문제는 알려진 제한 사항이며 현재 해결 방법이 없습니다. [숫자를 초과하는 병렬 연결/분리를 지원하는 사용자 음성 항목이 있습니다](https://feedback.azure.com/forums/216843-virtual-machines/suggestions/40444528-vmss-support-for-parallel-disk-attach-detach-for).

### <a name="azure-disk-detach-failure-leading-to-potential-node-vm-in-failed-state"></a>잠재적 노드 VM이 실패 상태가 되는 Azure 디스크 분리 오류

일부 에지의 경우 Azure 디스크 분리가 부분적으로 실패하고 노드 VM이 실패 상태로 유지될 수 있습니다.

이 문제는 다음 Kubernetes 버전에서 해결되었습니다.

| Kubernetes 버전 | 수정 버전 |
|--|:--:|
| 1.12 | 1.12.10 이상 |
| 1.13 | 1.13.8 이상 |
| 1.14 | 1.14.4 이상 |
| 1.15 이상 | 해당 없음 |

이 문제에 대한 수정이 없는 Kubernetes 버전을 사용하고 있고 노드가 실패 상태에 있는 경우 다음 중 하나를 사용하여 VM 상태를 수동으로 업데이트하여 완화할 수 있습니다.

* 가용성 집합 기반 클러스터의 경우:
    ```azurecli
    az vm update -n <VM_NAME> -g <RESOURCE_GROUP_NAME>
    ```

* VMSS 기반 클러스터의 경우:
    ```azurecli
    az vmss update-instances -g <RESOURCE_GROUP_NAME> --name <VMSS_NAME> --instance-id <ID>
    ```

## <a name="azure-files-and-aks-troubleshooting"></a>Azure Files 및 AKS 문제 해결

### <a name="what-are-the-recommended-stable-versions-of-kubernetes-for-azure-files"></a>Azure Files용으로 추천되는 안정적인 Kubernetes 버전은 무엇인가요?
 
| Kubernetes 버전 | 추천 버전 |
|--|:--:|
| 1.12 | 1.12.6 이상 |
| 1.13 | 1.13.4 이상 |
| 1.14 | 1.14.0 이상 |

### <a name="what-are-the-default-mountoptions-when-using-azure-files"></a>Azure Files를 사용하는 경우 기본 mountOptions는 무엇인가요?

추천 설정:

| Kubernetes 버전 | fileMode 및 dirMode 값|
|--|:--:|
| 1.12.0 - 1.12.1 | 0755 |
| 1.12.2 이상 | 0777 |

탑재 옵션은 스토리지 클래스 개체에 지정할 수 있습니다. 다음 예제에서는 *0777* 을 설정합니다.

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
  - mfsymlinks
  - nobrl
  - cache=none
parameters:
  skuName: Standard_LRS
```

몇 가지 유용한 추가 *mountOptions* 설정은 다음과 같습니다.

* `mfsymlinks` cifs (Azure Files mount)에서 기호화 된 링크를 지원 하는지 확인 합니다.
* `nobrl` 는 바이트 범위 잠금 요청을 서버로 보내지 못하게 합니다. 이 설정은 cifs 스타일 필수 바이트 범위 잠금으로 중단되는 특정 애플리케이션에 필요합니다. 대부분의 cifs 서버는 아직 추천 바이트 범위 잠금 요청을 지원하지 않습니다. *nobrl* 을 사용하지 않는 경우 cifs 스타일 필수 바이트 범위 잠금으로 중단되는 애플리케이션에서 다음과 비슷한 오류 메시지가 발생할 수 있습니다.
    ```console
    Error: SQLITE_BUSY: database is locked
    ```

### <a name="error-could-not-change-permissions-when-using-azure-files"></a>Azure Files를 사용하는 경우 발생하는 "권한을 변경할 수 없습니다" 오류

Azure Files 플러그 인에서 PostgreSQL을 실행하면 다음과 비슷한 오류가 표시될 수 있습니다.

```console
initdb: could not change permissions of directory "/var/lib/postgresql/data": Operation not permitted
fixing permissions on existing directory /var/lib/postgresql/data
```

이 오류는 cifs/SMB 프로토콜을 사용하는 Azure Files 플러그 인으로 인해 발생합니다. cifs/SMB 프로토콜을 사용하는 경우 탑재 후에 파일 및 디렉터리 권한을 변경할 수 없습니다.

이 문제를 해결 하려면 `subPath` Azure Disk plugin과 함께를 사용 합니다. 

> [!NOTE] 
> ext3/4 디스크 유형의 경우 디스크를 포맷한 후에 lost+found 디렉터리가 있습니다.

### <a name="azure-files-has-high-latency-compared-to-azure-disk-when-handling-many-small-files"></a>Azure Files에서 작은 파일을 많이 처리할 때 Azure 디스크에 비해 대기 시간이 오래 걸립니다.

많은 작은 파일을 처리하는 것과 같은 경우에 Azure 디스크와 비교할 때 Azure Files를 사용할 때 대기 시간이 길어질 수 있습니다.

### <a name="error-when-enabling-allow-access-allow-access-from-selected-network-setting-on-storage-account"></a>스토리지 계정에서 "선택한 네트워크에서 액세스 허용" 설정을 사용하도록 설정하면 발생하는 오류

AKS에서 동적 프로비저닝에 사용되는 스토리지 계정에서 *선택한 네트워크에서 액세스 허용* 을 사용하도록 설정하면 AKS에서 파일 공유를 만들 때 오류가 발생합니다.

```console
persistentvolume-controller (combined from similar events): Failed to provision volume with StorageClass "azurefile": failed to create share kubernetes-dynamic-pvc-xxx in account xxx: failed to create file share, err: storage: service returned error: StatusCode=403, ErrorCode=AuthorizationFailure, ErrorMessage=This request is not authorized to perform this operation.
```

*선택한 네트워크에서 액세스 허용* 을 설정할 때 선택한 네트워크에 Kubernetes *persistentvolume-controller* 가 없으므로 이 오류가 발생합니다.

이 문제는 [Azure Files에서 정적 프로비저닝](azure-files-volume.md)을 사용하여 완화할 수 있습니다.

### <a name="azure-files-fails-to-remount-in-windows-pod"></a>Azure Files에서 Windows Pod에 다시 탑재하지 못했습니다.

Azure Files 탑재가 있는 Windows Pod가 삭제된 다음, 동일한 노드에 다시 만들어지도록 예약되면 탑재가 실패합니다. Azure Files 탑재가 이미 노드에 탑재되어 있어 `New-SmbGlobalMapping` 명령이 실패하므로 이 오류가 발생합니다.

예를 들어 다음과 비슷한 오류가 표시될 수 있습니다.

```console
E0118 08:15:52.041014    2112 nestedpendingoperations.go:267] Operation for "\"kubernetes.io/azure-file/42c0ea39-1af9-11e9-8941-000d3af95268-pvc-d7e1b5f9-1af3-11e9-8941-000d3af95268\" (\"42c0ea39-1af9-11e9-8941-000d3af95268\")" failed. No retries permitted until 2019-01-18 08:15:53.0410149 +0000 GMT m=+732.446642701 (durationBeforeRetry 1s). Error: "MountVolume.SetUp failed for volume \"pvc-d7e1b5f9-1af3-11e9-8941-000d3af95268\" (UniqueName: \"kubernetes.io/azure-file/42c0ea39-1af9-11e9-8941-000d3af95268-pvc-d7e1b5f9-1af3-11e9-8941-000d3af95268\") pod \"deployment-azurefile-697f98d559-6zrlf\" (UID: \"42c0ea39-1af9-11e9-8941-000d3af95268\") : azureMount: SmbGlobalMapping failed: exit status 1, only SMB mount is supported now, output: \"New-SmbGlobalMapping : Generic failure \\r\\nAt line:1 char:190\\r\\n+ ... ser, $PWord;New-SmbGlobalMapping -RemotePath $Env:smbremotepath -Cred ...\\r\\n+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~\\r\\n    + CategoryInfo          : NotSpecified: (MSFT_SmbGlobalMapping:ROOT/Microsoft/...mbGlobalMapping) [New-SmbGlobalMa \\r\\n   pping], CimException\\r\\n    + FullyQualifiedErrorId : HRESULT 0x80041001,New-SmbGlobalMapping\\r\\n \\r\\n\""
```

이 문제는 다음 Kubernetes 버전에서 해결되었습니다.

| Kubernetes 버전 | 수정 버전 |
|--|:--:|
| 1.12 | 1.12.6 이상 |
| 1.13 | 1.13.4 이상 |
| 1.14 이상 | 해당 없음 |

### <a name="azure-files-mount-fails-because-of-storage-account-key-changed"></a>스토리지 계정 키가 변경되어 Azure Files 탑재가 실패합니다.

스토리지 계정 키가 변경된 경우 Azure Files 탑재 실패가 표시될 수 있습니다.

base64로 인코딩된 스토리지 계정 키를 사용하여 Azure 파일 비밀에서 `azurestorageaccountkey` 필드를 수동으로 업데이트하여 완화할 수 있습니다.

스토리지 계정 키를 base64로 인코딩하려면 `base64`를 사용할 수 있습니다. 다음은 그 예입니다.

```console
echo X+ALAAUgMhWHL7QmQ87E1kSfIqLKfgC03Guy7/xk9MyIg2w4Jzqeu60CVw2r/dm6v6E0DWHTnJUEJGVQAoPaBc== | base64
```

Azure 비밀 파일을 업데이트하려면 `kubectl edit secret`을 사용합니다. 다음은 그 예입니다.

```console
kubectl edit secret azure-storage-account-{storage-account-name}-secret
```

몇 분 후에 에이전트 노드에서 업데이트된 스토리지 키를 사용하여 Azure File 탑재를 다시 시도합니다.


### <a name="cluster-autoscaler-fails-to-scale-with-error-failed-to-fix-node-group-sizes"></a>노드 그룹 크기를 수정하지 못하는 오류로 인해 클러스터 자동 크기 조정기에서 크기를 조정하지 못했습니다.

클러스터 자동 크기 조정기에서 규모 강화/축소를 수행하지 않고 [클러스터 자동 크기 조정기 로그][view-master-logs]에 다음과 같은 오류가 표시되는 경우입니다.

```console
E1114 09:58:55.367731 1 static_autoscaler.go:239] Failed to fix node group sizes: failed to decrease aks-default-35246781-vmss: attempt to delete existing nodes
```

이 오류는 업스트림 클러스터 자동 크기 조정기 경합 상태로 인해 발생합니다. 이러한 경우 클러스터 자동 크기 조정기는 실제로 클러스터에 있는 값과 다른 값으로 끝납니다. 이 상태를 벗어나려면 [클러스터 자동 크기 조정기][cluster-autoscaler]를 사용하지 않도록 설정했다가 다시 사용하도록 설정합니다.

### <a name="slow-disk-attachment-getazuredisklun-takes-10-to-15-minutes-and-you-receive-an-error"></a>디스크 첨부 속도가 느려서 `GetAzureDiskLun` 10 ~ 15 분 정도 걸리며 오류가 발생 합니다.

**1.15.0 이전** 의 Kubernetes 버전에서 **WaitForAttach에서 디스크에 대한 LUN을 찾을 수 없음 오류** 와 같은 오류가 발생할 수 있습니다.  이 문제를 해결하려면 약 15분 정도 기다렸다가 다시 시도합니다.


### <a name="why-do-upgrades-to-kubernetes-116-fail-when-using-node-labels-with-a-kubernetesio-prefix"></a>Kubernetes.io 접두사를 사용 하 여 노드 레이블을 사용 하는 경우 Kubernetes 1.16로의 업그레이드가 실패 하는 이유

Kubernetes [1.16](https://v1-16.docs.kubernetes.io/docs/setup/release/notes/) 를 기준으로 [kubernetes.io 접두사를 사용 하 여 정의 된 레이블의 하위 집합만](https://v1-18.docs.kubernetes.io/docs/concepts/overview/working-with-objects/labels/) 노드에 적용할 수 있습니다. AKS는 영향을 받는 작업에 가동 중지 시간이 발생할 수 있으므로 동의 없이 사용자를 대신 하 여 활성 레이블을 제거할 수 없습니다.

따라서이 문제를 완화 하기 위해 다음 작업을 수행할 수 있습니다.

1. 클러스터 제어 평면을 1.16 이상으로 업그레이드
2. 지원 되지 않는 kubernetes.io 레이블이 없으면 1.16 이상에서 새 nodepoool를 추가 합니다.
3. 이전 노드 풀 삭제

AKS는이 완화를 개선 하기 위해 노드 풀에서 활성 레이블을 변경할 수 있는 기능을 조사 하 고 있습니다.



<!-- LINKS - internal -->
[view-master-logs]: view-master-logs.md
[cluster-autoscaler]: cluster-autoscaler.md
