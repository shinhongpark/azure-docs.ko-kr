---
title: Azure Private Link란?
description: Azure Private Link 기능, 아키텍처 및 구현에 대한 개요입니다. Azure 프라이빗 엔드포인트와 Azure Private Link 서비스의 작동 방식 및 사용 방법을 알아봅니다.
services: private-link
author: malopMSFT
ms.service: private-link
ms.topic: overview
ms.date: 09/03/2020
ms.author: allensu
ms.custom: fasttrack-edit, references_regions
ms.openlocfilehash: b3ca4f11b02f32e65cf80adc65ec12d25e6e7905
ms.sourcegitcommit: 65cef6e5d7c2827cf1194451c8f26a3458bc310a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2021
ms.locfileid: "98573176"
---
# <a name="what-is-azure-private-link"></a>Azure Private Link란? 
Azure Private Link를 사용하면 가상 네트워크의 [프라이빗 엔드포인트](private-endpoint-overview.md)를 통해 Azure PaaS Services(예: Azure Storage 및 SQL Database)와 Azure 호스팅 고객 소유/파트너 서비스에 액세스할 수 있습니다.

가상 네트워크와 서비스 사이의 트래픽은 Microsoft 백본 네트워크를 통해 이동합니다. 서비스를 공용 인터넷에 더 이상 노출할 필요가 없습니다. 가상 네트워크에 자체 [프라이빗 링크 서비스](private-link-service-overview.md)를 만들어서 고객에게 제공할 수도 있습니다. Azure Private Link를 사용한 설치 및 소비는 Azure PaaS, 고객 소유 및 공유 파트너 서비스에서 일관적입니다.

> [!IMPORTANT]
> Azure Private Link가 이제 일반 공급됩니다. 프라이빗 엔드포인트 및 Private Link 서비스(표준 부하 분산 장치 뒤의 서비스)가 모두 일반 공급됩니다. 다른 Azure PaaS는 다른 일정에 따라 Azure Private Link에 온보딩됩니다. 이 문서의 [가용성](#availability) 섹션에서 Private Link의 Azure PaaS에 대한 정확한 상태를 확인하세요. 알려진 제한은 [프라이빗 엔드포인트](private-endpoint-overview.md#limitations) 및 [Private Link Service](private-link-service-overview.md#limitations)를 참조하세요. 

:::image type="content" source="./media/private-link-overview/private-link-center.png" alt-text="Azure Portal의 Azure Private Link 센터" border="false":::

## <a name="key-benefits"></a>주요 이점
Azure Private Link는 다음과 같은 이점이 있습니다.  
- **Azure 플랫폼에서 서비스에 비공개로 액세스**: 원본 또는 대상의 공용 IP 주소 없이 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 서비스 공급자는 자체 가상 네트워크에서 서비스를 렌더링할 수 있으며, 소비자는 로컬 가상 네트워크에서 이러한 서비스에 액세스할 수 있습니다. Private Link 플랫폼은 Azure 백본 네트워크를 통해 소비자와 서비스 간의 연결을 처리합니다. 
 
- **온-프레미스 및 피어링된 네트워크** 프라이빗 엔드포인트를 사용하여 온-프레미스에서 ExpressRoute 프라이빗 피어링, VPN 터널 및 피어링된 가상 네트워크를 통해 Azure에서 실행되는 서비스에 액세스할 수 있습니다. 서비스에 연결하기 위해 ExpressRoute Microsoft 피어링을 구성하거나 인터넷을 트래버스할 필요가 없습니다. Private Link는 워크로드를 Azure로 안전하게 마이그레이션하는 방법을 제공합니다.
 
- **데이터 유출 방지**: 프라이빗 엔드포인트는 전체 서비스가 아닌 PaaS 리소스 인스턴스에 매핑됩니다. 소비자는 특정 리소스에만 연결할 수 있습니다. 서비스의 다른 리소스에 대한 액세스는 차단됩니다. 이 메커니즘은 데이터 유출 위험을 방지합니다. 
 
- **글로벌 환경**: 다른 Azure 지역에서 실행되는 서비스에 비공개로 연결할 수 있습니다. 소비자의 가상 네트워크는 A 지역에 있으며, B 지역의 Private Link 뒤에 있는 서비스에 연결할 수 있습니다.  
 
- **사용자 고유의 서비스로 확장**: 동일한 환경과 기능을 사용하여 자체 서비스를 Azure의 소비자에게 비공개로 렌더링할 수 있습니다. 서비스를 표준 Azure Load Balancer 뒤에 배치하여 Private Link에 사용할 수 있습니다. 그러면 소비자는 자체 가상 네트워크에서 프라이빗 엔드포인트를 사용하여 서비스에 직접 연결할 수 있습니다. 승인 호출 흐름을 사용하여 연결 요청을 관리할 수 있습니다. Azure Private Link는 서로 다른 Azure Active Directory 테넌트에 속한 소비자 및 서비스에 대해 작동합니다. 

## <a name="availability"></a>가용성 
 다음 표에는 Private Link 서비스 및 이러한 서비스를 사용할 수 있는 지역이 나열되어 있습니다. 

|지원되는 서비스  |사용 가능한 지역 | 기타 고려 사항 | 상태  |
|:-------------------|:-----------------|:----------------|:--------|
|표준 Azure Load Balancer 뒤에 있는 Private Link 서비스 | 모든 공용 지역<br/> Azure Government 지역<br/>모든 중국 지역  | 표준 Load Balancer에서 지원 | GA <br/> [Private Link 서비스를 만드는 방법을 알아봅니다.](create-private-link-service-portal.md) |
| Azure Blob 스토리지(Data Lake Storage Gen2 포함)       |  모든 공용 지역<br/> Azure Government 지역       |  계정 종류 범용 V2에서 지원 | GA <br/> [Blob 스토리지에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](tutorial-private-endpoint-storage-portal.md)  |
| Azure 파일 | 모든 공용 지역<br/> Azure Government 지역      | |   GA <br/> [Azure Files 네트워크 엔드포인트를 만드는 방법을 알아봅니다.](../storage/files/storage-files-networking-endpoints.md)   |
| Azure 파일 동기화 | 모든 공용 지역      | |   GA <br/> [Azure Files 네트워크 엔드포인트를 만드는 방법을 알아봅니다.](../storage/files/storage-sync-files-networking-endpoints.md)   |
| Azure Queue 스토리지       |  모든 공용 지역<br/> Azure Government 지역       |  계정 종류 범용 V2에서 지원 | GA <br/> [큐 스토리지에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](tutorial-private-endpoint-storage-portal.md) |
| Azure Table Storage       |  모든 공용 지역<br/> Azure Government 지역       |  계정 종류 범용 V2에서 지원 | GA <br/> [테이블 스토리지에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](tutorial-private-endpoint-storage-portal.md)  |
|  Azure SQL Database         | 모든 공용 지역 <br/> Azure Government 지역<br/>모든 중국 지역      |  프록시 [연결 정책](../azure-sql/database/connectivity-architecture.md#connection-policy)에 대해 지원됨 | GA <br/> [Azure SQL에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](create-private-endpoint-portal.md)      |
|Azure Synapse Analytics| 모든 공용 지역 <br/> Azure Government 지역 |  프록시 [연결 정책](../azure-sql/database/connectivity-architecture.md#connection-policy)에 대해 지원됨 |GA <br/> [Azure Synapse Analytics에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../azure-sql/database/private-endpoint-overview.md)|
|Azure Cosmos DB|  모든 공용 지역<br/> Azure Government 지역</br> 모든 중국 지역 | |GA <br/> [Cosmos DB에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](./tutorial-private-endpoint-cosmosdb-portal.md)|
|  Azure Database for PostgreSQL - 단일 서버         | 모든 공용 지역 <br/> Azure Government 지역<br/>모든 중국 지역     | 범용 및 메모리 최적화된 가격 책정 계층에 지원됨 | GA <br/> [Azure Database for PostgreSQL에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../postgresql/concepts-data-access-and-security-private-link.md)      |
|  Azure Database for MySQL         | 모든 공용 지역<br/> Azure Government 지역<br/>모든 중국 지역      |  | GA <br/> [Azure Database for MySQL에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../mysql/concepts-data-access-security-private-link.md)     |
|  Azure Database for MariaDB         | 모든 공용 지역<br/> Azure Government 지역<br/>모든 중국 지역     |  | GA <br/> [Azure Database for MariaDB에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../mariadb/concepts-data-access-security-private-link.md)      |
|  Azure Key Vault         | 모든 공용 지역<br/> Azure Government 지역      |  | GA   <br/> [Azure Key Vault에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../key-vault/general/private-link-service.md)   |
|Azure Kubernetes Service - Kubernetes API | 모든 공용 지역      |  | GA   <br/> [Azure Kubernetes Service에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../aks/private-clusters.md)   |
|Azure Search | 모든 공용 지역 <br/> Azure Government 지역 | 개인 모드 서비스에서 지원됨 | GA   <br/> [Azure Search에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../search/service-create-private-endpoint.md)    |
|Azure Container Registry | 모든 공용 지역<br/> Azure Government 지역    | 컨테이너 레지스트리의 프리미엄 계층에서 지원됨 [계층 선택](../container-registry/container-registry-skus.md)| GA   <br/> [Azure Container Registry에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../container-registry/container-registry-private-link.md)   |
|Azure App Configuration | 모든 공용 지역      |  | 미리 보기  </br> [Azure App Configuration에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../azure-app-configuration/concept-private-endpoint.md) |
|Azure Backup | 모든 공용 지역<br/> Azure Government 지역   |  | GA   <br/> [Azure Backup에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../backup/private-endpoints.md)   |
|Azure Event Hub | 모든 공용 지역<br/>Azure Government 지역      |   | GA   <br/> [Azure Event Hub에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../event-hubs/private-link-service.md)  |
|Azure Service Bus | 모든 공용 지역<br/>Azure Government 지역  | Azure Service Bus의 프리미엄 계층에서 지원됩니다. [계층 선택](../service-bus-messaging/service-bus-premium-messaging.md) | GA   <br/> [Azure Service Bus에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../service-bus-messaging/private-link-service.md)    |
|Azure Relay | 모든 공용 지역      |  | 미리 보기 <br/> [Azure Relay에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../azure-relay/private-link-service.md)  |
|Azure Event Grid| 모든 공용 지역<br/> Azure Government 지역       |  | GA   <br/> [Azure Event Grid에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../event-grid/network-security.md) |
|Azure Web Apps | 모든 공용 지역      | PremiumV2, PremiumV3 또는 함수 프리미엄 계획에서 지원됨  | GA   <br/> [Azure Web Apps에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](./tutorial-private-endpoint-webapp-portal.md)   |
|Azure Machine Learning | 모든 공용 지역    |  | GA   <br/> [Azure Machine Learning에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../machine-learning/how-to-configure-private-link.md)   |
| Azure Automation  | 모든 공용 지역<br/> Azure Government 지역 |  | 미리 보기 </br> [Azure Automation에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../automation/how-to/private-link-security.md)| |
| Azure IoT Hub | 모든 공용 지역    |  | GA   <br/> [Azure IoT Hub에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../iot-hub/virtual-network-support.md) |
| Azure SignalR | 미국 동부, 미국 중남부,<br/>미국 서부 2, 모든 중국 지역      |  | 미리 보기   <br/> [Azure SignalR에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../azure-signalr/howto-private-endpoints.md)   |
| Azure Monitor <br/>(Log Analytics 및 Application Insights) | 모든 공용 지역      |  | GA   <br/> [Azure Monitor에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../azure-monitor/platform/private-link-security.md)   | 
| Azure Batch | 다음을 제외한 모든 공용 지역: 독일 중부, 독일 북동부 <br/> Azure Government 지역  | | GA <br/> [Azure Batch에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../batch/private-connectivity.md) |
|Azure 데이터 팩터리 | 모든 공용 지역<br/> Azure Government 지역<br/>모든 중국 지역    | 자격 증명을 Azure key vault에 저장해야 합니다.| GA   <br/> [Azure Data Factory에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](../data-factory/data-factory-private-link.md)   |
|Azure Managed Disks | 모든 공용 지역<br/> Azure Government 지역<br/>모든 중국 지역    | [알려진 제한 사항을 보려면 여기를 클릭하세요.](https://docs.microsoft.com/azure/virtual-machines/disks-enable-private-links-for-import-export-portal#limitations) | GA   <br/> [Azure Managed Disks에 대한 프라이빗 엔드포인트를 만드는 방법을 알아봅니다.](https://docs.microsoft.com/azure/virtual-machines/disks-enable-private-links-for-import-export-portal)   |



최신 알림은 [Azure Private Link 업데이트 페이지](https://azure.microsoft.com/updates/?product=private-link)를 확인하세요.

## <a name="logging-and-monitoring"></a>로깅 및 모니터링

Azure Private Link는 Azure Monitor와 통합되었습니다. 이 조합을 통해 다음을 수행할 수 있습니다.

 - 스토리지 계정에 로그를 보관합니다.
 - 이벤트를 Event Hubs로 스트리밍합니다.
 - Azure Monitor 로깅이 가능합니다.

Azure Monitor에서 다음 정보에 액세스할 수 있습니다. 
- **프라이빗 엔드포인트**: 
    - 프라이빗 엔드포인트에서 처리한 데이터(수신/송신)
 
- **Private Link 서비스**:
    - Private Link 서비스에서 처리한 데이터(수신/송신)
    - NAT 포트 가용성  
 
## <a name="pricing"></a>가격 책정   
가격 책정에 대한 자세한 내용은 [Azure Private Link 가격 책정](https://azure.microsoft.com/pricing/details/private-link/)을 참조하세요.
 
## <a name="faqs"></a>FAQ  
FAQ는 [Azure Private Link FAQ](private-link-faq.md)를 참조하세요.
 
## <a name="limits"></a>제한  
제한은 [Azure Private Link 제한](../azure-resource-manager/management/azure-subscription-service-limits.md#private-link-limits)을 참조하세요.

## <a name="service-level-agreement"></a>서비스 수준 계약
SLA는 [Azure Private Link에 대한 SLA](https://azure.microsoft.com/support/legal/sla/private-link/v1_0/)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [빠른 시작: Azure Portal을 사용하여 프라이빗 엔드포인트 만들기l](create-private-endpoint-portal.md)
- [빠른 시작: Azure Portal을 사용하여 Private Link 서비스 만들기](create-private-link-service-portal.md)


