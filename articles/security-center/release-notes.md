---
title: Azure Security Center에 대한 릴리스 정보
description: Azure Security Center의 새로운 기능과 변경된 기능에 대한 설명
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/17/2021
ms.author: memildin
ms.openlocfilehash: 48e7093c30ffb135231f5843cb0767848f242d89
ms.sourcegitcommit: 949c0a2b832d55491e03531f4ced15405a7e92e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98541389"
---
# <a name="whats-new-in-azure-security-center"></a>Azure Security Center의 새로운 기능

Security Center는 현재 개발 중이며 지속적으로 향상된 기능을 수용합니다. 이 페이지에서는 최신 개발 정보를 제공하기 위해 새로운 기능, 버그 수정 및 사용되지 않는 기능에 대한 정보를 제공합니다.

이 페이지는 자주 업데이트되므로 자주 다시 방문하세요. 

곧 Security Center에 적용되는 *계획된* 변경 내용에 대한 자세한 내용은 [Azure Security Center의 예정된 중요 변경 내용](upcoming-changes.md)을 참조하세요. 

> [!TIP]
> 6개월 이상된 항목을 찾으려는 경우 [Azure Security Center의 새로운 기능 아카이브](release-notes-archive.md)에서 찾을 수 있습니다.


## <a name="january-2021"></a>2021년 1월

12월의 업데이트는 다음과 같습니다.

- [필터링된 권장 목록의 CSV 내보내기](#csv-export-of-filtered-list-of-recommendations)
- [온-프레미스 및 다중 클라우드 머신의 취약성 평가가 일반 공급됨](#vulnerability-assessment-for-on-premise-and-multi-cloud-machines-is-generally-available)


### <a name="csv-export-of-filtered-list-of-recommendations"></a>필터링된 권장 목록의 CSV 내보내기 

2020년 11월에 권장 사항 페이지에 필터를 추가했습니다([이제 권장 목록에 필터가 포함됨](#recommendations-list-now-includes-filters)). 12월에 이러한 필터를 확장했습니다([권장 사항 페이지에는 환경, 심각도 및 사용 가능한 응답에 대한 새 필터가 있음](#recommendations-page-has-new-filters-for-environment-severity-and-available-responses)). 

이 공지 사항에서는 **CSV로 다운로드** 단추의 동작을 변경하여 CSV 내보내기에 현재 필터링된 목록에 표시된 권장 사항만 포함되도록 합니다. 

예를 들어 아래 이미지에서 목록이 두 가지 권장 사항으로 필터링된 것을 볼 수 있습니다. 생성된 CSV 파일에는 이러한 두 가지 권장 사항이 적용되는 모든 리소스에 대한 상태 정보가 포함됩니다.   

:::image type="content" source="media/security-center-managing-and-responding-alerts/export-to-csv-with-filters.png" alt-text="필터링된 권장 사항을 CSV 파일로 내보내기":::

[Azure Security Center의 보안 권장 사항](security-center-recommendations.md)에서 자세히 알아보세요.

### <a name="vulnerability-assessment-for-on-premise-and-multi-cloud-machines-is-generally-available"></a>온-프레미스 및 다중 클라우드 머신의 취약성 평가가 일반 공급됨

당사는 10월에 [서버용 Azure Defender](defender-for-servers-introduction.md)의 통합 취약성 평가 스캐너(Qualys 기반)로 Azure Arc 사용 서버를 검색하는 기능의 미리 보기를 발표했습니다.

이 기능은 이제 일반 공급됩니다. 

Azure가 아닌 머신에서 Azure Arc를 사용하도록 설정한 경우 Security Center는 이러한 머신에 통합 취약성 스캐너를 수동 및 대규모로 배포할 수 있습니다.

이번 업데이트를 통해 모든 Azure 및 비-Azure 자산의 취약성 관리 프로그램을 통합하는 **서버용 Azure Defender** 의 강력한 성능을 발휘할 수 있습니다.

주요 기능:

- Azure Arc 머신의 VA(취약성 평가) 스캐너 프로비저닝 상태 모니터링
- 보호되지 않는 Windows 및 Linux Azure Arc 머신에 통합 VA 에이전트 프로비저닝(수동 및 대규모로)
- 배포된 에이전트에서 탐지된 취약성 수신 및 분석(수동 및 대규모로)
- Azure VM 및 Azure Arc 머신에 대한 통합 환경

[하이브리드 머신에 통합 취약성 스캐너를 배포하는 내용을 자세히 알아보세요](deploy-vulnerability-assessment-vm.md#deploy-the-integrated-scanner-to-your-azure-and-hybrid-machines).

[Azure Arc 사용 서버에 대해 자세히 알아보세요](../azure-arc/servers/index.yml).


## <a name="december-2020"></a>2020년 12월

12월의 업데이트는 다음과 같습니다.

- [머신의 SQL 서버용 Azure Defender를 일반적으로 사용할 수 있습니다.](#azure-defender-for-sql-servers-on-machines-is-generally-available)
- [Azure Synapse Analytics 전용 SQL 풀에 대한 Azure Defender for SQL 지원이 일반적으로 제공됩니다.](#azure-defender-for-sql-support-for-azure-synapse-analytics-dedicated-sql-pool-is-generally-available)
- [전역 관리자는 이제 자신에게 테넌트 수준 권한을 부여할 수 있습니다.](#global-administrators-can-now-grant-themselves-tenant-level-permissions)
- [새로운 두 가지 Azure Defender 계획: Azure Defender for DNS 및 Azure Defender for Resource Manager(미리 보기)](#two-new-azure-defender-plans-azure-defender-for-dns-and-azure-defender-for-resource-manager-in-preview)
- [Azure Portal의 새 보안 경고 페이지(미리 보기)](#new-security-alerts-page-in-the-azure-portal-preview)
- [Azure SQL Database & SQL Managed Instance의 재활성화된 Security Center 환경](#revitalized-security-center-experience-in-azure-sql-database--sql-managed-instance)
- [자산 인벤토리 도구 및 필터 업데이트됨](#asset-inventory-tools-and-filters-updated)
- [SSL 인증서를 요청하는 웹앱에 대한 권장 사항은 더 이상 보안 점수에 포함되지 않음](#recommendation-about-web-apps-requesting-ssl-certificates-no-longer-part-of-secure-score)
- [권장 사항 페이지에는 환경, 심각도 및 사용 가능한 응답에 대한 새 필터가 있음](#recommendations-page-has-new-filters-for-environment-severity-and-available-responses)
- [연속 내보내기는 새 데이터 형식 및 향상된 deployifnotexist 정책을 가져옴](#continuous-export-gets-new-data-types-and-improved-deployifnotexist-policies)


### <a name="azure-defender-for-sql-servers-on-machines-is-generally-available"></a>머신의 SQL 서버용 Azure Defender를 일반적으로 사용할 수 있습니다.

Azure Security Center는 SQL Server에 대한 두 가지 Azure Defender 플랜을 제공합니다.

- **Azure SQL 데이터베이스 서버용 Azure Defender** - Azure 네이티브 SQL Server 방어 
- **머신의 SQL 서버용 Azure Defender** - 하이브리드, 다중 클라우드 및 온-프레미스 환경의 SQL 서버로 동일한 보호를 확장합니다.

이 공지를 통해 **Azure Defender for SQL** 은 이제 데이터베이스와 해당 데이터가 어디에 있든 보호합니다.

Azure Defender for SQL에는 취약성 평가 기능이 포함되어 있습니다. 취약성 평가 도구에는 다음과 같은 고급 기능이 포함되어 있습니다.

- **기본 구성**(신규!)을 통해 취약성 검색 결과를 실제 보안 문제를 나타낼 수 있는 결과로 지능적으로 구체화할 수 있습니다. 기본 보안 상태를 설정한 후 취약성 평가 도구는 해당 기준 상태의 편차만 보고합니다. 기준과 일치하는 결과는 후속 검색을 통과한 것으로 간주됩니다. 이를 통해 사용자와 분석가는 중요한 부분에 집중할 수 있습니다.
- 검색된 결과 및 리소스와 관련된 이유를 *이해* 하는 데 도움이 되는 **자세한 벤치마크 정보**.
- 식별된 위험을 완화하는 데 도움이 되는 **수정 스크립트**.

[Azure Defender for SQL](defender-for-sql-introduction.md)에 대해 자세히 알아봅니다.


### <a name="azure-defender-for-sql-support-for-azure-synapse-analytics-dedicated-sql-pool-is-generally-available"></a>Azure Synapse Analytics 전용 SQL 풀에 대한 Azure Defender for SQL 지원이 일반적으로 제공됩니다.

Azure Synapse Analytics(이전의 SQL DW)는 엔터프라이즈 데이터 웨어하우징과 빅 데이터 분석을 결합한 분석 서비스입니다. 전용 SQL 풀은 Azure Synapse의 엔터프라이즈 데이터 웨어하우징 기능입니다. [Azure Synapse Analytics(이전의 SQL DW)란?](../synapse-analytics/sql-data-warehouse/sql-data-warehouse-overview-what-is.md)에서 자세히 알아봅니다.

Azure Defender for SQL은 다음을 통해 전용 SQL 풀을 보호합니다.

- 위협 및 공격을 감지하는 **지능형 위협 방지** 
- 보안 오류를 식별하고 수정하기 위한 **취약성 평가 기능**

Azure Synapse Analytics SQL 풀에 대한 Azure Defender for SQL의 지원은 Azure Security Center의 Azure SQL 데이터베이스 번들에 자동으로 추가됩니다. Azure Portal의 Synapse 작업 영역 페이지에 새로운 "Azure Defender for SQL" 탭을 찾을 수 있습니다.

[Azure Defender for SQL](defender-for-sql-introduction.md)에 대해 자세히 알아봅니다.


### <a name="global-administrators-can-now-grant-themselves-tenant-level-permissions"></a>전역 관리자는 이제 자신에게 테넌트 수준 권한을 부여할 수 있습니다.

**전역 관리자** 의 Azure Active Directory 역할을 가진 사용자는 테넌트 전체의 책임이 있지만 Azure Security Center에서 해당 조직 전체 정보를 볼 수 있는 Azure 권한은 없습니다. 

자신에게 테넌트 수준 사용 권한을 할당하려면 [자신에게 테넌트 전체 사용 권한 부여](security-center-management-groups.md#grant-tenant-wide-permissions-to-yourself)의 지침을 따르세요.


### <a name="two-new-azure-defender-plans-azure-defender-for-dns-and-azure-defender-for-resource-manager-in-preview"></a>새로운 두 가지 Azure Defender 계획: Azure Defender for DNS 및 Azure Defender for Resource Manager(미리 보기)

Azure 환경을 위한 새로운 두 가지 클라우드 네이티브 너비 위협 방지 기능이 추가되었습니다.

이러한 새로운 보호 기능은 위협 행위자의 공격에 대한 복원력을 크게 향상시키고 Azure Defender로 보호되는 Azure 리소스의 수를 크게 늘립니다.

- **Azure Defender for Resource Manager** - 조직에서 수행되는 모든 리소스 관리 작업을 자동으로 모니터링합니다. 자세한 내용은 다음을 참조하세요.
    - [Azure Defender for Resource Manager 소개](defender-for-resource-manager-introduction.md)
    - [Azure Defender for Resource Manager 경고에 대한 대응](defender-for-resource-manager-usage.md)
    - [Azure Defender for Resource Manager에서 제공하는 경고 목록](alerts-reference.md#alerts-resourcemanager)

- **Azure Defender for DNS** - Azure 리소스의 모든 DNS 쿼리를 지속적으로 모니터링합니다. 자세한 내용은 다음을 참조하세요.
    - [Azure Defender for DNS 소개](defender-for-dns-introduction.md)
    - [Azure Defender for DNS 경고에 대한 대응](defender-for-dns-usage.md)
    - [Azure Defender for DNS에서 제공하는 경고 목록](alerts-reference.md#alerts-dns)


### <a name="new-security-alerts-page-in-the-azure-portal-preview"></a>Azure Portal의 새 보안 경고 페이지(미리 보기)

Azure Security Center의 보안 경고 페이지가 다음을 제공하도록 다시 디자인되었습니다.

- **경고에 대한 향상된 심사 환경** - 경고 피로를 줄이고 가장 관련성이 높은 위협에 더 쉽게 집중하는 데 도움이 됩니다. 목록에는 사용자 지정 가능한 필터 및 그룹화 옵션이 포함되어 있습니다.
- **경고 목록의 추가 정보** - 예: MITRE ATT&ACK 전술
- **샘플 경고를 만드는 단추** - Azure Defender 기능을 평가하고 경고 구성(SIEM 통합, 이메일 알림 및 워크플로 자동화)을 테스트하기 위해 모든 Azure Defender 계획의 샘플 경고를 만들 수 있습니다.
- **Azure Sentinel의 인시던트 환경에 맞춤** - 이제 두 제품을 사용하는 고객이 두 제품 간에 더 직관적으로 전환할 수 있는 환경이 제공되며, 두 제품을 손쉽게 알아볼 수 있습니다.
- 대규모 경고 목록의 **성능 개선**
- 경고 목록 **키보드 탐색**
- **Azure Resource Graph의 경고** - 모든 리소스에 대한 Kusto 같은 API인 Azure Resource Graph에서 경고를 쿼리할 수 있습니다. 이는 자체 경고 대시보드를 빌드하는 경우에도 유용합니다. [Azure Resource Graph에 대한 자세한 정보](../governance/resource-graph/index.yml).

새 환경에 액세스하려면 보안 경고 페이지 맨 위에 있는 배너에서 '지금 사용해 보기' 링크를 사용합니다.

:::image type="content" source="media/security-center-managing-and-responding-alerts/preview-alerts-experience-banner.png" alt-text="새 미리 보기 경고 환경에 대한 링크가 포함된 배너":::

새 경고 환경에서 샘플 경고를 만들려면 [샘플 Azure Defender 경고 생성](security-center-alert-validation.md#generate-sample-azure-defender-alerts)을 참조하세요.


### <a name="revitalized-security-center-experience-in-azure-sql-database--sql-managed-instance"></a>Azure SQL Database & SQL Managed Instance의 재활성화된 Security Center 환경 

SQL 내의 Security Center 환경은 다음과 같은 Security Center 및 Azure Defender for SQL 기능에 대한 액세스를 제공합니다.

- **보안 권장 사항** – Security Center는 연결된 모든 Azure 리소스의 보안 상태를 정기적으로 분석하여 잠재적인 보안 구성 오류를 식별합니다. 그런 다음, 이러한 취약성을 해결하고 조직의 보안 태세를 개선하는 방법에 대한 권장 사항을 제공합니다.
- **보안 경고** - SQL 삽입, 무차별 암호 대입 공격 및 권한 남용 같은 위협에 대해 Azure SQL 활동을 지속적으로 모니터링하는 검색 서비스입니다. 이 서비스는 Security Center에서 세부적이고 작업 지향적인 보안 경고를 트리거하고 Microsoft의 Azure 네이티브 SIEM 솔루션인 Azure Sentinel을 사용하여 지속적으로 조사하기 위한 옵션을 제공합니다.
- **검색 결과** – Azure SQL 구성을 지속적으로 모니터링하고 취약성을 해결하는 데 도움이 되는 취약성 평가 서비스입니다. 평가 검사는 자세한 보안 결과와 함께 Azure SQL 보안 상태의 개요를 제공합니다.     

:::image type="content" source="media/release-notes/azure-security-center-experience-in-sql.png" alt-text="SQL에 대한 Azure Security Center의 보안 기능은 Azure SQL 내에서 사용할 수 있습니다.":::


### <a name="asset-inventory-tools-and-filters-updated"></a>자산 인벤토리 도구 및 필터 업데이트됨

Azure Security Center의 인벤토리 페이지가 다음과 같이 변경되었습니다.

- 도구 모음에 **가이드 및 피드백** 추가. 관련 정보 및 도구에 대한 링크가 포함된 창이 열립니다. 
- 리소스에 사용할 수 있는 기본 필터에 **구독 필터** 추가.
- 현재 필터 옵션을 Azure Resource Graph 쿼리(이전에는 "리소스 그래프 탐색기에서 보기"라고 함)로 열기 위한 **쿼리 열기** 링크.
- 각 필터에 대한 **운영자 옵션**. 이제 '=' 이외의 추가 논리 연산자 중에서 선택할 수 있습니다. 예를 들어, 'encrypt(암호화)' 문자열이 있는 제목을 가진 활성 권장 사항이 있는 모든 리소스를 찾을 수 있습니다. 

    :::image type="content" source="media/release-notes/inventory-filter-operators.png" alt-text="자산 인벤토리 필터의 운영자 옵션에 대한 컨트롤":::

[자산 인벤토리를 사용하여 리소스 검색 및 관리](asset-inventory.md)에서 인벤토리에 대해 자세히 알아보세요.


### <a name="recommendation-about-web-apps-requesting-ssl-certificates-no-longer-part-of-secure-score"></a>SSL 인증서를 요청하는 웹앱에 대한 권장 사항은 더 이상 보안 점수에 포함되지 않음

"웹앱에서 들어오는 모든 요청에 대해 SSL 인증서를 요청해야 합니다" 권장 사항이 보안 컨트롤 **액세스 및 권한 관리**(최대 4포인트 상당)에서 **보안 모범 사례 구현**(포인트 가치 없음)으로 이동되었습니다. 

웹앱이 인증서를 요청하도록 하면 더욱 안전하게 보호할 수 있습니다. 그러나 공용 웹앱의 경우에는 관련이 없습니다. HTTP를 통해 사이트에 액세스하고 HTTPS를 통해서는 액세스하지 않는 경우 클라이언트 인증서가 제공되지 않습니다. 따라서 애플리케이션에 클라이언트 인증서가 필요한 경우 HTTP를 통한 애플리케이션 요청을 허용해서는 안 됩니다. [Azure App Service에 대한 TLS 상호 인증 구성](../app-service/app-service-web-configure-tls-mutual-auth.md)에서 자세히 알아보세요.

이러한 변경으로 권장 사항은 이제 점수에 영향을 주지 않는 권장 모범 사례가 됩니다. 

[보안 컨트롤 및 해당 권장](secure-score-security-controls.md#security-controls-and-their-recommendations)에서 각 보안 제어에 어떤 권장 사항이 있는지 알아보세요.


### <a name="recommendations-page-has-new-filters-for-environment-severity-and-available-responses"></a>권장 사항 페이지에는 환경, 심각도 및 사용 가능한 응답에 대한 새 필터가 있음

Azure Security Center는 연결된 모든 리소스를 모니터링하고 보안 권장 사항을 생성합니다. 이러한 권장 사항을 사용하여 하이브리드 클라우드 상태를 강화하고 조직, 산업 및 국가와 관련된 정책 및 표준 준수 여부를 추적합니다.

Security Center가 범위와 기능을 계속 확장함에 따라 보안 권장 사항 목록이 매월 증가하고 있습니다. 예를 들어, [Azure 보안 벤치마크의 적용 범위를 늘리기 위해 29개의 미리 보기 추천 사항이 추가됨](#29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark)을 참조하세요.

목록이 증가함에 따라 가장 관심 있는 권장 사항을 필터링할 수 있어야 합니다. 11월에는 권장 사항 페이지에 필터를 추가했습니다([이제 추천 목록에 필터가 포함됨](#recommendations-list-now-includes-filters) 참조).

이 달에 추가된 필터는 다음에 따라 추천 목록을 세분화하는 옵션을 제공합니다.

- **환경** - AWS, GCP 또는 Azure 리소스(또는 모든 조합)에 대한 권장 사항 보기
- **심각도** - Security Center에 의해 설정된 심각도 분류에 따른 권장 사항 보기
- **대응 조치** - 다음과 같은 Security Center 대응 옵션에 따른 권장 사항 보기 빠른 수정, 거부 및 적용

    > [!TIP]
    > 대응 조치 필터는 **빠른 수정 사용 가능(예/아니요)** 필터를 대체합니다. 
    > 
    > 각각의 대응 옵션에 대해 자세히 알아보세요.
    > - [빠른 수정](security-center-remediate-recommendations.md#quick-fix-remediation)
    > - [적용/거부 권장 사항을 사용하여 구성 오류 방지](prevent-misconfigurations.md)

:::image type="content" source="./media/release-notes/added-recommendations-filters.png" alt-text="보안 컨트롤별로 그룹화된 권장 사항" lightbox="./media/release-notes/added-recommendations-filters.png":::

### <a name="continuous-export-gets-new-data-types-and-improved-deployifnotexist-policies"></a>연속 내보내기는 새 데이터 형식 및 향상된 deployifnotexist 정책을 가져옴

Azure Security Center의 연속 내보내기 도구를 사용하여 환경의 다른 모니터링 도구와 함께 사용할 Security Center의 권장 사항 및 경고를 내보낼 수 있습니다.

연속 내보내기를 사용하면 내보낼 대상과 위치를 자유롭게 사용자 지정할 수 있습니다. 자세한 내용은 [Security Center 데이터 연속 내보내기](continuous-export.md)를 참조하세요.

이러한 도구는 다음과 같은 방법으로 향상되고 확장되었습니다.

- **연속 내보내기의 deployifnotexist 정책이 향상되었습니다**. 현재 정책은

    - **구성을 사용할 수 있는지 여부를 확인합니다.** 그렇지 않은 경우 정책은 비준수로 표시되고 준수 리소스를 생성합니다. [연속 내보내기 설정](continuous-export.md#set-up-a-continuous-export)의 "Azure Policy를 사용하여 대규모 배포 탭"에서 제공된 Azure Policy 템플릿에 대해 자세히 알아보세요.

    - **보안 결과 내보내기를 지원합니다.** Azure Policy 템플릿을 사용하는 경우 검색 결과를 포함하도록 연속 내보내기를 구성할 수 있습니다. 이는 취약성 평가 스캐너의 검색 결과 또는 '상위' 권장 사항 "시스템 업데이트가 컴퓨터에 설치되어 있어야 합니다."에 대한 특정 시스템 업데이트와 같은 '하위' 권장 사항이 있는 권장 사항을 내보낼 때 관련됩니다.
    
    - **보안 점수 데이터 내보내기를 지원합니다.**

- **규정 준수 평가 데이터(미리 보기 형식)가 추가되었습니다.** 이제 사용자 지정 이니셔티브를 포함하여 규정 준수 평가에 대한 업데이트를 Log Analytics 작업 영역 또는 Event Hub로 지속적으로 내보낼 수 있습니다. 국가/소버린 클라우드에서는 이 기능을 사용할 수 없습니다.

    :::image type="content" source="media/release-notes/continuous-export-regulatory-compliance-option.png" alt-text="연속 내보내기 데이터와 함께 규정 준수 평가 정보를 포함하기 위한 옵션.":::


## <a name="november-2020"></a>2020년 11월

11월의 업데이트는 다음과 같습니다.

- [Azure 보안 벤치마크의 적용 범위를 늘리기 위해 29개의 미리 보기 추천 사항이 추가됨](#29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark)
- [Security Center의 규정 준수 대시보드에 NIST SP 800 171 R2가 추가됨](#nist-sp-800-171-r2-added-to-security-centers-regulatory-compliance-dashboard)
- [이제 추천 목록에 필터가 포함됨](#recommendations-list-now-includes-filters)
- [자동 프로비저닝 환경 향상 및 확장](#auto-provisioning-experience-improved-and-expanded)
- [이제 연속 내보내기(미리 보기)에서 보안 점수를 사용할 수 있습니다.](#secure-score-is-now-available-in-continuous-export-preview)
- ["시스템 업데이트가 컴퓨터에 설치되어 있어야 합니다." 권장 사항이 이제 하위 권장 사항을 포함합니다.](#system-updates-should-be-installed-on-your-machines-recommendation-now-includes-sub-recommendations)
- [이제 기본 정책 할당의 상태를 보여주는 Azure Portal의 정책 관리 페이지](#policy-management-page-in-the-azure-portal-now-shows-status-of-default-policy-assignments)

### <a name="29-preview-recommendations-added-to-increase-coverage-of-azure-security-benchmark"></a>Azure 보안 벤치마크의 적용 범위를 늘리기 위해 29개의 미리 보기 권장 사항 추가됨

Azure 보안 벤치마크는 일반적인 규정 준수 프레임워크를 기반으로 하는 보안 및 규정 준수 모범 사례에 대해 Microsoft에서 작성한 Azure 관련 지침 세트입니다. [Azure 보안 벤치마크에 대해 자세히 알아보세요](../security/benchmarks/introduction.md).

이 벤치마크의 적용 범위를 넓히기 위해 다음 29개의 새로운 추천 사항이 Security Center에 추가되었습니다.

미리 보기 추천 사항은 리소스를 비정상으로 렌더링하지 않으며 보안 점수 계산에 포함되지 않습니다. 미리 보기 기간이 끝나면 점수에 기여할 수 있도록 가능한 경우 언제든지 수정합니다. [Azure Security Center의 추천 사항 수정](security-center-remediate-recommendations.md)에서 이러한 추천 사항에 대응하는 방법에 대해 자세히 알아보세요.

| 보안 컨트롤                     | 새로운 권장 사항                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 전송 중인 데이터 암호화              | - PostgreSQL 데이터베이스 서버에 대해 SSL 연결 적용을 사용하도록 설정해야 합니다.<br>- MySQL 데이터베이스 서버에 대해 SSL 연결 적용을 사용하도록 설정해야 합니다.<br>- TLS를 최신 API 앱 버전으로 업데이트해야 합니다.<br>- TLS를 최신 함수 앱 버전으로 업데이트해야 합니다.<br>- TLS를 최신 웹앱 버전으로 업데이트해야 합니다.<br>- API 앱에서 FTPS를 요구해야 합니다.<br>- 함수 앱에서 FTPS를 요구해야 합니다.<br>- 웹앱에서 FTPS를 요구해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 액세스 및 사용 권한 관리        | - 웹앱에서 들어오는 모든 요청에 대해 SSL 인증서를 요청해야 합니다.<br>- API 앱에서 관리 ID를 사용해야 합니다.<br>- 함수 앱에서 관리 ID를 사용해야 합니다.<br>- 웹앱에서 관리 ID를 사용해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 무단 네트워크 액세스 제한 | - 프라이빗 엔드포인트를 PostgreSQL 서버에서 사용할 수 있어야 합니다.<br>- 프라이빗 엔드포인트를 MariaDB 서버에서 사용할 수 있어야 합니다.<br>- 프라이빗 엔드포인트를 MySQL 서버에서 사용할 수 있어야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 감사 및 로깅 사용          | - App Services에서 진단 로그를 사용하도록 설정해야 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 보안 모범 사례 구현    | - Azure Backup을 가상 머신에 사용하도록 설정해야 합니다.<br>- Azure Database for MariaDB에 대해 지역 중복 백업을 사용하도록 설정해야 합니다.<br>- Azure Database for MySQL에 대해 지역 중복 백업을 사용하도록 설정해야 합니다.<br>- Azure Database for PostgreSQL에 대해 지역 중복 백업을 사용하도록 설정해야 합니다.<br>- PHP를 최신 API 앱 버전으로 업데이트해야 합니다.<br>- PHP를 최신 웹앱 버전으로 업데이트해야 합니다.<br>- Java를 최신 API 앱 버전으로 업데이트해야 합니다.<br>- Java를 최신 함수 앱 버전으로 업데이트해야 합니다.<br>- Java를 최신 웹앱 버전으로 업데이트해야 합니다.<br>- Python을 최신 API 앱 버전으로 업데이트해야 합니다.<br>- Python을 최신 함수 앱 버전으로 업데이트해야 합니다.<br>- Python을 최신 웹앱 버전으로 업데이트해야 합니다.<br>- SQL 서버에 대한 감사 보존 기간은 90일 이상으로 설정해야 합니다. |
|                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

관련 링크:

- [Azure 보안 벤치마크에 대한 자세한 정보](../security/benchmarks/introduction.md)
- [Azure API 앱에 대한 자세한 정보](../app-service/app-service-web-tutorial-rest-api.md)
- [Azure 함수 앱에 대한 자세한 정보](../azure-functions/functions-overview.md)
- [Azure 웹앱에 대한 자세한 정보](../app-service/overview.md)
- [Azure Database for MariaDB에 대한 자세한 정보](../mariadb/overview.md)
- [Azure Database for MySQL에 대한 자세한 정보](../mysql/overview.md)
- [Azure Database for PostgreSQL에 대한 자세한 정보](../postgresql/overview.md)


### <a name="nist-sp-800-171-r2-added-to-security-centers-regulatory-compliance-dashboard"></a>Security Center의 규정 준수 대시보드에 NIST SP 800 171 R2가 추가됨

NIST SP 800-171 R2 표준은 이제 Azure Security Center의 규정 준수 대시보드에서 사용할 수 있는 기본 이니셔티브로 제공됩니다. 제어에 대한 매핑은 [NIST SP 800-171 R2 규정 준수 기본 제공 이니셔티브의 세부 정보](../governance/policy/samples/nist-sp-800-171-r2.md)에 설명되어 있습니다. 

표준을 구독에 적용하고 규정 준수 상태를 지속적으로 모니터링하려면 [규정 준수 대시보드의 표준 집합 사용자 지정](update-regulatory-compliance-packages.md)의 지침을 사용합니다.

:::image type="content" source="media/release-notes/nist-sp-800-171-r2-standard.png" alt-text="Security Center 규정 준수 대시보드의 NIST SP 800 171 R2 표준":::

이 규정 준수 표준에 대한 자세한 내용은 [NIST SP 800-171 R2](https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final)를 참조하세요.


### <a name="recommendations-list-now-includes-filters"></a>이제 추천 목록에 필터가 포함됨

이제 일련의 조건에 따라 보안 추천 목록을 필터링할 수 있습니다. 다음 예에서는 다음과 같은 추천을 보여주기 위해 추천 목록이 필터링되었습니다.

- **일반 공급**(즉, 미리 보기 아님)
- **스토리지 계정** 에 대한 추천
- **빠른 수정** 수정을 지원하는 추천

:::image type="content" source="media/release-notes/recommendations-filters.png" alt-text="추천 목록에 대한 필터":::


### <a name="auto-provisioning-experience-improved-and-expanded"></a>자동 프로비저닝 환경 향상 및 확장

자동 프로비저닝 기능은 신규 및 기존 Azure VM에 필요한 확장을 설치하여 관리 오버헤드를 줄이는 데 도움이 되므로 Security Center의 보호 기능을 활용할 수 있습니다. 

Azure Security Center가 성장함에 따라 더 많은 확장이 개발되었으며 보안 센터에서 더 많은 리소스 유형을 모니터링할 수 있습니다. 이제 Azure Policy의 기능을 활용하여 추가 확장 및 리소스 유형을 지원하도록 자동 프로비저닝 도구가 확장되었습니다.

이제 다음 항목의 자동 프로비저닝을 구성할 수 있습니다.

- Log Analytics 에이전트
- (신규) Kubernetes에 대한 Azure Policy 추가 기능
- (신규) Microsoft Dependency Agent

[Azure Security Center에서 에이전트 및 확장 자동 프로비저닝](security-center-enable-data-collection.md)에서 자세히 알아보세요.


### <a name="secure-score-is-now-available-in-continuous-export-preview"></a>이제 연속 내보내기(미리 보기)에서 보안 점수를 사용할 수 있습니다.

보안 점수를 연속적으로 내보내면 점수 변경 내용을 Azure Event Hubs 또는 Log Analytics 작업 영역에 실시간으로 스트리밍할 수 있습니다. 이 기능을 사용하여 다음을 수행할 수 있습니다.

- 동적 보고서로 시간 경과에 따른 보안 점수 추적
- 보안 점수 데이터를 Azure Sentinel(또는 기타 SIEM)로 내보내기
- 이 데이터를 조직에서 보안 점수를 모니터링하는 데 이미 사용하고 있을 수 있는 프로세스와 통합

[Security Center 데이터를 연속적으로 내보내는](continuous-export.md) 방법에 대해 자세히 알아보세요.


### <a name="system-updates-should-be-installed-on-your-machines-recommendation-now-includes-sub-recommendations"></a>"시스템 업데이트가 컴퓨터에 설치되어 있어야 합니다." 권장 사항이 이제 하위 권장 사항을 포함합니다.

**시스템 업데이트가 컴퓨터에 설치되어 있어야 합니다.** 권장 사항이 향상되었습니다. 새 버전에는 누락된 각 업데이트에 대한 하위 권장 사항이 포함되어 있으며 다음과 같은 기능이 향상되었습니다.

- Azure Portal의 Azure Security Center 페이지에서 새롭게 디자인된 환경. **시스템 업데이트는 머신에 설치되어야 합니다** 에 대한 권장 사항 세부 정보 페이지에는 아래와 같은 결과 목록이 포함되어 있습니다. 단일 찾기를 선택하면 재구성 정보 및 영향을 받는 리소스의 목록에 대한 링크가 포함된 세부 정보 창이 열립니다.

    :::image type="content" source="./media/upcoming-changes/system-updates-should-be-installed-subassessment.png" alt-text="업데이트된 권장 사항에 대한 포털 환경에서 하위 권장 사항 중 하나 열기":::

- ARG(Azure Resource Graph)의 권장 사항에 대한 보강 데이터. ARG는 효율적인 리소스 탐색을 제공하도록 디자인된 Azure 서비스입니다. ARG를 사용하여 사용자 환경을 효과적으로 관리할 수 있도록 지정된 구독 세트에서 대규모로 쿼리할 수 있습니다. 

    Azure Security Center의 경우 ARG 및 [KQL(Kusto Query Language)](/azure/data-explorer/kusto/query/)을 사용하여 다양한 보안 태세 데이터를 쿼리할 수 있습니다.

    이전에는 ARG에서 이 권장 사항을 쿼리한 경우 권장 사항을 머신에서 수정해야 한다는 정보만 제공되었습니다. 향상된 버전의 다음 쿼리는 누락된 각 시스템 업데이트를 머신별로 그룹화하여 반환합니다.

    ```kusto
    securityresources
    | where type =~ "microsoft.security/assessments/subassessments"
    | where extract(@"(?i)providers/Microsoft.Security/assessments/([^/]*)", 1, id) == "4ab6e3c5-74dd-8b35-9ab9-f61b30875b27"
    | where properties.status.code == "Unhealthy"
    ```

### <a name="policy-management-page-in-the-azure-portal-now-shows-status-of-default-policy-assignments"></a>이제 기본 정책 할당의 상태를 보여주는 Azure Portal의 정책 관리 페이지

이제 Azure Portal의 Security Center **보안 정책** 페이지에서 구독에 기본 Security Center 정책이 할당되었는지 여부를 확인할 수 있습니다.

:::image type="content" source="media/release-notes/policy-assignment-info-per-subscription.png" alt-text="기본 정책 할당을 보여주는 Azure Security Center의 정책 관리 페이지":::

## <a name="october-2020"></a>2020년 10월

10월의 업데이트는 다음과 같습니다.
- [온-프레미스 및 다중 클라우드 머신의 취약성 평가(미리 보기)](#vulnerability-assessment-for-on-premise-and-multi-cloud-machines-preview)
- [Azure Firewall 권장 사항 추가(미리 보기)](#azure-firewall-recommendation-added-preview)
- [[Kubernetes 서비스에서 권한 있는 IP 범위를 정의해야 함] 권장 사항의 빠른 픽스가 업데이트됨](#authorized-ip-ranges-should-be-defined-on-kubernetes-services-recommendation-updated-with-quick-fix)
- [이제 규정 준수 대시보드에는 표준을 제거하는 옵션이 포함됨](#regulatory-compliance-dashboard-now-includes-option-to-remove-standards)
- [ARG(Azure Resource Graph)에서 Microsoft.Security/securityStatuses 테이블이 제거됨](#microsoftsecuritysecuritystatuses-table-removed-from-azure-resource-graph-arg)

### <a name="vulnerability-assessment-for-on-premise-and-multi-cloud-machines-preview"></a>온-프레미스 및 다중 클라우드 머신의 취약성 평가(미리 보기)

[서버용 Azure Defender](defender-for-servers-introduction.md)의 통합 취약성 평가 스캐너(Qualys 기반)는 이제 Azure Arc 사용 서버를 검색합니다.

Azure가 아닌 머신에서 Azure Arc를 사용하도록 설정한 경우 Security Center는 이러한 머신에 통합 취약성 스캐너를 수동 및 대규모로 배포할 수 있습니다.

이번 업데이트를 통해 모든 Azure 및 비-Azure 자산의 취약성 관리 프로그램을 통합하는 **서버용 Azure Defender** 의 강력한 성능을 발휘할 수 있습니다.

주요 기능:

- Azure Arc 머신의 VA(취약성 평가) 스캐너 프로비저닝 상태 모니터링
- 보호되지 않는 Windows 및 Linux Azure Arc 머신에 통합 VA 에이전트 프로비저닝(수동 및 대규모로)
- 배포된 에이전트에서 탐지된 취약성 수신 및 분석(수동 및 대규모로)
- Azure VM 및 Azure Arc 머신에 대한 통합 환경

[하이브리드 머신에 통합 취약성 스캐너를 배포하는 내용을 자세히 알아보세요](deploy-vulnerability-assessment-vm.md#deploy-the-integrated-scanner-to-your-azure-and-hybrid-machines).

[Azure Arc 사용 서버에 대해 자세히 알아보세요](../azure-arc/servers/index.yml).


### <a name="azure-firewall-recommendation-added-preview"></a>Azure Firewall 권장 사항 추가(미리 보기)

Azure Firewall을 통해 모든 가상 네트워크를 보호하기 위해 새로운 권장 사항이 추가되었습니다.

**가상 네트워크는 Azure Firewall로 보호해야 합니다** 권장 사항은 Azure Firewall을 사용하여 가상 네트워크에 대한 액세스를 제한하고 잠재적 위협을 차단할 것을 조언합니다.

[Azure Firewall](https://azure.microsoft.com/services/azure-firewall/)에 대해 자세히 알아보세요.


### <a name="authorized-ip-ranges-should-be-defined-on-kubernetes-services-recommendation-updated-with-quick-fix"></a>[Kubernetes 서비스에서 권한 있는 IP 범위를 정의해야 함] 권장 사항의 빠른 픽스가 업데이트됨

**Kubernetes 서비스에서 권한 있는 IP 범위를 정의해야 함** 권장 사항은 이제 빠른 픽스 옵션을 제공합니다.

이 권장 사항 및 기타 모든 Security Center 권장 사항에 대한 자세한 내용은 [보안 권장 사항 - 참조 가이드](recommendations-reference.md)를 참조하세요.

:::image type="content" source="./media/release-notes/authorized-ip-ranges-recommendation.png" alt-text="빠른 픽스 옵션을 제공하는 [Kubernetes 서비스에서 권한 있는 IP 범위를 정의해야 함] 권장 사항":::


### <a name="regulatory-compliance-dashboard-now-includes-option-to-remove-standards"></a>이제 규정 준수 대시보드에는 표준을 제거하는 옵션이 포함됨

Security Center의 규정 준수 대시보드는 특정 규정 준수 제어 및 요구 사항을 충족하는 방법에 따라 규정 준수 상태에 대한 인사이트를 제공합니다.

대시보드에는 규정 표준의 기본 세트가 포함되어 있습니다. 제공된 표준이 조직과 관련이 없는 경우 이제 구독에 대한 UI에서 해당 표준을 간단히 제거할 수 있는 간단한 프로세스입니다. 표준은 관리 그룹 범위가 아닌 *구독* 수준에서만 제거할 수 있습니다.

[대시보드에서 표준 제거](update-regulatory-compliance-packages.md#removing-a-standard-from-your-dashboard)에서 자세히 알아봅니다.


### <a name="microsoftsecuritysecuritystatuses-table-removed-from-azure-resource-graph-arg"></a>ARG(Azure Resource Graph)에서 Microsoft.Security/securityStatuses 테이블이 제거됨

Azure Resource Graph는 작업 환경을 효과적으로 관리할 수 있도록 특정 구독 세트에서 대규모로 쿼리를 수행할 수 있는 효율적인 리소스 탐색 기능을 제공하도록 디자인된 Azure 서비스입니다. 

Azure Security Center의 경우 ARG 및 [KQL(Kusto Query Language)](/azure/data-explorer/kusto/query/)을 사용하여 다양한 보안 태세 데이터를 쿼리할 수 있습니다. 예를 들어:

- 자산 인벤토리 활용(ARG)
- [MFA(다단계 인증)를 사용하지 않고 계정을 식별](security-center-identity-access.md#identify-accounts-without-multi-factor-authentication-mfa-enabled)하는 방법에 대한 샘플 ARG 쿼리가 문서로 준비되어 있습니다.

ARG 내에는 쿼리에 사용할 수 있는 데이터 테이블이 들어 있습니다.

:::image type="content" source="./media/release-notes/azure-resource-graph-tables.png" alt-text="Azure Resource Graph Explorer 및 사용 가능한 테이블":::

> [!TIP]
> ARG 설명서에는 [Azure Resource Graph 테이블 및 리소스 종류 참조](../governance/resource-graph/reference/supported-tables-resources.md)에서 사용 가능한 모든 테이블이 나열되어 있습니다.

이번 업데이트에서 **Microsoft.Security/securityStatuses** 테이블이 제거되었습니다. securityStatuses API는 계속 사용할 수 있습니다.

데이터 교체는 Microsoft.Security/Assessments에서 사용할 수 있습니다.

Microsoft.Security/securityStatuses는 평가의 집계를 보여주고 Microsoft.Security/Assessments는 각 평가에 대한 단일 레코드를 포함한다는 것이 가장 큰 차이점입니다.

예를 들어 Microsoft.Security/securityStatuses는 다음과 같은 두 개의 policyAssessments 배열이 포함된 결과를 반환합니다.

```
{
id: "/subscriptions/449bcidd-3470-4804-ab56-2752595 felab/resourceGroups/mico-rg/providers/Microsoft.Network/virtualNetworks/mico-rg-vnet/providers/Microsoft.Security/securityStatuses/mico-rg-vnet",
name: "mico-rg-vnet",
type: "Microsoft.Security/securityStatuses",
properties:  {
    policyAssessments: [
        {assessmentKey: "e3deicce-f4dd-3b34-e496-8b5381bazd7e", category: "Networking", policyName: "Azure DDOS Protection Standard should be enabled",...},
        {assessmentKey: "sefac66a-1ec5-b063-a824-eb28671dc527", category: "Compute", policyName: "",...}
    ],
    securitystateByCategory: [{category: "Networking", securityState: "None" }, {category: "Compute",...],
    name: "GenericResourceHealthProperties",
    type: "VirtualNetwork",
    securitystate: "High"
}
```
반면 Microsoft.Security/Assessments는 다음과 같이 각 정책 평가에 대한 레코드를 보유합니다.

```
{
type: "Microsoft.Security/assessments",
id:  "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourceGroups/mico-rg/providers/Microsoft. Network/virtualNetworks/mico-rg-vnet/providers/Microsoft.Security/assessments/e3delcce-f4dd-3b34-e496-8b5381ba2d70",
name: "e3deicce-f4dd-3b34-e496-8b5381ba2d70",
properties:  {
    resourceDetails: {Source: "Azure", Id: "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourceGroups/mico-rg/providers/Microsoft.Network/virtualNetworks/mico-rg-vnet"...},
    displayName: "Azure DDOS Protection Standard should be enabled",
    status: (code: "NotApplicable", cause: "VnetHasNOAppGateways", description: "There are no Application Gateway resources attached to this Virtual Network"...}
}

{
type: "Microsoft.Security/assessments",
id:  "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourcegroups/mico-rg/providers/microsoft.network/virtualnetworks/mico-rg-vnet/providers/Microsoft.Security/assessments/80fac66a-1ec5-be63-a824-eb28671dc527",
name: "8efac66a-1ec5-be63-a824-eb28671dc527",
properties: {
    resourceDetails: (Source: "Azure", Id: "/subscriptions/449bc1dd-3470-4804-ab56-2752595f01ab/resourcegroups/mico-rg/providers/microsoft.network/virtualnetworks/mico-rg-vnet"...),
    displayName: "Audit diagnostic setting",
    status:  {code: "Unhealthy"}
}
```

**이제 assessments 테이블을 사용하도록 securityStatuses를 사용하여 기존 ARG 쿼리를 변환하는 예제:**

SecurityStatuses를 참조하는 쿼리:

```kusto
SecurityResources 
| where type == 'microsoft.security/securitystatuses' and properties.type == 'virtualMachine'
| where name in ({vmnames}) 
| project name, resourceGroup, policyAssesments = properties.policyAssessments, resourceRegion = location, id, resourceDetails = properties.resourceDetails
```

Assessments 테이블의 대체 쿼리:

```kusto
securityresources
| where type == "microsoft.security/assessments" and id contains "virtualMachine"
| extend resourceName = extract(@"(?i)/([^/]*)/providers/Microsoft.Security/assessments", 1, id)
| extend source = tostring(properties.resourceDetails.Source)
| extend resourceId = trim(" ", tolower(tostring(case(source =~ "azure", properties.resourceDetails.Id,
source =~ "aws", properties.additionalData.AzureResourceId,
source =~ "gcp", properties.additionalData.AzureResourceId,
extract("^(.+)/providers/Microsoft.Security/assessments/.+$",1,id)))))
| extend resourceGroup = tolower(tostring(split(resourceId, "/")[4]))
| where resourceName in ({vmnames}) 
| project resourceName, resourceGroup, resourceRegion = location, id, resourceDetails = properties.additionalData
```

다음 링크에서 자세한 내용을 알아보세요.
- [Azure Resource Graph Explorer를 사용하여 쿼리를 만드는 방법](../governance/resource-graph/first-query-portal.md)
- [Kusto Query Language(KQL)](/azure/data-explorer/kusto/query/)


## <a name="september-2020"></a>2020년 9월

9월의 업데이트는 다음과 같습니다.
- [Security Center가 새로운 모습으로 바뀌었습니다!](#security-center-gets-a-new-look)
- [Azure Defender가 릴리스됨](#azure-defender-released)
- [Key Vault용 Azure Defender가 일반 공급됨](#azure-defender-for-key-vault-is-generally-available)
- [Files 및 ADLS Gen2에 대한 Storage용 Azure Defender 보호가 일반 공급됨](#azure-defender-for-storage-protection-for-files-and-adls-gen2-is-generally-available)
- [이제 자산 인벤토리 도구가 일반 공급됨](#asset-inventory-tools-are-now-generally-available)
- [컨테이너 레지스트리 및 가상 머신 검사에 대한 특정 취약성 결과 사용 안 함](#disable-a-specific-vulnerability-finding-for-scans-of-container-registries-and-virtual-machines)
- [권장 사항에서 리소스 제외](#exempt-a-resource-from-a-recommendation)
- [Security Center의 AWS 및 GCP 커넥터에서 다중 클라우드 환경을 제공함](#aws-and-gcp-connectors-in-security-center-bring-a-multi-cloud-experience)
- [Kubernetes 워크로드 보호 추천 사항 번들](#kubernetes-workload-protection-recommendation-bundle)
- [이제 취약성 평가 결과를 연속 내보내기에서 사용할 수 있음](#vulnerability-assessment-findings-are-now-available-in-continuous-export)
- [새 리소스를 만들 때 추천 사항을 적용하여 보안 구성 오류 방지](#prevent-security-misconfigurations-by-enforcing-recommendations-when-creating-new-resources)
- [네트워크 보안 그룹 추천 사항이 향상됨](#network-security-group-recommendations-improved)
- ["Kubernetes 서비스에 Pod 보안 정책을 정의해야 합니다."라는 미리 보기 AKS 추천 사항이 더 이상 사용되지 않음](#deprecated-preview-aks-recommendation-pod-security-policies-should-be-defined-on-kubernetes-services)
- [Azure Security Center의 이메일 알림이 향상됨](#email-notifications-from-azure-security-center-improved)
- [보안 점수에 미리 보기 추천 사항이 포함되지 않음](#secure-score-doesnt-include-preview-recommendations)
- [이제 추천 사항에 심각도 표시기 및 새로 고침 간격이 포함됨](#recommendations-now-include-a-severity-indicator-and-the-freshness-interval)


### <a name="security-center-gets-a-new-look"></a>Security Center가 새로운 모습으로 바뀌었습니다!

Security Center의 포털 페이지에 대해 새로 고친 UI를 릴리스했습니다. 새 페이지에는 보안 점수, 자산 인벤토리 및 Azure Defender 대시보드뿐만 아니라 새 개요 페이지도 포함되었습니다.

다시 설계된 개요 페이지에는 이제 보안 점수, 자산 인벤토리 및 Azure Defender 대시보드에 액세스하기 위한 타일이 있습니다. 또한 규정 준수 대시보드에 연결되는 타일도 있습니다.

[개요 페이지](overview-page.md)에 대해 자세히 알아보세요.


### <a name="azure-defender-released"></a>Azure Defender가 릴리스됨

**Azure Defender** 는 Security Center 내부에 통합되어 Azure 및 하이브리드 워크로드에 대한 고급 인텔리전트 보호를 제공하는 CWPP(클라우드 워크로드 보호 플랫폼)입니다. Security Center의 표준 가격 책정 계층 옵션을 대체합니다. 

Azure Security Center의 **가격 책정 및 설정** 영역에서 Azure Defender를 사용하도록 설정하면 다음 Defender 플랜이 동시에 사용하도록 설정되어 환경의 컴퓨팅, 데이터 및 서비스 계층에 대한 포괄적인 방어 기능을 제공합니다.

- [서버용 Azure Defender](defender-for-servers-introduction.md)
- [App Service용 Azure Defender](defender-for-app-service-introduction.md)
- [스토리지용 Azure Defender](defender-for-storage-introduction.md)
- [Azure Defender for SQL](defender-for-sql-introduction.md)
- [Key Vault용 Azure Defender](defender-for-key-vault-introduction.md)
- [Kubernetes용 Azure Defender](defender-for-kubernetes-introduction.md)
- [컨테이너 레지스트리용 Azure Defender](defender-for-container-registries-introduction.md)

이러한 플랜 각각은 Security Center 설명서에서 별도로 설명하고 있습니다.

Azure Defender는 전용 대시보드를 사용하여 가상 머신, SQL 데이터베이스, 컨테이너, 웹 애플리케이션, 네트워크 등에 대한 보안 경고 및 지능형 위협 방지 기능을 제공합니다.

[Azure Defender](azure-defender.md)에 대해 자세히 알아보세요.

### <a name="azure-defender-for-key-vault-is-generally-available"></a>Key Vault용 Azure Defender가 일반 공급됨

Azure Key Vault는 암호화 키와 비밀(예: 인증서, 연결 문자열 및 암호)을 보호하는 클라우드 서비스입니다. 

**Key Vault용 Azure Defender** 는 Azure Key Vault용 Azure 네이티브 Advanced Threat Protection 기능을 통해 추가 보안 인텔리전스 계층을 제공합니다. Key Vault용 Azure Defender는 확장을 통해 결과적으로 Key Vault 계정에 종속된 많은 리소스를 보호합니다.

선택적 플랜은 이제 GA입니다. 이 기능은 미리 보기에서 "Azure Key Vault용 Advanced Threat Protection"으로 제공되었습니다.

또한 Azure Portal의 Key Vault 페이지에는 이제 **Security Center** 추천 사항 및 경고에 대한 전용 **보안** 페이지가 포함됩니다.

[Key Vault용 Azure Defender](defender-for-key-vault-introduction.md)에서 자세히 알아보세요.


### <a name="azure-defender-for-storage-protection-for-files-and-adls-gen2-is-generally-available"></a>Files 및 ADLS Gen2에 대한 Storage용 Azure Defender 보호가 일반 공급됨 

**Storage용 Azure Defender** 는 Azure Storage 계정에서 잠재적으로 유해한 활동을 탐지합니다. Blob 컨테이너, 파일 공유 또는 데이터 레이크로 저장되는지에 관계없이 데이터를 보호할 수 있습니다.

이제 [Azure Files](../storage/files/storage-files-introduction.md) 및 [Azure Data Lake Storage Gen2](../storage/blobs/data-lake-storage-introduction.md)에 대한 지원이 일반 공급됩니다.

2020년 10월 1일부터 이러한 서비스에서 리소스를 보호하는 데 드는 요금이 청구됩니다.

[Storage용 Azure Defender](defender-for-storage-introduction.md)에서 자세히 알아보세요.


### <a name="asset-inventory-tools-are-now-generally-available"></a>이제 자산 인벤토리 도구가 일반 공급됨

Azure Security Center의 자산 인벤토리 페이지는 Security Center에 연결한 리소스의 보안 상태를 확인할 수 있는 단일 페이지를 제공합니다.

Security Center는 Azure 리소스의 보안 상태를 정기적으로 분석하여 잠재적인 보안 취약성을 식별합니다. 그런 다음, 이러한 취약성을 수정하는 방법에 대한 추천 사항을 제공합니다.

리소스에 수정되지 않은 추천 사항이 있으면 인벤토리에 표시됩니다.

[자산 인벤토리로 리소스 탐색 및 관리](asset-inventory.md)에서 자세히 알아보세요.



### <a name="disable-a-specific-vulnerability-finding-for-scans-of-container-registries-and-virtual-machines"></a>컨테이너 레지스트리 및 가상 머신 검사에 대한 특정 취약성 결과 사용 안 함

Azure Defender에는 Azure Container Registry 및 가상 머신의 이미지를 검사하는 취약성 스캐너가 포함되어 있습니다.

조직에서 결과를 수정하지 않고 무시해야 하는 요구 사항이 있으면 필요에 따라 이 결과를 사용하지 않도록 설정할 수 있습니다. 사용하지 않도록 설정된 결과는 보안 점수에 영향을 주거나 원치 않는 노이즈를 생성하지 않습니다.

결과가 사용 안 함 규칙에 정의한 조건과 일치하면 검색 결과 목록에 표시되지 않습니다.

이 옵션은 다음에 대한 추천 사항 세부 정보 페이지에서 사용할 수 있습니다.

- **Azure Container Registry 이미지의 취약성을 수정해야 함**
- **가상 머신의 취약성을 수정해야 함**

[컨테이너 이미지에 대한 특정 결과 사용 안 함](defender-for-container-registries-usage.md#disable-specific-findings-preview) 및 [가상 머신에 대한 특정 결과 사용 안 함](remediate-vulnerability-findings-vm.md#disable-specific-findings-preview)에서 자세히 알아보세요.


### <a name="exempt-a-resource-from-a-recommendation"></a>권장 사항에서 리소스 제외

경우에 따라 리소스가 특정 추천 사항과 관련하여 비정상 상태가 아니라고 생각하더라도 비정상 상태로 표시됩니다. 이로 인해 보안 점수가 낮아집니다. Security Center에서 추적하지 않는 프로세스를 통해 수정되었을 수 있습니다. 또는 조직에서 특정 리소스에 대한 위험을 감수하기로 결정했을 수도 있습니다. 

이러한 경우 예외 규칙을 만들고 나중에 해당 리소스가 비정상 리소스에 나열되지 않도록 할 수 있습니다. 이러한 규칙에는 아래에서 설명한 대로 문서화된 근거가 포함될 수 있습니다.

[추천 사항 및 보안 점수에서 리소스 제외](exempt-resource.md)에서 자세히 알아보세요.


### <a name="aws-and-gcp-connectors-in-security-center-bring-a-multi-cloud-experience"></a>Security Center의 AWS 및 GCP 커넥터에서 다중 클라우드 환경을 제공함

클라우드 워크로드가 일반적으로 여러 클라우드 플랫폼에 걸쳐 있는 경우 클라우드 보안 서비스도 동일한 작업을 수행해야 합니다.

Azure Security Center는 이제 Azure, AWS(Amazon Web Services) 및 GCP(Google Cloud Platform)에서 워크로드를 보호합니다.

AWS 및 GCP 계정을 Security Center에 온보딩하면 AWS Security Hub, GCP Security Command 및 Azure Security Center를 통합합니다. 

[Azure Security Center에 AWS 계정 연결](quickstart-onboard-aws.md) 및 [Azure Security Center에 GCP 계정 연결](quickstart-onboard-gcp.md)에서 자세히 알아보세요.


### <a name="kubernetes-workload-protection-recommendation-bundle"></a>Kubernetes 워크로드 보호 추천 사항 번들

Kubernetes 워크로드에서 기본적으로 보안을 유지할 수 있도록 하기 위해 Security Center에서 Kubernetes 허용 제어를 사용하는 적용 옵션을 포함하여 Kubernetes 수준 보안 강화 추천 사항을 추가합니다.

Kubernetes용 Azure Policy 추가 기능을 AKS 클러스터에 설치한 경우 Kubernetes API 서버에 대한 모든 요청은 클러스터에 유지되기 전에 미리 정의된 모범 사례 세트에 대해 모니터링됩니다. 그런 다음, 모범 사례를 적용하고 향후 워크로드에 대해 위임하도록 구성할 수 있습니다.

예를 들어 권한 있는 컨테이너를 만들지 않도록 위임할 수 있습니다. 그러면, 이러한 작업에 대한 이후의 모든 요청이 차단됩니다.

[Kubernetes 허용 제어를 사용하여 워크로드 보호 모범 사례](container-security.md#workload-protection-best-practices-using-kubernetes-admission-control)에서 자세히 알아보세요.


### <a name="vulnerability-assessment-findings-are-now-available-in-continuous-export"></a>이제 취약성 평가 결과를 연속 내보내기에서 사용할 수 있음

연속 내보내기를 사용하여 경고 및 추천 사항을 Azure Event Hubs, Log Analytics 작업 영역 또는 Azure Monitor에 실시간으로 스트리밍합니다. 여기서는 이 데이터를 SIEM(예: Azure Sentinel, Power BI, Azure Data Explorer 등)과 통합할 수 있습니다.

Security Center의 통합 취약성 평가 도구는 "가상 머신의 취약성을 수정해야 함"과 같은 '부모' 추천 사항 내에서 리소스에 대한 결과를 실행 가능한 추천 사항으로 반환합니다. 

이제 추천 사항을 선택하고 **보안 결과 포함** 옵션을 사용하도록 설정하면 연속 내보내기를 통해 보안 결과를 내보낼 수 있습니다.

:::image type="content" source="./media/continuous-export/include-security-findings-toggle.png" alt-text="연속 내보내기 구성의 보안 결과 포함 설정/해제" :::

관련 페이지:

- [Azure 가상 머신에 대한 Security Center의 통합 취약성 평가 솔루션](deploy-vulnerability-assessment-vm.md)
- [Azure Container Registry 이미지에 대한 Security Center의 통합 취약성 평가 솔루션](defender-for-container-registries-usage.md)
- [연속 내보내기](continuous-export.md)

### <a name="prevent-security-misconfigurations-by-enforcing-recommendations-when-creating-new-resources"></a>새 리소스를 만들 때 추천 사항을 적용하여 보안 구성 오류 방지

보안 구성 오류는 보안 인시던트의 주요 원인입니다. 이제 Security Center에는 특정 추천 사항과 관련하여 새 리소스의 구성 오류를 *방지* 하는 데 도움이 되는 기능이 있습니다. 

이 기능을 통해 워크로드를 안전하게 유지하고 보안 점수를 안정화할 수 있습니다.

특정 추천 사항에 따라 보안 구성을 적용하는 방법은 다음 두 가지 모드로 제공됩니다.

- Azure Policy의 **거부** 효과를 사용하여 비정상 리소스가 만들어지는 것을 중지할 수 있습니다.

- **적용** 옵션을 사용하여 Azure Policy의 **DeployIfNotExist** 효과를 활용하고, 비준수 리소스를 만들 때 자동으로 수정할 수 있습니다.
 
이는 선택한 보안 추천 사항에 사용할 수 있으며 리소스 세부 정보 페이지의 위쪽에서 찾을 수 있습니다.

[적용/거부 추천 사항을 사용하여 구성 오류 방지](prevent-misconfigurations.md)에서 자세히 알아보세요.

###  <a name="network-security-group-recommendations-improved"></a>네트워크 보안 그룹 추천 사항이 향상됨

일부 가양성 인스턴스를 줄이기 위해 네트워크 보안 그룹과 관련된 다음과 같은 보안 추천 사항이 향상되었습니다.

- VM에 연결된 NSG에서 모든 네트워크 포트를 제한해야 함
- 가상 머신에서 관리 포트를 닫아야 합니다.
- 인터넷 연결 가상 머신은 네트워크 보안 그룹과 함께 보호되어야 합니다.
- 서브넷을 네트워크 보안 그룹과 연결해야 합니다.


### <a name="deprecated-preview-aks-recommendation-pod-security-policies-should-be-defined-on-kubernetes-services"></a>"Kubernetes 서비스에 Pod 보안 정책을 정의해야 합니다."라는 미리 보기 AKS 추천 사항이 더 이상 사용되지 않음

[Azure Kubernetes Service](../aks/use-pod-security-policies.md) 설명서에서 설명한 대로 "Kubernetes Services에서 Pod 보안 정책을 정의해야 합니다."라는 미리 보기 추천 사항이 더 이상 사용되지 않습니다.

Pod 보안 정책(미리 보기) 기능은 더 이상 사용하지 않도록 설정되며, AKS에 대한 Azure Policy에 따라 2020년 10월 15일 이후에는 더 이상 사용할 수 없습니다.

Pod 보안 정책(미리 보기)이 더 이상 사용되지 않는 경우 향후 클러스터 업그레이드를 수행하고 Azure 지원을 유지하려면 더 이상 사용되지 않는 기능을 사용하여 기존 클러스터에서 이 기능을 사용하지 않도록 설정해야 합니다.


### <a name="email-notifications-from-azure-security-center-improved"></a>Azure Security Center의 이메일 알림이 향상됨

보안 경고와 관련하여 향상된 이메일 영역은 다음과 같습니다. 

- 모든 심각도 수준에 대한 경고와 관련된 이메일 알림을 보내는 기능이 추가되었습니다.
- 구독에서 다른 Azure 역할의 사용자에게 알리는 기능이 추가되었습니다.
- 심각도가 높은 경고(진짜 위반일 가능성이 높음)는 기본적으로 구독 소유자에게 사전에 알려줍니다.
- 이메일 알림 구성 페이지에서 전화 번호 필드가 제거되었습니다.

[보안 경고에 대한 이메일 알림 설정](security-center-provide-security-contact-details.md)에서 자세히 알아보세요.


### <a name="secure-score-doesnt-include-preview-recommendations"></a>보안 점수에 미리 보기 추천 사항이 포함되지 않음 

Security Center는 리소스, 구독 및 조직의 보안 이슈를 지속적으로 평가합니다. 그런 다음, 현재 보안 상황을 한눈에 파악할 수 있도록 모든 결과를 단일 점수에 집계합니다. 즉, 점수가 높을수록 식별된 위험 수준은 낮습니다.

새 위협이 발견되면 Security Center에서 새 추천 사항을 통해 새로운 보안 제안이 제공됩니다. 보안 점수가 예기치 않게 변경되지 않도록 방지하고 새 추천 사항이 점수에 영향을 주기 전에 이러한 새 추천 사항을 검색할 수 있는 유예 기간을 제공하기 위해 **미리 보기** 플래그로 지정된 추천 사항은 더 이상 보안 점수 계산에 포함되지 않습니다. 미리 보기 기간이 종료되면 점수에 기여할 수 있도록 가능한 경우 언제든지 수정해야 합니다.

또한 **미리 보기** 추천 사항은 리소스를 "비정상"으로 렌더링하지 않습니다.

미리 보기 추천 사항의 예는 다음과 같습니다.

:::image type="content" source="./media/secure-score-security-controls/example-of-preview-recommendation.png" alt-text="미리 보기 플래그가 있는 추천 사항":::

[보안 점수](secure-score-security-controls.md)에 대해 자세히 알아보세요.


### <a name="recommendations-now-include-a-severity-indicator-and-the-freshness-interval"></a>이제 추천 사항에 심각도 표시기 및 새로 고침 간격이 포함됨

추천 사항에 대한 세부 정보 페이지에는 이제 새로 고침 간격 표시기(관련될 때마다) 및 추천 사항의 심각도에 대한 명확한 표시가 포함됩니다.

:::image type="content" source="./media/release-notes/recommendations-severity-freshness-indicators.png" alt-text="새고 고침 및 심각도를 보여 주는 추천 사항 페이지":::



## <a name="august-2020"></a>2020년 8월

8월의 업데이트는 다음과 같습니다.

- [자산 인벤토리 - 자산의 보안 상태에 대한 강력하고 새로운 보기](#asset-inventory---powerful-new-view-of-the-security-posture-of-your-assets)
- [Azure Active Directory 보안 기본값에 대한 지원(다단계 인증용)이 추가됨](#added-support-for-azure-active-directory-security-defaults-for-multi-factor-authentication)
- [서비스 주체 추천 사항이 추가됨](#service-principals-recommendation-added)
- [VM에 대한 취약성 평가 - 추천 사항과 정책이 통합됨](#vulnerability-assessment-on-vms---recommendations-and-policies-consolidated)
- [새 AKS 보안 정책이 ASC_default 이니셔티브에 추가됨 - 프라이빗 미리 보기 고객만 사용](#new-aks-security-policies-added-to-asc_default-initiative--for-use-by-private-preview-customers-only)


### <a name="asset-inventory---powerful-new-view-of-the-security-posture-of-your-assets"></a>자산 인벤토리 - 자산의 보안 상태에 대한 강력하고 새로운 보기

Security Center의 자산 인벤토리(현재 미리 보기 상태)는 Security Center에 연결한 리소스의 보안 상태를 확인할 수 있는 방법을 제공합니다.

Security Center는 Azure 리소스의 보안 상태를 정기적으로 분석하여 잠재적인 보안 취약성을 식별합니다. 그런 다음, 이러한 취약성을 수정하는 방법에 대한 추천 사항을 제공합니다. 리소스에 수정되지 않은 추천 사항이 있으면 인벤토리에 표시됩니다.

보기 및 해당 필터를 사용하여 보안 상태 데이터를 검색하고 결과에 따라 추가 작업을 수행할 수 있습니다.

[자산 인벤토리](asset-inventory.md)에 대해 자세히 알아보세요.


### <a name="added-support-for-azure-active-directory-security-defaults-for-multi-factor-authentication"></a>Azure Active Directory 보안 기본값에 대한 지원(다단계 인증용)이 추가됨

Security Center에는 Microsoft의 무료 ID 보안 보호인 [보안 기본값](../active-directory/fundamentals/concept-fundamentals-security-defaults.md)에 대한 완전한 지원이 추가되었습니다.

보안 기본값은 일반적인 ID 관련 공격으로부터 조직을 보호하기 위해 미리 구성된 ID 보안 설정을 제공합니다. 보안 기본값은 이미 전체적으로 500만 개 이상의 테넌트를 보호하고 있으며, 5만 개의 테넌트도 Security Center를 통해 보호됩니다.

Security Center는 이제 보안 기본값을 사용하도록 설정되지 않은 Azure 구독을 식별할 때마다 보안 추천 사항을 제공합니다. 지금까지 Security Center는 AD(Azure Active Directory) Premium 라이선스의 일부인 조건부 액세스를 사용하는 다단계 인증을 사용하도록 추천했습니다. Azure AD 체험 라이선스를 사용하는 고객의 경우 이제 보안 기본값을 사용하도록 설정하는 것이 좋습니다. 

Microsoft의 목표는 더 많은 고객이 MFA를 사용하여 클라우드 환경을 보호하도록 권장하고, [보안 점수](secure-score-security-controls.md)에 가장 큰 영향을 미치는 가장 높은 위험 중 하나를 완화하는 것입니다.

[보안 기본값](../active-directory/fundamentals/concept-fundamentals-security-defaults.md)에 대해 자세히 알아보세요.


### <a name="service-principals-recommendation-added"></a>서비스 주체 추천 사항이 추가됨

관리 인증서를 사용하여 구독을 관리하는 Security Center 고객에게 서비스 주체로 전환하도록 추천하는 새 추천 사항이 추가되었습니다.

**관리 인증서 대신 서비스 주체를 사용하여 구독을 보호해야 합니다.** 라는 추천 사항은 서비스 주체 또는 Azure Resource Manager를 사용하여 구독을 더 안전하게 관리하도록 추천합니다. 

[Azure Active Directory의 애플리케이션 및 서비스 주체 개체](../active-directory/develop/app-objects-and-service-principals.md#service-principal-object)에 대해 자세히 알아보세요.


### <a name="vulnerability-assessment-on-vms---recommendations-and-policies-consolidated"></a>VM에 대한 취약성 평가 - 추천 사항과 정책이 통합됨

Security Center는 VM을 검사하여 해당 VM에서 취약성 평가 솔루션을 실행하고 있는지 여부를 검색합니다. 취약성 평가 솔루션을 찾을 수 없는 경우 Security Center는 배포를 간소화하기 위한 추천 사항을 제공합니다.

취약성이 발견되면 Security Center에서 필요에 따라 조사하고 수정할 수 있도록 결과를 요약한 추천 사항을 제공합니다.

사용하는 스캐너 유형에 관계없이 모든 사용자에게 일관된 환경을 보장하기 위해 4가지 추천 사항이 다음 2가지 추천 사항으로 통합되었습니다.

|통합 추천 사항|변경 내용 설명|
|----|:----|
|**취약성 평가 솔루션을 가상 머신에서 사용하도록 설정해야 함**|다음 두 가지 추천 사항을 대체합니다.<br> **•** 가상 머신에서 기본 제공 취약성 평가 솔루션 사용(Qualys에서 제공)(현재 사용되지 않음)(표준 계층에 포함됨)<br> **•** 가상 머신에 취약성 평가 솔루션을 설치해야 함(현재 사용되지 않음)(표준 및 체험 계층)|
|**가상 머신의 취약성을 수정해야 함**|다음 두 가지 추천 사항을 대체합니다.<br>**•** 가상 머신에서 발견한 취약성 수정(Qualys 제공)(현재 사용되지 않음)<br>**•** 취약성 평가 솔루션으로 취약성을 수정해야 함(현재 사용되지 않음)|
|||

이제 동일한 추천 사항을 사용하여 Qualys 또는 Rapid7과 같은 파트너로부터 Security Center의 취약성 평가 확장 또는 개인적으로 사용이 허가된 솔루션("BYOL")을 배포합니다.

또한 취약성이 발견되어 Security Center에 보고되면 이를 식별한 취약성 평가 솔루션에 관계없이 단일 추천 사항에서 결과를 알려줍니다.

#### <a name="updating-dependencies"></a>종속성 업데이트

이전 추천 사항 또는 정책 키/이름을 참조하는 스크립트, 쿼리 또는 자동화가 있는 경우 아래 표를 사용하여 참조를 업데이트합니다.

##### <a name="before-august-2020"></a>2020년 8월 이전

|권장|Scope|
|----|:----|
|**가상 머신에서 기본 제공 취약성 평가 솔루션 사용(Qualys에서 제공)**<br>키: 550e890b-e652-4d22-8274-60b3bdb24c63|기본 제공|
|**가상 머신에서 발견한 취약성 수정(Qualys 제공)**<br>키: 1195afff-c881-495e-9bc5-1486211ae03f|기본 제공|
|**가상 머신에 취약성 평가 솔루션을 설치해야 함**<br>키: 01b1ed4c-b733-4fee-b145-f23236e70cf3|BYOL|
|**취약성 평가 솔루션으로 취약성을 수정해야 합니다.**<br>키: 71992a2a-d168-42e0-b10e-6b45fa2ecddb|BYOL|
||||


|정책|Scope|
|----|:----|
|**가상 머신에서 취약성 평가를 사용하도록 설정해야 함**<br>정책 ID: 501541f7-f7e7-4cd6-868c-4190fdad3ac9|기본 제공|
|**취약성 평가 솔루션으로 취약성을 수정해야 함**<br>정책 ID: 760a85ff-6162-42b3-8d70-698e268f648c|BYOL|
||||


##### <a name="from-august-2020"></a>2020년 8월부터

|권장|Scope|
|----|:----|
|**취약성 평가 솔루션을 가상 머신에서 사용하도록 설정해야 함**<br>키: ffff0522-1e88-47fc-8382-2a80ba848f5d|기본 제공 + BYOL|
|**가상 머신의 취약성을 수정해야 함**<br>키: 1195afff-c881-495e-9bc5-1486211ae03f|기본 제공 + BYOL|
||||

|정책|Scope|
|----|:----|
|[**가상 머신에서 취약성 평가를 사용하도록 설정해야 함**](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2f501541f7-f7e7-4cd6-868c-4190fdad3ac9)<br>정책 ID: 501541f7-f7e7-4cd6-868c-4190fdad3ac9 |기본 제공 + BYOL|
||||


### <a name="new-aks-security-policies-added-to-asc_default-initiative--for-use-by-private-preview-customers-only"></a>새 AKS 보안 정책이 ASC_default 이니셔티브에 추가됨 - 프라이빗 미리 보기 고객만 사용

Kubernetes 워크로드에서 기본적으로 보안을 유지할 수 있도록 하기 위해 Security Center에서 Kubernetes 허용 제어를 사용하는 적용 옵션을 포함하여 Kubernetes 수준 정책 보안 강화 추천 사항을 추가합니다.

이 프로젝트의 초기 단계에는 프라이빗 미리 보기 및 ASC_default 이니셔티브에 추가된 새 정책(기본적으로 사용 안 함)이 포함됩니다.

이러한 정책은 무시해도 되지만 환경에는 영향을 주지 않습니다. 이러한 정책을 사용하도록 설정하려면 https://aka.ms/SecurityPrP 에서 미리 보기에 가입하고 다음 옵션 중에서 선택합니다.

1. **단일 미리 보기** – 이 프라이빗 미리 보기에만 조인합니다. "ASC 연속 검사"를 조인하려는 미리 보기로 명시적으로 언급합니다.
1. **진행 중인 프로그램** - 현재 및 향후 프라이빗 미리 보기에 추가됩니다. 프로필 및 개인 정보 계약을 완료해야 합니다.