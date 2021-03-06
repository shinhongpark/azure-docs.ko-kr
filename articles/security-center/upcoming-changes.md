---
title: Azure Security Center에 예정된 중요한 변경
description: 알아야 하고 계획해야 할 수 있는 Azure Security Center에 예정된 변경입니다
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/18/2021
ms.author: memildin
ms.openlocfilehash: ba9a640c2231c7098e58ad6e29bbfa196436a7f9
ms.sourcegitcommit: 61d2b2211f3cc18f1be203c1bc12068fc678b584
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98562321"
---
# <a name="important-upcoming-changes-to-azure-security-center"></a>Azure Security Center에 예정된 중요한 변경

> [!IMPORTANT]
> 이 페이지의 정보는 시험판 제품 또는 기능과 관련이 있으며, 이는 상업적으로 릴리스되기 전에 대폭 수정될 수 있습니다. Microsoft는 여기에 제공된 정보와 관련하여 어떠한 명시적 또는 묵시적 약속 또는 보증도 하지 않습니다.

이 페이지에서는 Security Center에 계획된 변경에 대해 알아봅니다. 보안 점수 또는 워크플로와 같은 항목에 영향을 줄 수 있는 제품에 대한 계획된 수정을 설명합니다.

최신 릴리스 정보를 찾고 있으면 [Azure Security Center의 새로운 기능](release-notes.md)에서 확인할 수 있습니다.


## <a name="planned-changes"></a>계획된 변경

- [더 이상 사용되지 않는 "시스템 업데이트 적용" 보안 제어의 두 가지 권장 사항](#two-recommendations-from-apply-system-updates-security-control-being-deprecated)
- [SQL 데이터 분류 권장 사항 향상](#enhancements-to-sql-data-classification-recommendation)
- [Azure Policy 평가에서 "규정 준수"로 보고되는 "해당 없음" 리소스](#not-applicable-resources-to-be-reported-as-compliant-in-azure-policy-assessments)
- [Azure 보안 벤치마크의 적용 범위를 늘리기 위해 35개의 미리 보기 추천 사항이 추가됨](#35-preview-recommendations-being-added-to-increase-coverage-of-azure-security-benchmark)


### <a name="two-recommendations-from-apply-system-updates-security-control-being-deprecated"></a>더 이상 사용되지 않는 "시스템 업데이트 적용" 보안 제어의 두 가지 권장 사항 

**변경 예상 날짜:** 2021년 2월

다음 두 가지 권장 사항은 2021년 2월에 더 이상 사용되지 않을 예정입니다.

- **시스템 업데이트를 적용하려면 머신을 다시 시작해야 합니다**. 이로 인해 보안 점수에 약간의 영향을 줄 수 있습니다.
- **머신에 모니터링 에이전트를 설치해야 합니다**. 이 권장 사항은 온-프레미스 머신에만 관련되며 해당 논리의 일부는 다른 권장 사항으로 전송됩니다. **Log Analytics 에이전트 상태 문제는 머신에서 해결해야 합니다**. 이로 인해 보안 점수에 약간의 영향을 줄 수 있습니다.

연속 내보내기 및 워크플로 자동화 구성을 확인하여 이러한 권장 사항이 포함되어 있는지 확인하는 것이 좋습니다. 또한 대시보드 또는 이를 사용할 수 있는 기타 모니터링 도구를 적절하게 업데이트해야 합니다.

[보안 추천 사항 참조 페이지](recommendations-reference.md)에서 이러한 권장 사항에 대해 자세히 알아보세요.


### <a name="enhancements-to-sql-data-classification-recommendation"></a>SQL 데이터 분류 권장 사항 향상

**변경 예상 날짜:** Q2 2021

**데이터 분류 적용** 보안 제어에서 권장 사항 **SQL 데이터베이스의 중요 데이터를 분류해야 함** 의 현재 버전은 더 이상 사용되지 않으며 Microsoft의 데이터 분류 전략에 맞춰 향상된 새 버전으로 대체됩니다. 결과는 다음과 같습니다.

- 권장 사항은 더 이상 보안 점수에 영향을 주지 않습니다.
- 보안 제어("데이터 분류 적용")는 더 이상 보안 점수에 영향을 주지 않습니다.
- 권장 사항의 ID도 변경됩니다(현재 b0df6f56-862d-4730-8597-38c0fd4ebd59).



### <a name="not-applicable-resources-to-be-reported-as-compliant-in-azure-policy-assessments"></a>Azure Policy 평가에서 "규정 준수"로 보고되는 "해당 없음" 리소스

**변경 예상 날짜:** 2021년 1월

현재 권장 사항에 대해 평가되고 **해당 없음** 으로 확인된 리소스는 Azure Policy에 "비규격"으로 표시됩니다. 어떤 사용자 작업도 상태를 "규정 준수"로 변경할 수 없습니다. 이 계획된 변경 내용에 따라 명확하게 개선하기 위해 "규정 준수"로 보고됩니다.

규정 준수 리소스의 수가 증가하는 Azure Policy에만 영향을 줍니다. Azure Security Center의 보안 점수에는 영향을 주지 않습니다.

### <a name="35-preview-recommendations-being-added-to-increase-coverage-of-azure-security-benchmark"></a>Azure 보안 벤치마크의 적용 범위를 늘리기 위해 35개의 미리 보기 추천 사항이 추가됨

**변경 예상 날짜:** 2021년 1월

Azure 보안 벤치마크는 일반적인 규정 준수 프레임워크를 기반으로 하는 보안 및 규정 준수 모범 사례에 대해 Microsoft에서 작성한 Azure 관련 지침 세트입니다. [Azure 보안 벤치마크에 대해 자세히 알아보세요](../security/benchmarks/introduction.md).

이 벤치마크의 적용 범위를 넓히기 위해 다음 35개의 새로운 추천 사항이 Security Center에 추가됩니다.

미리 보기 추천 사항은 리소스를 비정상으로 렌더링하지 않으며 보안 점수 계산에 포함되지 않습니다. 미리 보기 기간이 끝나면 점수에 기여할 수 있도록 가능한 경우 언제든지 수정합니다. [Azure Security Center의 추천 사항 수정](security-center-remediate-recommendations.md)에서 이러한 추천 사항에 대응하는 방법에 대해 자세히 알아보세요.

| 보안 컨트롤                     | 새로운 권장 사항                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 저장 데이터 암호화 사용            | - Azure Cosmos DB 계정은 고객 관리형 키를 사용하여 미사용 데이터를 암호화해야 함<br>- Azure Machine Learning 작업 영역은 CMK(고객 관리형 키)를 사용하여 암호화해야 함<br>- MySQL 서버에 대해 BYOK(Bring Your Own Key) 데이터 보호를 사용하도록 설정해야 함<br>- PostgreSQL 서버에 대해 BYOK(Bring Your Own Key) 데이터 보호를 사용하도록 설정해야 함<br>- Cognitive Services 계정은 CMK(고객 관리형 키)로 데이터 암호화를 사용하도록 설정해야 함<br>- 컨테이너 레지스트리는 CMK(고객 관리형 키)로 암호화해야 함<br>- SQL Managed Instance는 고객 관리형 키를 사용하여 미사용 데이터를 암호화해야 함<br>- SQL Server는 고객 관리형 키를 사용하여 미사용 데이터를 암호화해야 함<br>- 스토리지 계정은 암호화에 CMK(고객 관리형 키)를 사용해야 함                                                                                                                                                              |
| 보안 모범 사례 구현    | - 구독에 보안 문제에 대한 연락처 이메일 주소가 있어야 함<br> - 구독에 Log Analytics 에이전트의 자동 프로비저닝을 사용하도록 설정해야 함<br> - 심각도가 높은 경고에 대해 이메일 알림을 사용하도록 설정해야 함<br> - 심각도가 높은 경고에 대해 구독 소유자에게 이메일 알림을 사용하도록 설정해야 함<br> - 키 자격 증명 모음에 제거 방지를 사용하도록 설정해야 함<br> - 키 자격 증명 모음에 일시 삭제를 사용하도록 설정해야 함 |
| 액세스 및 사용 권한 관리        | - 함수 앱은 '클라이언트 인증서(들어오는 클라이언트 인증서)'를 사용하도록 설정해야 함 |
| DDoS 공격으로부터 애플리케이션 보호 | - Application Gateway에 WAF(웹 애플리케이션 방화벽)를 사용하도록 설정해야 함<br> - Azure Front Door Service 서비스에 대해 WAF(Web Application Firewall)를 사용하도록 설정해야 함 |
| 무단 네트워크 액세스 제한 | - Key Vault에서 방화벽을 사용하도록 설정해야 함<br> - Key Vault의 프라이빗 엔드포인트를 구성해야 함<br> - App Configuration은 프라이빗 링크를 사용해야 함<br> - Azure Cache for Redis는 가상 네트워크 내에 있어야 함<br> - Azure Event Grid 도메인은 프라이빗 링크를 사용해야 함<br> - Azure Event Grid 토픽은 프라이빗 링크를 사용해야 함<br> - Azure Machine Learning 작업 영역은 프라이빗 링크를 사용해야 함<br> - Azure SignalR Service는 프라이빗 링크를 사용해야 함<br> - Azure Spring Cloud는 네트워크 주입을 사용해야 함<br> - 컨테이너 레지스트리는 무제한 네트워크 액세스를 허용하지 않아야 함<br> - 컨테이너 레지스트리는 프라이빗 링크를 사용해야 함<br> - MariaDB 서버에 대해 공용 네트워크 액세스를 사용하지 않도록 설정해야 함<br> - MySQL 서버에 대해 공용 네트워크 액세스를 사용하지 않도록 설정해야 함<br> - PostgreSQL 서버에 대해 공용 네트워크 액세스를 사용하지 않도록 설정해야 함<br> - 스토리지 계정은 프라이빗 링크 연결을 사용해야 함<br> - 스토리지 계정은 가상 네트워크 규칙을 사용하여 네트워크 액세스를 제한해야 함<br> - VM Image Builder 템플릿은 프라이빗 링크를 사용해야 함|
|                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

관련 링크:

- [Azure 보안 벤치마크에 대한 자세한 정보](../security/benchmarks/introduction.md)
- [Azure Database for MariaDB에 대한 자세한 정보](../mariadb/overview.md)
- [Azure Database for MySQL에 대한 자세한 정보](../mysql/overview.md)
- [Azure Database for PostgreSQL에 대한 자세한 정보](../postgresql/overview.md)





## <a name="next-steps"></a>다음 단계

제품에 대한 모든 최근 변경 내용은 [Azure Security Center의 새로운 기능](release-notes.md)을 참조하세요.