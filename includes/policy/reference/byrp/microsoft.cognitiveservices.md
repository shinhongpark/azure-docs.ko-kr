---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 01/21/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 37d6380e8955e02e96383592b48a9e54cdf30145
ms.sourcegitcommit: 75041f1bce98b1d20cd93945a7b3bd875e6999d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2021
ms.locfileid: "98701937"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Cognitive Services 계정은 데이터 암호화를 사용하도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2bdd0062-9d75-436e-89df-487dd8e4b3c7) |이 정책은 데이터 암호화를 사용하지 않는 모든 Cognitive Services 계정을 감사합니다. 스토리지를 사용하는 각 Cognitive Services 계정에 대해 고객 관리형 키 또는 Microsoft 관리형 키로 데이터 암호화를 사용하도록 설정해야 합니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_Encryption_Audit.json) |
|[Cognitive Services 계정은 CMK (고객이 관리 하는 키)를 사용 하 여 데이터 암호화를 사용 하도록 설정 해야 합니다.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F67121cc7-ff39-4ab8-b7e3-95b84dab487d) |CMK(고객 관리형 키)는 일반적으로 규정 준수 표준을 충족하는 데 필요합니다. CMK를 사용하면 Cognitive Services에 저장된 데이터를 사용자가 만들고 소유한 Azure Key Vault 키로 데이터를 암호화할 수 있습니다. 순환 및 관리를 포함하여 키의 수명 주기를 고객이 모두 제어하고 책임져야 합니다. [https://aka.ms/cosmosdb-cmk](https://aka.ms/cosmosdb-cmk)에서 CMK 암호화에 대해 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_CustomerManagedKey_Audit.json) |
|[Cognitive Services 계정은 네트워크 액세스를 제한해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F037eea7a-bd0a-46c5-9a66-03aea78705d3) |Cognitive Services 계정에 대한 네트워크 액세스는 제한되어야 합니다. 허용되는 네트워크의 애플리케이션만 Cognitive Services 계정에 액세스할 수 있도록 네트워크 규칙을 구성합니다. 특정 인터넷 또는 온-프레미스 클라이언트의 연결을 허용하기 위해 특정 Azure 가상 네트워크에서의 트래픽 또는 공용 인터넷 IP 주소 범위에 액세스 권한을 부여할 수 있습니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_NetworkAcls_Audit.json) |
|[Cognitive Services 계정은 고객 소유 스토리지를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F46aa9b05-0e60-4eae-a88b-1e9d374fa515) |이 정책은 고객 소유 스토리지를 사용하지 않는 모든 Cognitive Services 계정을 감사합니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_UserOwnedStorage_Audit.json) |
|[Cognitive Services 계정은 고객 소유 스토리지를 사용하거나 데이터 암호화를 사용하도록 설정해야 합니다.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F11566b39-f7f7-4b82-ab06-68d8700eb0a4) |이 정책은 고객 소유 스토리지 또는 데이터 암호화를 사용하지 않는 모든 Cognitive Services 계정을 감사합니다. 스토리지를 사용하는 각 Cognitive Services 계정에 대해 고객 소유 스토리지를 사용하거나 데이터 암호화를 사용하도록 설정합니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_BYOX_Audit.json) |
|[Cognitive Services 계정에 대해 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0725b4dd-7e76-479c-a735-68e7ee23d5ca) |이 정책은 공용 네트워크 액세스가 활성화된 환경에서 Cognitive Services 계정을 감사합니다. 프라이빗 엔드포인트에서의 연결만 허용되도록 공용 네트워크 액세스를 사용하지 않도록 설정해야 합니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Cognitive%20Services/CognitiveServices_DisablePublicNetworkAccess_Audit.json) |
