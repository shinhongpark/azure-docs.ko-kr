---
title: Azure Cloud Services (클래식) NetworkConfiguration 스키마 | Microsoft Docs
description: Virtual Network 및 DNS 값을 지정 하는 서비스 구성 파일의 NetworkConfiguration 요소에 대 한 자식 요소에 대해 알아봅니다.
ms.topic: article
ms.service: cloud-services
ms.date: 10/14/2020
ms.author: tagore
author: tanmaygore
ms.reviewer: mimckitt
ms.custom: ''
'---thor': tagore
ms.openlocfilehash: acf4c050ade21a6e5fc51ee6ace512eff00360ab
ms.sourcegitcommit: 6272bc01d8bdb833d43c56375bab1841a9c380a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98743460"
---
# <a name="azure-cloud-services-classic-config-networkconfiguration-schema"></a>Azure Cloud Services (클래식) Config NetworkConfiguration 스키마

> [!IMPORTANT]
> Azure [Cloud Services (확장 지원)](../cloud-services-extended-support/overview.md) 는 azure Cloud Services 제품에 대 한 새로운 Azure Resource Manager 기반 배포 모델입니다.이러한 변경으로 Azure Service Manager 기반 배포 모델에서 실행 되는 Azure Cloud Services는 Cloud Services (클래식)으로 이름이 바뀌고 모든 새 배포는 [Cloud Services (확장 된 지원)](../cloud-services-extended-support/overview.md)를 사용 해야 합니다.

서비스 구성 파일의 `NetworkConfiguration` 요소는 Virtual Network 및 DNS 값을 지정합니다. 이러한 설정은 클라우드 서비스에 대한 선택 사항입니다.

Virtual Network와 연결된 스키마에 대한 자세한 내용을 보려면 다음 리소스를 사용할 수 있습니다.

- [Cloud Service(클래식) 구성 스키마](schema-cscfg-file.md)
- [Cloud Service(클래식) 정의 스키마](schema-csdef-file.md)
- [Virtual Network(클래식) 만들기](/previous-versions/azure/virtual-network/virtual-networks-create-vnet-classic-pportal)

## <a name="networkconfiguration-element"></a>NetworkConfiguration 요소
다음 예제는 `NetworkConfiguration` 요소와 해당 자식 요소를 보여 줍니다.

```xml
<ServiceConfiguration>
  <NetworkConfiguration>
    <AccessControls>
      <AccessControl name="aclName1">
        <Rule order="<rule-order>" action="<rule-action>" remoteSubnet="<subnet-address>" description="rule-description"/>
      </AccessControl>
    </AccessControls>
    <EndpointAcls>
      <EndpointAcl role="<role-name>" endpoint="<endpoint-name>" accessControl="<acl-name>"/>
    </EndpointAcls>
    <Dns>
      <DnsServers>
        <DnsServer name="<server-name>" IPAddress="<server-address>" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSite name="Group <RG-VNet> <VNet-name>"/>
    <AddressAssignments>
      <InstanceAddress roleName="<role-name>">
        <Subnets>
          <Subnet name="<subnet-name>"/>
        </Subnets>
      </InstanceAddress>
      <ReservedIPs>
        <ReservedIP name="<reserved-ip-name>"/>
      </ReservedIPs>
    </AddressAssignments>
  </NetworkConfiguration>
</ServiceConfiguration>
```

다음 테이블에서는 `NetworkConfiguration` 요소의 자식 요소에 대해 설명합니다.

| 요소       | 설명 |
| ------------- | ----------- |
| AccessControl | 선택 사항입니다. 클라우드 서비스에서 엔드포인트에 대한 액세스 규칙을 지정합니다. 액세스 제어 이름은 `name` 특성에 대한 문자열로 정의됩니다. `AccessControl` 요소는 하나 이상의 `Rule` 요소를 포함합니다. 둘 이상의 `AccessControl` 요소를 정의할 수 있습니다.|
| 규칙 | 선택 사항입니다. IP 주소의 지정된 서브넷 범위에 대해 수행해야 하는 동작을 지정합니다. 규칙의 순서는 `order` 특성에 대한 문자열 값으로 정의됩니다. 규칙 번호가 낮을수록 우선 순위가 높습니다. 예를 들어 규칙을 순서 번호 100, 200 및 300으로 지정할 수 있습니다. 순서 번호가 100인 규칙은 순서가 200인 규칙보다 우선합니다.<br /><br /> 규칙에 대한 동작은 `action` 특성에 대한 문자열로 정의됩니다. 가능한 값은<br /><br /> -   `permit` - 지정된 서브넷 범위의 패킷만 엔드포인트와 통신할 수 있음을 지정합니다.<br />-   `deny` - 지정된 서브넷 범위의 엔드포인트에 대한 액세스가 거부되었음을 지정합니다.<br /><br /> 규칙의 영향을 받는 IP 주소의 서브넷 범위는 `remoteSubnet` 특성에 대한 문자열로 정의됩니다. 규칙에 대한 설명은 `description` 특성에 대한 문자열로 정의됩니다.|
| EndpointAcl | 선택 사항입니다. 엔드포인트에 대한 액세스 제어 규칙의 할당을 지정합니다. 엔드포인트를 포함하는 역할의 이름은 `role` 특성에 대한 문자열로 정의됩니다. 엔드포인트의 이름은 `endpoint` 특성에 대한 문자열로 정의됩니다. 엔드포인트에 적용되어야 하는 `AccessControl` 규칙 집합의 이름은 `accessControl` 특성에 대한 문자열로 정의됩니다. 둘 이상의 `EndpointAcl` 요소를 정의할 수 있습니다.|
| DnsServer | 선택 사항입니다. DNS 서버에 대한 설정을 지정합니다. Virtual Network 없이 DNS 서버에 대한 설정을 지정할 수 있습니다. DNS 서버의 이름은 `name` 특성에 대한 문자열로 정의됩니다. DNS 서버의 IP 주소는 `IPAddress` 특성에 대한 문자열로 정의됩니다. IP 주소는 유효한 IPv4 주소여야 합니다.|
| VirtualNetworkSite | 선택 사항입니다. 클라우드 서비스를 배포하려는 Virtual Network 사이트의 이름을 지정합니다. 이 설정은 Virtual Network 사이트를 만들지 않습니다. Virtual Network에 대한 네트워크 파일에 이전에 정의되어 있는 사이트를 참조합니다. 클라우드 서비스는 하나의 Virtual Network의 멤버일 수 있습니다. 이 설정을 지정하지 않으면 클라우드 서비스가 Virtual Network에 배포되지 않습니다. Virtual Network 사이트의 이름은 `name` 특성에 대한 문자열로 정의됩니다.|
| InstanceAddress | 선택 사항입니다. Virtual Network의 서브넷 또는 서브넷 집합에 대한 역할의 연결을 지정합니다. 역할 이름을 인스턴스 주소에 연결할 때 이 역할을 연결할 서브넷을 지정할 수 있습니다. `InstanceAddress`에는 Subnets 요소가 포함됩니다. 서브넷에 연결되는 역할의 이름은 `roleName` 특성에 대한 문자열로 정의됩니다.|
| 서브넷 | 선택 사항입니다. 네트워크 구성 파일에서 서브넷 이름에 해당하는 서브넷을 지정합니다. 서브넷의 이름은 `name` 특성에 대한 문자열로 정의됩니다.|
| ReservedIP | 선택 사항입니다. 배포와 연결해야 하는 예약된 IP 주소를 지정합니다. 예약된 IP 주소 만들기를 사용하여 예약된 IP 주소를 만들어야 합니다. 클라우드 서비스의 각 배포는 하나의 예약된 IP 주소와 연결할 수 있습니다. 예약된 IP 주소의 이름은 `name` 특성에 대한 문자열로 정의됩니다.|

## <a name="see-also"></a>참고 항목
[Cloud Service(클래식) 구성 스키마](schema-cscfg-file.md)