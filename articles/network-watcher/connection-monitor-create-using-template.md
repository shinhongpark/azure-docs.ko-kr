---
title: 연결 모니터 만들기-ARM 템플릿
titleSuffix: Azure Network Watcher
description: ARMClient를 사용 하 여 연결 모니터를 만드는 방법에 대해 알아봅니다.
services: network-watcher
documentationcenter: na
author: vinigam
ms.service: network-watcher
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/07/2021
ms.author: vinigam
ms.openlocfilehash: 46d569eae768178815a933d9a857e19bacdaaeb9
ms.sourcegitcommit: 42a4d0e8fa84609bec0f6c241abe1c20036b9575
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98013229"
---
# <a name="create-a-connection-monitor-using-the-arm-template"></a>ARM 템플릿을 사용 하 여 연결 모니터 만들기

ARMClient를 사용 하 여 리소스 간의 통신을 모니터링 하는 연결 모니터를 만드는 방법에 대해 알아봅니다. 하이브리드 및 Azure 클라우드 배포를 지원 합니다.


## <a name="before-you-begin"></a>시작하기 전 주의 사항 

연결 모니터에서 만드는 연결 모니터에서 온-프레미스 컴퓨터와 Azure Vm을 모두 원본으로 추가할 수 있습니다. 이러한 연결 모니터는 끝점에 대 한 연결을 모니터링할 수도 있습니다. 끝점은 Azure 또는 다른 모든 URL 또는 IP에 있을 수 있습니다.

연결 모니터에는 다음 엔터티가 포함 됩니다.

* **연결 모니터 리소스** – 지역별 Azure 리소스입니다. 다음 엔터티는 모두 연결 모니터 리소스의 속성입니다.
* **끝점** – 연결 확인에 참여 하는 원본 또는 대상입니다. 끝점의 예로는 Azure Vm, 온-프레미스 에이전트, Url 및 Ip가 있습니다.
* **테스트 구성** – 테스트에 대 한 프로토콜 관련 구성입니다. 선택한 프로토콜에 따라 포트, 임계값, 테스트 빈도 및 기타 매개 변수를 정의할 수 있습니다.
* **테스트 그룹** – 소스 끝점, 대상 끝점 및 테스트 구성이 포함 된 그룹입니다. 연결 모니터에는 두 개 이상의 테스트 그룹이 포함 될 수 있습니다.
* **Test** – 소스 끝점, 대상 끝점 및 테스트 구성의 조합입니다. 테스트는 모니터링 데이터를 사용할 수 있는 가장 세분화 된 수준입니다. 모니터링 데이터는 실패 한 검사 비율과 RTT (왕복 시간)를 포함 합니다.

    ![테스트 그룹 및 테스트 간의 관계를 정의 하는 연결 모니터를 보여 주는 다이어그램](./media/connection-monitor-2-preview/cm-tg-2.png)

## <a name="steps-to-create-with-sample-arm-template"></a>샘플 ARM 템플릿을 사용 하 여 만드는 단계

ARMClient를 사용 하 여 연결 모니터를 만들려면 다음 코드를 사용 합니다.

```armclient
$connectionMonitorName = "sampleConnectionMonitor"

$ARM = "https://management.azure.com"

$SUB = "subscriptions/<subscription id 1>;"

$NW = "resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher\_<region>"

$body =

"{

location: '<region>',

properties: {

endpoints: [{

name: 'endpoint_workspace_machine',

type: 'MMAWorkspaceMachine',

resourceId: '/subscriptions/<subscription id>/resourcegroups/<resource group>/providers/Microsoft.OperationalInsights/workspaces/sampleWorkspace',

//Example 1: Choose a machine

address : '<non-Azure machine FQDN>'
}

//Example 2: Select IP from chosen machines

address : '<non-Azure machine FQDN>

"scope": {
      "include": [
            {
                  "address": "<IP belonging to machine chosen above>"  
        }
       ]
      }
   }    
   
name: 'endpoint_workspace_network',

type: 'MMAWorkspaceNetwork',

resourceId: '/subscriptions/<subscription id>/resourcegroups/<resource group>/providers/Microsoft.OperationalInsights/workspaces/sampleWorkspace',

 coverage level : 'high', //Optional
 
 //Include subnets. You can also exclude IPs from subnet to exclude from monitoring
 
 scope: {
      "include": [
            {
                  "address": "<subnet 1 mask>" // Eg: 10.10.1.0/28
            },
            {
                  "address": "<subnet 2 mask>" 
            }
      ],
      "exclude": [
            { 
            "address" : "<ip-from-included-subnets-that-should-be-excluded>"
        }
      ]
     }
},

//Use a Azure VM as an endpoint
{

name: 'endpoint_virtualmachine',

resourceId: '/subscriptions/<subscription id>/resourceGroups/<resource group>/providers/Microsoft.Compute/virtualMachines/<vm-name>'

},

//Use an Azure VNET or Subnet as an endpoint

 {

name: 'endpoint_vnet_subnet',

resourceId: '<resource id of VNET or subnet'
coverage level: 'high' //Optional

//Scope is optional.

  "scope": {
      "include": [
            {
                  "address": "<subnet 1 mask>" // Eg: 10.10.1.0/28 .This subnet should match with any existing subnet in vnet
            }
      ],
    "exclude": [
            {
                  "address": "<ip-from-included-subnets-that-should-be-excluded>" // If used with include, IP should be part of the subnet defined above. Without include, this could be any address within vnet range or any specific subnet range as a whole.
            }
      ]
  }
   },

//Endpoint as a URL
{

name: 'azure portal'

address: '<URL>'

   },

//Endpoint as an IP 
 {

    name: 'ip',

     address: '<IP>'

 }

  ],

  testGroups: [{

    name: 'Connectivity to Azure Portal and Public IP',

    testConfigurations: ['http', 'https', 'tcpEnabled', 'icmpEnabled'],

    sources: ['vm1', 'workspace'],

    destinations: ['azure portal', 'ip']

   },

{

    name: 'Connectivty from Azure VM 1 to Azure VM 2',

   // Choose your protocol
   
    testConfigurations: ['http', 'https', 'tcpDisabled', 'icmpDisabled'],

    sources: ['vm1'],

    destinations: ['vm2'],

    disable: true

   }

  ],

  testConfigurations: [{

    name: 'http',

    testFrequencySec: <frequency>,

    protocol: 'HTTP',

    successThreshold: {

     checksFailedPercent: <threshold for checks failed %>,

     roundTripTimeMs: <threshold for RTT>

    }

   }, {

    name: 'https',

    testFrequencySec: <frequency>,

    protocol: 'HTTP',

    httpConfiguration: {
    
     port: '<port of choice>'
  
    preferHTTPS: true // If port chosen is not 80 or 443
    
    method: 'GET', //Choose GET or POST
    
    path: '/', //Specify path for request
         
    requestHeaders: [
            {
              "name": "Content-Type",
              "value": "appication/json"
            }
          ],
          
    validStatusCodeRanges: [ "102", "200-202", "3xx" ], //Samples
          
    },

    successThreshold: {

     checksFailedPercent: <choose your checks failed threshold>,

     roundTripTimeMs: <choose your RTT threshold>

    }

   }, 
   {

    name: 'tcpEnabled',

    testFrequencySec: <frequency>,

    protocol: 'TCP',

    tcpConfiguration: {

     port: 80

    },

    successThreshold: {

     checksFailedPercent: <choose your checks failed threshold>,

     roundTripTimeMs: <choose your RTT threshold>

    }

   }, {

    name: 'icmpEnabled',

    testFrequencySec: <frequency>,

    protocol: 'ICMP',

    successThreshold: {

     checksFailedPercent: <choose your checks failed threshold>,

     roundTripTimeMs: <choose your RTT threshold>

    }

   }, {

    name: 'icmpDisabled',

    testFrequencySec: <frequency>,

    protocol: 'ICMP',

    icmpConfiguration: {

     disableTraceRoute: true

    },

    successThreshold: {

     checksFailedPercent: <choose your checks failed threshold>,

     roundTripTimeMs: <choose your RTT threshold>

    }

   }, {

    name: 'tcpDisabled',

    testFrequencySec: <frequency>,

    protocol: 'TCP',

    tcpConfiguration: {

     port: 80,

     disableTraceRoute: true

    },

    successThreshold: {

     checksFailedPercent: <choose your checks failed threshold>,

     roundTripTimeMs: <choose your RTT threshold>

    }

   }

  ]

 }

} "
```

배포 명령은 다음과 같습니다.
```
armclient PUT $ARM/$SUB/$NW/connectionMonitors/$connectionMonitorName/?api-version=2019-07-01 $body -verbose
```

## <a name="description-of-properties"></a>속성 설명

* connectionMonitorName-연결 모니터 리소스의 이름

* 연결 모니터를 만들려는 구독의 하위 구독 ID

* NW-CM이 생성 되는 리소스 ID를 Network Watcher 합니다. 

* 위치-연결 모니터가 생성 될 지역

* 엔드포인트
    * 이름 – 각 끝점에 대 한 고유 이름
    * resourceId – Azure 끝점의 경우 리소스 ID는 가상 머신의 Azure Resource Manager 리소스 ID를 나타냅니다. 비 Azure 끝점의 경우 리소스 ID는 비 Azure 에이전트에 연결 된 Log Analytics 작업 영역에 대 한 Azure Resource Manager 리소스 ID를 나타냅니다.
    * address – 리소스 ID가 지정 되지 않았거나 리소스 ID가 작업 영역 Log Analytics 경우에만 적용 됩니다. Log Analytics 리소스 ID와 함께 사용 하는 경우이는 모니터링에 사용할 수 있는 에이전트의 FQDN을 나타냅니다. 리소스 ID 없이 사용 하는 경우이는 모든 공용 끝점의 URL 또는 IP 일 수 있습니다.
    * filter – 비 Azure 끝점의 경우 필터를 사용 하 여 연결 모니터 리소스의 모니터링에 사용할 Log Analytics 작업 영역에서 에이전트를 선택 합니다. 필터를 설정 하지 않으면 Log Analytics 작업 영역에 속하는 모든 에이전트를 모니터링에 사용할 수 있습니다.
        * 유형 – 유형을 "에이전트 주소"로 설정 합니다.
        * 주소 – 온-프레미스 에이전트의 FQDN으로 주소를 설정 합니다.

* 테스트 그룹
    * 이름-테스트 그룹 이름을로 합니다.
    * testConfigurations-대상 끝점에 연결 하는 소스 끝점을 기준으로 하는 테스트 구성
    * 소스-위에서 만든 끝점에서 선택 합니다. Azure 기반 소스 끝점은 Azure Network Watcher 확장을 설치 해야 하며 Azure 기반이 아닌 소스 끝점은 haveAzure Log Analytics 에이전트가 설치 되어야 합니다. 원본에 대 한 에이전트를 설치 하려면 [모니터링 에이전트 설치](./connection-monitor-overview.md#install-monitoring-agents)를 참조 하세요.
    * 대상-위에서 만든 끝점에서 선택 합니다. 대상으로 지정 하 여 Azure Vm 또는 끝점 (공용 IP, URL 또는 FQDN)에 대 한 연결을 모니터링할 수 있습니다. 단일 테스트 그룹에서 Azure Vm, Office 365 Url, Dynamics 365 Url 및 사용자 지정 끝점을 추가할 수 있습니다.
    * disable-이 필드를 사용 하 여 테스트 그룹에서 지정 하는 모든 원본 및 대상에 대해 모니터링을 사용 하지 않도록 설정 합니다.

* 테스트 구성
    * 이름-테스트 구성의 이름입니다.
    * testFrequencySec-원본에서 지정 된 프로토콜 및 포트의 대상을 ping 하는 빈도를 지정 합니다. 30 초, 1 분, 5 분, 15 분 또는 30 분을 선택할 수 있습니다. 원본은 사용자가 선택한 값을 기준으로 대상에 대 한 연결을 테스트 합니다. 예를 들어 30 초를 선택 하면 소스는 30 초 동안 한 번 이상 대상에 대 한 연결을 확인 합니다.
    * 프로토콜-TCP, ICMP, HTTP 또는 HTTPS를 선택할 수 있습니다. 프로토콜에 따라 몇 가지 프로토콜 관련 configs을 수행할 수 있습니다.
    
        * preferHTTPS-사용 되는 포트가 80 또는 443이 아닌 경우 HTTP를 통해 HTTPS를 사용할지 여부를 지정 합니다.
        * 포트-선택한 대상 포트를 지정 합니다.
        * disableTraceRoute-프로토콜이 TCP 또는 ICMP 인 테스트 구성에 적용 됩니다. 원본 토폴로지 및 홉 단위 RTT를 검색 하지 못하도록 합니다.
        * 메서드-프로토콜이 HTTP 인 테스트 구성에 적용 됩니다. HTTP 요청 메서드 (GET 또는 POST)를 선택 합니다.
        * 경로-URL에 추가할 경로 매개 변수를 지정 합니다.
        * 유효한 Statuscode-적용 가능한 상태 코드를 선택 합니다. 응답 코드가이 목록과 일치 하지 않으면 진단 메시지를 받게 됩니다.
        * requestHeaders-대상에 전달 될 사용자 지정 요청 헤더 문자열을 지정 합니다.
        
    * successThreshold-다음 네트워크 매개 변수에 대 한 임계값을 설정할 수 있습니다.
        * checksFailedPercent-원본에서 지정 된 조건을 사용 하 여 대상에 대 한 연결을 확인할 때 실패할 수 있는 검사 비율을 설정 합니다. TCP 또는 ICMP 프로토콜의 경우 실패 한 검사의 백분율이 패킷 손실의 백분율에 동일시 수 있습니다. HTTP 프로토콜의 경우이 필드는 응답을 받지 못한 HTTP 요청 비율을 나타냅니다.
        * roundTripTimeMs-소스에서 테스트 구성을 통해 대상에 연결 하는 데 걸리는 시간 (밀리초)을 설정 합니다.

## <a name="scale-limits"></a> 확장 한도

연결 모니터의 크기 제한은 다음과 같습니다.

* 지역별 구독 당 최대 연결 모니터 수: 100
* 연결당 최대 테스트 그룹 수 모니터: 20
* 연결 당 최대 원본 및 대상 모니터: 100
* 연결 모니터 당 최대 테스트 구성 수: 20 via ARMClient

## <a name="next-steps"></a>다음 단계

* [모니터링 데이터를 분석 하 고 경고를 설정 하는 방법](./connection-monitor-overview.md#analyze-monitoring-data-and-set-alerts) 알아보기
* [네트워크에서 문제를 진단 하는 방법을](./connection-monitor-overview.md#diagnose-issues-in-your-network) 알아봅니다.