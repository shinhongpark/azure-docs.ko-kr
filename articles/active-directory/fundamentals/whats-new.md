---
title: 새로운 기능은 무엇입니까? 릴리스 정보 - Azure Active Directory | Microsoft Docs
description: Azure Active Directory의 새로운 기능에 대해 알아봅니다. 최신 릴리스 정보, 알려진 문제, 버그 수정, 사용 되지 않는 기능 및 예정 된 변경 사항 등이 있습니다.
services: active-directory
author: ajburnle
manager: daveba
featureFlags:
- clicktale
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.subservice: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 12/18/2020
ms.author: ajburnle
ms.reviewer: dhanyahk
ms.custom: it-pro
ms.collection: M365-identity-device-management
ms.openlocfilehash: 12b5c95b67f8fada29914d3a8de559280e6145f8
ms.sourcegitcommit: 78ecfbc831405e8d0f932c9aafcdf59589f81978
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98724223"
---
# <a name="whats-new-in-azure-active-directory"></a>Azure Active Directory의 새로운 기능

>이 URL `https://docs.microsoft.com/api/search/rss?search=%22Release+notes+-+Azure+Active+Directory%22&locale=en-us`를 ![RSS 피드 판독기 아이콘](./media/whats-new/feed-icon-16x16.png) 피드 판독기에 복사하고 붙어넣어 업데이트를 위해 이 페이지를 다시 방문해야 할 때 알림을 받습니다.

Azure AD는 지속적인 향상되고 있습니다. 최신 개발 정보를 확인할 수 있도록 이 문서에서는 다음에 대한 정보를 제공합니다.

- 최신 릴리스
- 알려진 문제
- 버그 수정
- 사용되지 않는 기능
- 변경 계획

이 페이지는 매월 업데이트되므로 정기적으로 다시 방문해 주세요. 6 개월 보다 오래 된 항목을 찾는 경우 [Azure Active Directory의 새로운 기능에 대 한 보관](whats-new-archive.md)에서 찾을 수 있습니다.

---
## <a name="december-2020"></a>2020년 12월

### <a name="public-preview---azure-ad-b2c-phone-sign-up-and-sign-in-using-built-in-policy"></a>공개 미리 보기-기본 제공 정책을 사용 하 여 전화 등록 및 로그인 Azure AD B2C

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
B2C Phone 등록 및 로그인 기본 제공 정책을 사용 하 여 IT 관리자와 조직의 개발자는 최종 사용자가 사용자 흐름의 전화 번호를 사용 하 여 로그인 하 고 등록할 수 있습니다. 자세한 내용은 [사용자 흐름에 대 한 전화 등록 및 로그인 설정 (미리 보기)](../../active-directory-b2c/phone-authentication-user-flows.md) 을 참조 하세요.

---

### <a name="general-availability---security-defaults-now-enabled-for-all-new-tenants-by-default"></a>일반 공급-기본적으로 모든 새 테 넌 트에 보안 기본값을 사용 하도록 설정 되었습니다.

**유형:** 새로운 기능  
**서비스 범주:** 기타  
**제품 기능:** Id 보안 & 보호
 
사용자 계정을 보호 하기 위해 2020 년 11 월 12 일 이후에 생성 된 모든 새 테 넌 트에는 보안 기본값을 사용할 수 있는 상태로 제공 됩니다. 보안 기본값은 다음을 비롯 한 여러 정책을 적용 합니다.
- 모든 사용자 및 관리자가 Microsoft Authenticator 앱을 사용 하 여 MFA에 등록 해야 함
- 매일 로그인 할 때마다 MFA를 사용 하려면 중요 한 관리자 역할이 필요 합니다. 필요할 때마다 다른 모든 사용자에 게 MFA를 요청 하는 메시지가 표시 됩니다. 
- 레거시 인증은 테 넌 트 전체에서 차단 됩니다. 

자세한 내용은 [보안 기본값 이란?](../fundamentals/concept-fundamentals-security-defaults.md) 을 참조 하세요.

---

### <a name="general-availability---support-for-groups-with-up-to-250k-members-in-aadconnect"></a>일반 공급-AADConnect에 최대 250K의 구성원이 있는 그룹에 대 한 지원

**유형:** 변경된 기능  
**서비스 범주:** AD Connect  
**제품 기능:** Id 수명 주기 관리
 
Microsoft는 Azure AD Connect에 대한 새 엔드포인트(API)를 배포하여 Azure Active Directory에 대한 동기화 서비스 작업의 성능을 향상시켰습니다. 새 [V2 끝점](../hybrid/how-to-connect-sync-endpoint-api-v2.md)을 사용 하는 경우 Azure AD로 내보내기 및 가져오기에 대 한 성능이 크게 향상 됩니다. 이 새 끝점은 다음과 같은 시나리오를 지원 합니다.

- 최대 250k 구성원이 포함 된 그룹 동기화
- Azure AD로 내보내기 및 가져오기의 성능 향상

---

### <a name="general-availability---entitlement-management-available-for-tenants-in-azure-china-cloud"></a>Azure 중국 클라우드의 테 넌 트에 사용할 수 있는 일반 가용성-자격 관리

**유형:** 새로운 기능  
**서비스 범주:** 사용자 액세스 관리  
**제품 기능:** 자격 관리
 

이제 Azure 중국 클라우드의 모든 테 넌 트에 대해 자격 관리 기능을 사용할 수 있습니다. 자세한 내용은 [id 거 버 넌 스 설명서](https://docs.azure.cn/zh-cn/active-directory/governance/) 사이트를 참조 하세요.

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---december-2020"></a>Azure AD 응용 프로그램 갤러리의 새로운 프로 비전 커넥터-12 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** 타사 통합

다음과 같은 통합된 새 앱에 대한 사용자 계정을 만들고, 업데이트하고, 삭제하는 작업을 자동화할 수 있습니다.

- [디지털 프로세스 자동화를 위한 Bizagi Studio](../saas-apps/bizagi-studio-for-digital-process-automation-provisioning-tutorial.md)
- [CybSafe](../saas-apps/cybsafe-provisioning-tutorial.md)
- [GroupTalk](../saas-apps/grouptalk-provisioning-tutorial.md)
- [PaperCut 클라우드 인쇄 관리](../saas-apps/papercut-cloud-print-management-provisioning-tutorial.md)
- [구문 분석 가능](../saas-apps/parsable-provisioning-tutorial.md)
- [Shopify Plus](../saas-apps/shopify-plus-provisioning-tutorial.md)

자동화된 사용자 계정 프로비저닝을 사용하여 조직의 보안을 강화하는 방법에 대한 자세한 내용은 [Azure AD를 사용하여 SaaS 애플리케이션에 대한 사용자 프로비저닝 자동화](../app-provisioning/user-provisioning.md)를 참조하세요.
 
---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---december-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-12 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합
 
12 월 2020에 앱 갤러리에 페더레이션 지원과 함께 다음 18 개의 새로운 응용 프로그램이 추가 되었습니다.

[AwareGo](../saas-apps/awarego-tutorial.md), [HowNow SSO](https://gethownow.com/), [Zylab ONE 법적 보유](https://www.zylab.com/en/product/legal-hold), [Guider](http://www.guider-ai.com/), [소프트](https://www.softcrisis.se/sv/)위험, [Pims 365](http://www.omega365.com/pims), [InformaCast](../saas-apps/informacast-tutorial.md), [RetrieverMediaDatabase](../saas-apps/retrievermediadatabase-tutorial.md), [vonage](../saas-apps/vonage-tutorial.md), [작업 내 수 대시보드](../saas-apps/count-me-in-operations-dashboard-tutorial.md), [ProProfs 기술](../saas-apps/proprofs-knowledge-base-tutorial.md)자료, [rightcrowd 직원 관리](../saas-apps/rightcrowd-workforce-management-tutorial.md), [jll TRIRIGA](../saas-apps/jll-tririga-tutorial.md), [Shutterstock](../saas-apps/shutterstock-tutorial.md), [fortiweb 웹 응용 프로그램 방화벽](../saas-apps/linkedin-talent-solutions-tutorial.md), [LinkedIn 인재 Solutions](../saas-apps/linkedin-talent-solutions-tutorial.md), [inix 페더레이션 앱](../saas-apps/equinix-federation-app-tutorial.md), [kfadvance](../saas-apps/kfadvance-tutorial.md)

여기에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다. https://aka.ms/AppsTutorial

Azure AD 앱 갤러리에 응용 프로그램을 나열 하려면 여기에서 세부 정보를 참조 하세요. https://aka.ms/AzureADAppRequest

---

### <a name="navigate-to-teams-directly-from-my-access-portal"></a>내 액세스 포털에서 직접 팀으로 이동

**유형:** 변경된 기능  
**서비스 범주:** 사용자 액세스 관리 **제품 기능:** 자격 관리

이제 내 액세스 포털에서 팀을 직접 시작할 수 있습니다. 이렇게 하려면 [내 액세스](https://myaccess.microsoft.com/)에 로그인 하 고 **액세스 패키지** 로 이동한 다음 **활성** 탭으로 이동 하 여 이미 액세스할 수 있는 모든 액세스 패키지를 확인 합니다. 액세스 패키지를 확장 하 고 팀을 마우스로 가리키면 **열기** 단추를 클릭 하 여 실행할 수 있습니다. 

내 액세스 포털을 사용 하는 방법에 대 한 자세한 내용을 보려면 [AZURE AD 자격 관리에서 액세스 패키지](../governance/entitlement-management-request-access.md#sign-in-to-the-my-access-portal)에 대 한 액세스 요청으로 이동 하세요.

---

### <a name="public-preview---second-level-manager-can-be-set-as-alternate-approver"></a>공개 미리 보기-두 번째 수준 관리자를 대체 승인자로 설정할 수 있습니다.

**유형:** 변경된 기능  
**서비스 범주:** 사용자 액세스 관리  
**제품 기능:** 자격 관리

이제 권한 관리의 승인 프로세스에서 추가 옵션을 사용할 수 있습니다. 첫 번째 승인자에 대 한 승인자로 관리자를 선택 하는 경우 대체 승인자 인 다른 두 번째 수준 관리자를 선택 하 여 대체 승인자 필드에서 선택할 수 있습니다. 이 옵션을 선택 하는 경우 시스템에서 두 번째 수준 관리자를 찾을 수 없는 경우에 요청을 전달 하는 대체 승인자를 추가 해야 합니다.

자세한 내용은 [AZURE AD 자격 관리에서 액세스 패키지에 대 한 승인 설정 변경](../governance/entitlement-management-access-package-approval-policy.md#alternate-approvers)을 참조 하세요.

--- 

## <a name="november-2020"></a>2020년 11월

### <a name="azure-active-directory-tls-10-tls-11-and-3des-deprecation"></a>Azure Active Directory TLS 1.0, TLS 1.1 및 3DES 사용 중단

**유형:** 변경 계획  
**서비스 범주:** 모든 Azure AD 응용 프로그램  
**제품 기능:** 기준

Azure Active Directory은 전 세계 지역 Azure Active Directory에서 2021 년 6 월 30 일까 지 다음 프로토콜을 사용 중단 합니다.

- TLS 1.0
- TLS 1.1
- 3DES 암호 그룹 (TLS_RSA_WITH_3DES_EDE_CBC_SHA)

영향을 받는 환경은 다음과 같습니다.
- Azure 상용 클라우드
- Office 365 GCC 및 WW

관련 공지 모든 클라이언트 서버와 브라우저 서버 조합은 TLS 1.2 및 최신 암호 그룹을 사용 하 여 Azure, Office 365 및 Microsoft 365 서비스에 대 한 Azure Active Directory에 대 한 보안 연결을 유지 해야 합니다. 이 변경 [내용은 US Gov 클라우드에서 AZURE ACTIVE DIRECTORY TLS 1.0 & 1.1 및 3Des 암호 모음](whats-new.md#azure-active-directory-tls-10-tls-11-and-3des-deprecation-in-us-gov-cloud)사용 중단에 관련 되어 있습니다.

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---november-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-11 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합

11 월 2020에서는 페더레이션 지원이 포함 된 앱 갤러리에서 다음 52 새 응용 프로그램을 추가 했습니다.

[여행 & Expense Management](https://app.expenseonce.com/Account/Login), [Tribeloo](../saas-apps/tribeloo-tutorial.md), [Itslearning File Picker](https://pmteam.itslearning.com/), [Crises Control](../saas-apps/crises-control-tutorial.md), [CourtAlert](https://www.courtalert.com/), [StealthMail](https://stealthmail.com/), [Edmentum-연구 섬](https://app.studyisland.com/cfw/login/), [가상 위험 관리자](../saas-apps/virtual-risk-manager-tutorial.md), [u](../saas-apps/timu-tutorial.md), [Looker Analytics Platform](../saas-apps/looker-analytics-platform-tutorial.md), [Talview](https://recruit.talview.com/login), 실시간 변환기, [Klaxoon](https://access.klaxoon.com/login), [Podbean](../saas-apps/podbean-tutorial.md), [Zcal](https://zcal.co/signup), [expensemanager](https://api.expense-manager.com/), [Netsparker Enterprise](../saas-apps/netsparker-enterprise-tutorial.md), [En-trak 테 넌 트 환경 플랫폼](https://portal.en-trak.app/), [Appian](../saas-apps/appian-tutorial.md), [Panorays](../saas-apps/panorays-tutorial.md), [Builterra](https://portal.builterra.com/), [EVA 체크](https://my.evacheckin.com/organization)인, [HowNow WebApp SSO](../saas-apps/hownow-webapp-sso-tutorial.md),, [Lucid, GoBright](../saas-apps/coupa-risk-assess-tutorial.md) [(All Products)](../saas-apps/lucid-tutorial.md), [SailPoint](https://portal.brightbooking.eu/), [IdentityNow](../saas-apps/sailpoint-identitynow-tutorial.md),[Resource Central](../saas-apps/resource-central-tutorial.md), [UiPathStudioO365App](https://www.uipath.com/product/platform), [Jedox](../saas-apps/jedox-tutorial.md), [C-toapplication Security](../saas-apps/cequence-application-security-tutorial.md), [PerimeterX](../saas-apps/perimeterx-tutorial.md), [TrendMiner](../saas-apps/trendminer-tutorial.md), [Lexion](../saas-apps/lexion-tutorial.md) [,,](../saas-apps/workware-tutorial.md) [ProdPad](../saas-apps/prodpad-tutorial.md), [AWS clientvpn](../saas-apps/aws-clientvpn-tutorial.md), [appsec Flow SSO](../saas-apps/appsec-flow-sso-tutorial.md), [luum](../saas-apps/luum-tutorial.md), [운임 측정값](https://www.gpcsl.com/freight.html), [terraform 양식 클라우드](../saas-apps/terraform-cloud-tutorial.md), [특성 연구](../saas-apps/nature-research-tutorial.md), [Play Digital Signage](https://login.playsignage.com/login), [RemotePC](../saas-apps/remotepc-tutorial.md), [Prolorus](../saas-apps/prolorus-tutorial.md), [ATS](../saas-apps/hirebridge-ats-tutorial.md), [Teamgage](https://www.teamgage.com/Account/ExternalLoginAzure), [Roadmunk](../saas-apps/roadmunk-tutorial.md), [일출 소프트웨어 관계 CRM](https://cloud.relations-crm.com/), [Procaire](../saas-apps/procaire-tutorial.md), [전문가® eDriving: Business](https://www.edriving.com/), [Gradle Enterprise](https://gradle.com/)

여기에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다. https://aka.ms/AppsTutorial

Azure AD 앱 갤러리에서 응용 프로그램을 나열 하려면 여기에서 세부 정보를 읽으십시오. https://aka.ms/AzureADAppRequest

---

### <a name="public-preview---custom-roles-for-enterprise-apps"></a>공개 미리 보기-엔터프라이즈 앱에 대 한 사용자 지정 역할

**유형:** 새로운 기능  
**서비스 범주:** RBAC  
**제품 기능:** 액세스 제어
 
 [위임 된 엔터프라이즈 응용 프로그램 관리에 대 한 사용자 지정 RBAC 역할](../roles/custom-available-permissions.md) 은 현재 공개 미리 보기로 제공 됩니다. 이러한 새 권한은 앱 등록 관리에 대 한 사용자 지정 역할을 기반으로 하며,이를 통해 관리자에 게 액세스 하는 기능을 세밀 하 게 제어할 수 있습니다. 시간이 지남에 따라 Azure AD의 관리를 위임 하는 추가 권한이 릴리스됩니다.

몇 가지 일반적인 위임 시나리오는 다음과 같습니다.
- SAML 기반 Single Sign-On 응용 프로그램에 액세스할 수 있는 사용자 및 그룹 할당
- Azure AD 갤러리 응용 프로그램 만들기
- SAML 기반 Single Sign-On 응용 프로그램에 대 한 기본 SAML 구성 업데이트 및 읽기
- SAML 기반 Single Sign-On 응용 프로그램에 대 한 서명 인증서 관리
- SAML 기반 Single Sign-On 응용 프로그램에 대 한 만료 된 로그인 인증서 알림 전자 메일 주소 업데이트
- saml 토큰 서명 및 SAML 기반 Single Sign-On 응용 프로그램에 대 한 로그인 알고리즘 업데이트
- SAML 기반 Single Sign-On 응용 프로그램에 대 한 사용자 특성 및 클레임 만들기, 삭제 및 업데이트
- 프로 비전 작업을 설정, 해제 및 다시 시작할 수 있는 기능
- 특성 매핑에 대 한 업데이트
- 개체와 연결 된 프로 비전 설정을 읽을 수 있습니다.
- 서비스 사용자와 연결 된 프로 비전 설정을 읽을 수 있습니다.
- 프로 비전을 위해 응용 프로그램 액세스 권한을 부여 하는 기능

---

### <a name="public-preview---azure-ad-application-proxy-natively-supports-single-sign-on-access-to-applications-that-use-headers-for-authentication"></a>공개 미리 보기-Azure AD 응용 프로그램 프록시는 인증에 헤더를 사용 하는 응용 프로그램에 대 한 Single Sign-On 액세스를 기본적으로 지원

**유형:** 새로운 기능  
**서비스 범주:** 응용 프로그램 프록시  
**제품 기능:** 액세스 제어
 
Azure Active Directory (Azure AD) 응용 프로그램 프록시는 인증에 헤더를 사용 하는 응용 프로그램에 대 한 Single Sign-On 액세스를 기본적으로 지원 합니다. Azure AD에서 응용 프로그램에 필요한 헤더 값을 구성할 수 있습니다. 헤더 값은 응용 프로그램 프록시를 통해 응용 프로그램으로 전송 됩니다. 자세한 내용은 [Azure AD 앱 프록시를 사용 하 여 온-프레미스 앱에 대 한 헤더 기반 Single Sign-On](../manage-apps/application-proxy-configure-single-sign-on-with-headers.md)
 
---

### <a name="general-availability---azure-ad-b2c-phone-sign-up-and-sign-in-using-custom-policy"></a>일반 공급-사용자 지정 정책을 사용 하 여 전화 등록 및 로그인 Azure AD B2C

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C

전화 번호 등록 및 로그인을 통해 개발자와 기업은 고객이 SMS를 통해 사용자의 전화 번호로 전송 된 일회용 암호를 사용 하 여 등록 하 고 로그인 할 수 있습니다. 또한이 기능을 통해 고객은 휴대폰에 대 한 액세스 권한을 상실 한 경우 전화 번호를 변경할 수 있습니다. 사용자 지정 정책을 사용 하면 개발자와 기업이 페이지 사용자 지정을 통해 브랜드를 통신할 수 있습니다. [Azure AD B2C에서 사용자 지정 정책을 사용 하 여 전화 등록 및 로그인을 설정](../../active-directory-b2c/phone-authentication.md)하는 방법을 알아봅니다.
 
---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---november-2020"></a>Azure AD 응용 프로그램 갤러리의 새로운 프로 비전 커넥터-11 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** 타사 통합
 
다음과 같은 통합된 새 앱에 대한 사용자 계정을 만들고, 업데이트하고, 삭제하는 작업을 자동화할 수 있습니다.

- [Adobe ID 관리](../saas-apps/adobe-identity-management-provisioning-tutorial.md)
- [Blogin](../saas-apps/blogin-provisioning-tutorial.md)
- [Clarizen One](../saas-apps/clarizen-one-provisioning-tutorial.md)
- [Contentful](../saas-apps/contentful-provisioning-tutorial.md)
- [GitHub AE](../saas-apps/github-ae-provisioning-tutorial.md)
- [Playvox](../saas-apps/playvox-provisioning-tutorial.md)
- [PrinterLogic SaaS](../saas-apps/printer-logic-saas-provisioning-tutorial.md)
- [3 목-Tac Mobile](../saas-apps/tic-tac-mobile-provisioning-tutorial.md)
- [Visibly](../saas-apps/visibly-provisioning-tutorial.md)

자세한 내용은 [AZURE AD를 사용 하 여 SaaS 응용 프로그램에 대 한 사용자 프로 비전 자동화](../app-provisioning/user-provisioning.md)를 참조 하세요.
 
---

### <a name="public-preview---email-sign-in-with-proxyaddresses-now-deployable-via-staged-rollout"></a>공개 미리 보기-ProxyAddresses로 메일 Sign-In 준비 된 롤아웃을 통해 배포 가능

**유형:** 새로운 기능  
**서비스 범주:** 인증 (로그인)  
**제품 기능:** 사용자 인증
 
이제 테 넌 트 관리자는 스테이징 된 롤아웃을 사용 하 여 특정 Azure AD 그룹에 ProxyAddresses로 전자 메일 Sign-In을 배포할 수 있습니다. 그러면 홈 영역 검색 정책을 통해 전체 테 넌 트에 배포 하기 전에 기능을 사용해 볼 수 있습니다. 단계적 롤아웃을 통해 ProxyAddresses로 메일 Sign-In를 배포 하는 지침은 [설명서](../authentication/howto-authentication-use-email-signin.md)에 있습니다.
 
---

### <a name="limited-preview---sign-in-diagnostic"></a>제한 된 미리 보기-로그인 진단

**유형:** 새로운 기능  
**서비스 범주:** 보고  
**제품 기능:** 모니터링 및 보고
 
로그인 진단의 초기 미리 보기 릴리스에서는 이제 관리자가 사용자 로그인을 검토할 수 있습니다. 관리자는 로그인 중에 발생 하는 작업과 문제를 해결 하는 방법에 대 한 상황에 맞는 특정 세부 정보 및 지침을 받을 수 있습니다. 이 진단은 Azure AD 수준 및 조건부 액세스 진단 및 분석 블레이드에서 모두 사용할 수 있습니다. 이 릴리스에 포함 된 진단 시나리오는 조건부 액세스, Multi-Factor Authentication 및 성공한 로그인입니다.

자세한 내용은 [AZURE AD의 로그인 진단 이란?](../reports-monitoring/overview-sign-in-diagnostics.md)을 참조 하세요.
 
---

### <a name="improved-unfamiliar-sign-in-properties"></a>잘 모르는 로그인 속성 개선

**유형:** 변경된 기능  
**서비스 범주:** Id 보호  
**제품 기능:** Id 보안 & 보호

  익숙하지 않은 로그인 속성 검색이 업데이트 되었습니다. 고객은 더 높은 위험 수준의 로그인 속성 검색을 확인할 수 있습니다. 자세한 내용은 [위험 이란?](../identity-protection/concept-identity-protection-risks.md) 을 참조 하세요.
 
---

### <a name="public-preview-refresh-of-cloud-provisioning-agent-now-available-version-112810"></a>이제 클라우드 프로 비전 에이전트의 공개 미리 보기 새로 고침을 사용할 수 있습니다 (버전: 1.1.281.0).

**유형:** 변경된 기능  
**서비스 범주:** Azure AD 클라우드 프로 비전  
**제품 기능:** Id 수명 주기 관리
 
클라우드 프로 비전 에이전트는 공개 미리 보기로 출시 되었으며 이제 포털을 통해 사용할 수 있습니다. 이 릴리스에는 도메인에 대 한 GMSA 지원을 포함 하 여 향상 된 보안을 제공 하 고, 초기 동기화 주기를 개선 하 고, 대량 그룹에 대 한 지원이 포함 되어 있습니다. 자세한 내용은 릴리스 버전 [기록을](../app-provisioning/provisioning-agent-release-version-history.md) 확인 하세요. 
 
---

### <a name="bitlocker-recovery-key-api-endpoint-now-under-informationprotection"></a>이제/Ds 보호 상태에서 BitLocker 복구 키 API 끝점

**유형:** 변경된 기능  
**서비스 범주:** 장치 액세스 관리  
**제품 기능:** 장치 수명 주기 관리
 
이전에는/bitlocker 끝점을 통해 BitLocker 키를 복구할 수 있었습니다. 결국이 끝점을 사용 중단 고객이 이제/informationProtection. 아래에 있는 API를 사용 하기 시작 합니다. 

이러한 변경 내용을 반영 하기 위해 설명서에 대 한 업데이트는 [BitLocker RECOVERY API](/graph/api/resources/bitlockerrecoverykey?view=graph-rest-beta) 를 참조 하세요.

---

### <a name="general-availability-of-application-proxy-support-for-remote-desktop-services-html5-web-client"></a>원격 데스크톱 서비스 HTML5 웹 클라이언트에 대 한 응용 프로그램 프록시 지원의 일반 가용성

**유형:** 변경된 기능  
**서비스 범주:** 응용 프로그램 프록시  
**제품 기능:** 액세스 제어
 
Azure AD 응용 프로그램 프록시 원격 데스크톱 서비스 (RDS) 웹 클라이언트는 이제 일반 공급으로 제공 됩니다. 사용자는 RDS 웹 클라이언트를 사용 하 여 Microsoft Edge, Internet Explorer 11, Google Chrome 등의 HTLM5 지원 브라우저를 통해 원격 데스크톱 인프라에 액세스할 수 있습니다. 사용자는 어디서 나 로컬 장치를 사용 하는 것 처럼 원격 앱 또는 데스크톱과 상호 작용할 수 있습니다. 

Azure AD 응용 프로그램 프록시을 사용 하 여 모든 유형의 리치 클라이언트 앱에 대 한 사전 인증 및 조건부 액세스 정책을 적용 하 여 RDS 배포의 보안을 강화할 수 있습니다. 자세히 알아보려면 [Azure로 원격 데스크톱 게시 AD 응용 프로그램 프록시](../manage-apps/application-proxy-integrate-with-remote-desktop-services.md) 를 참조 하세요.
 
---

### <a name="new-enhanced-dynamic-group-service-is-in-public-preview"></a>새 향상 된 동적 그룹 서비스는 공개 미리 보기 상태입니다.

**유형:** 변경된 기능  
**서비스 범주:** 그룹 관리  
**제품 기능:** 협업
 
향상 된 동적 그룹 서비스는 현재 공개 미리 보기로 제공 됩니다. 새 서비스를 사용 하 여 테 넌 트에 동적 그룹을 만들 수 있습니다. 동적 그룹을 만드는 데 필요한 시간은 테 넌 트의 크기 대신 생성 되는 그룹의 크기에 비례 합니다. 이 업데이트는 고객이 더 작은 그룹을 만들 때 큰 테 넌 트의 성능을 크게 향상 시킵니다. 

또한 새 서비스는 몇 분 내에 특성을 변경 하 여 멤버 추가 및 제거를 완료 하는 것을 목표로 합니다. 또한 단일 처리 오류는 테 넌 트 처리를 차단 하지 않습니다. 동적 그룹을 만드는 방법에 대 한 자세한 내용은 [설명서](../enterprise-users/groups-create-rule.md)를 참조 하세요.
 
---
## <a name="october-2020"></a>2020년 10월

### <a name="azure-ad-on-premises-hybrid-agents-impacted-by-azure-tls-certificate-changes"></a>Azure TLS 인증서 변경의 영향을 받는 azure AD 온-프레미스 하이브리드 에이전트

**유형:** 변경 계획  
**서비스 범주:** 해당 없음  
**제품 기능:** 플랫폼

Microsoft는 다른 루트 CA(인증 기관)의 TLS 인증서를 사용하도록 Azure 서비스를 업데이트하 고 있습니다. 이 업데이트는 CA/브라우저 포럼 기준 요구 사항 중 하나를 준수 하지 않는 현재 CA 인증서로 인해 발생 합니다. 이 변경 내용은 고정 된 루트 인증서 목록과 함께 확정 된 환경을 갖춘 온-프레미스에 설치 된 Azure AD 하이브리드 에이전트에 영향을 주므로 새 인증서 발급자를 신뢰 하도록 업데이트 해야 합니다.

이렇게 변경 하면 즉시 조치를 취하지 않는 경우 서비스가 중단 됩니다. 이러한 에이전트에는 온-프레미스에 대 한 원격 액세스를 위한 [응용 프로그램 프록시 커넥터](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AppProxy) , 사용자가 동일한 암호를 사용 하 여 응용 프로그램에 로그인 할 수 있도록 하는 [통과 인증](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect) 에이전트 및 AZURE ad sync에 ad를 수행 하는 [클라우드 프로 비전 미리 보기](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect) 에이전트가 포함 됩니다. 

특정 CRL (인증서 해지 목록) 다운로드에 대 한 아웃 바운드 호출을 허용 하도록 방화벽 규칙이 설정 된 환경이 있는 경우 다음 CRL 및 OCSP Url을 허용 해야 합니다. 에 대 한 액세스를 사용 하도록 설정 하는 변경 내용 및 CRL 및 OCSP Url에 대 한 자세한 내용은  [AZURE TLS 인증서 변경 내용](../../security/fundamentals/tls-certificate-changes.md)을 참조 하세요.

---

### <a name="provisioning-events-will-be-removed-from-audit-logs-and-published-solely-to-provisioning-logs"></a>프로 비전 이벤트는 감사 로그에서 제거 되 고 프로 비전 로그에만 게시 됩니다.

**유형:** 변경 계획  
**서비스 범주:** 보고  
**제품 기능:** 모니터링 및 보고
 
SCIM [프로 비전 서비스](../app-provisioning/user-provisioning.md) 에의 한 활동은 감사 로그와 프로 비전 로그 모두에 로깅됩니다. 여기에는 ServiceNow의 사용자 만들기, GSuite의 그룹 또는 AWS에서 역할 가져오기 등의 작업이 포함 됩니다. 향후 이러한 이벤트는 프로 비전 로그에만 게시 됩니다. 이 변경은 로그에서 중복 이벤트를 방지 하기 위해 구현 되며 log analytics에서 로그를 사용 하는 고객에 의해 발생 하는 추가 비용이 발생 하지 않도록 합니다. 

날짜가 완료 되 면 업데이트를 제공 합니다. 이 사용 중단은 2020 년에 계획 되지 않습니다. 

> [!NOTE]
> 이는 프로 비전 서비스에서 내보낸 동기화 이벤트 외부의 감사 로그에 있는 이벤트에는 영향을 주지 않습니다. 응용 프로그램 생성, 조건부 액세스 정책, 디렉터리의 사용자 등의 이벤트는 감사 로그에서 계속 내보내집니다. [자세히 알아보기](../reports-monitoring/concept-provisioning-logs.md?context=azure%2factive-directory%2fapp-provisioning%2fcontext%2fapp-provisioning-context).
 

---

### <a name="azure-ad-on-premises-hybrid-agents-impacted-by-azure-transport-layer-security-tls-certificate-changes"></a>Azure AD 온-프레미스 하이브리드 에이전트가 Azure TLS (전송 계층 보안) 인증서 변경의 영향을 받습니다.

**유형:** 변경 계획  
**서비스 범주:** 해당 없음  
**제품 기능:** 플랫폼
 
Microsoft는 다른 루트 CA(인증 기관)의 TLS 인증서를 사용하도록 Azure 서비스를 업데이트하 고 있습니다. CA/브라우저 포럼 기준 요구 사항 중 하나를 따르지 않는 현재 CA 인증서 때문에 업데이트가 수행 됩니다. 이 변경 내용은 고정 된 루트 인증서 목록을 사용 하 여 확정 된 환경을 보유 하 고 있는 온-프레미스에 설치 된 Azure AD 하이브리드 에이전트에 영향을 줍니다. 이러한 에이전트는 새 인증서 발급자를 신뢰 하도록 업데이트 해야 합니다.

이렇게 변경 하면 즉시 조치를 취하지 않는 경우 서비스가 중단 됩니다. 이러한 에이전트는 다음과 같습니다. 
- 온-프레미스에 대 한 원격 액세스를 위한 [응용 프로그램 프록시 커넥터](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AppProxy) 
- 사용자가 동일한 암호를 사용 하 여 응용 프로그램에 로그인 할 수 있도록 하는 [통과 인증](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect) 에이전트
- Azure AD sync에 AD를 수행 하는 [클라우드 프로 비전 미리 보기](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/AzureADConnect) 에이전트. 

특정 CRL (인증서 해지 목록) 다운로드에 대 한 아웃 바운드 호출을 허용 하도록 방화벽 규칙이 설정 된 환경이 있는 경우 CRL 및 OCSP Url을 허용 해야 합니다. 에 대 한 액세스를 사용 하도록 설정 하는 변경 내용 및 CRL 및 OCSP Url에 대 한 자세한 내용은  [AZURE TLS 인증서 변경 내용](../../security/fundamentals/tls-certificate-changes.md)을 참조 하세요.
 
---

### <a name="azure-active-directory-tls-10-tls-11-and-3des-deprecation-in-us-gov-cloud"></a>US Gov 클라우드에서 Azure Active Directory TLS 1.0, TLS 1.1 및 3DES 사용 중단

**유형:** 변경 계획  
**서비스 범주:** 모든 Azure AD 응용 프로그램  
**제품 기능:** 기준
 
Azure Active Directory는 2021 년 3 월 31 일까 지 다음 프로토콜을 사용 중단 합니다.
- TLS 1.0
- TLS 1.1
- 3DES 암호 그룹 (TLS_RSA_WITH_3DES_EDE_CBC_SHA)

모든 클라이언트-서버 및 브라우저 서버 조합에서는 TLS 1.2 및 최신 암호 그룹을 사용 하 여 Azure, Office 365 및 Microsoft 365 서비스의 Azure Active Directory에 대 한 보안 연결을 유지 해야 합니다.

영향을 받는 환경은 다음과 같습니다.
- Azure US Gov
- [Office 365 GCC High & DoD](/microsoft-365/compliance/tls-1-2-in-office-365-gcc)
 
---

### <a name="assign-applications-to-roles-on-au-and-object-scope"></a>AU 및 개체 범위에서 역할에 응용 프로그램 할당

**유형:** 새로운 기능  
**서비스 범주:** RBAC  
**제품 기능:** 액세스 제어
 
이 기능을 사용 하면 관리 단위 범위에 대 한 관리자 역할에 응용 프로그램 (SPN)을 할당할 수 있습니다. 자세한 내용은 [관리 단위에 범위 지정 역할 할당](../roles/admin-units-assign-roles.md)을 참조 하세요.

---

### <a name="now-you-can-disable-and-delete-guest-users-when-theyre-denied-access-to-a-resource"></a>이제 리소스에 대 한 액세스가 거부 된 경우 게스트 사용자를 사용 하지 않도록 설정 하 고 삭제할 수 있습니다.

**유형:** 새로운 기능  
**서비스 범주:** 액세스 검토  
**제품 기능:** Id 거 버 넌 스
 
비활성화 및 삭제는 조직이 그룹 및 앱에서 외부 게스트를 더 효율적으로 관리할 수 있도록 Azure AD 액세스 검토의 고급 제어입니다. 액세스 검토에서 게스트가 거부 된 경우 **disable 및 delete** 는 30 일 동안 로그인 하지 못하도록 자동으로 차단 합니다. 30 일 후에는 테 넌 트에서 완전히 제거 됩니다.

이 기능에 대 한 자세한 내용은 [AZURE AD 액세스 검토를 사용 하 여 외부 Id 비활성화 및 삭제 (미리 보기)](../governance/access-reviews-external-users.md#disable-and-delete-external-identities-with-azure-ad-access-reviews-preview)를 참조 하세요.
 
---

### <a name="access-review-creators-can-add-custom-messages-in-emails-to-reviewers"></a>액세스 검토 작성자는 전자 메일의 사용자 지정 메시지를 검토자에 게 추가할 수 있습니다.

**유형:** 새로운 기능  
**서비스 범주:** 액세스 검토  
**제품 기능:** Id 거 버 넌 스
 
Azure AD 액세스 검토에서 검토를 만드는 관리자는 이제 검토자에 게 사용자 지정 메시지를 작성할 수 있습니다. 검토자는 검토를 완료 하 라는 메시지를 받은 전자 메일에 메시지를 표시 합니다. 이 기능을 사용 하는 방법에 대 한 자세한 내용은 [하나 이상의 액세스 검토 만들기](../governance/create-access-review.md#create-one-or-more-access-reviews) 섹션의 14 단계를 참조 하세요.

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---october-2020"></a>Azure AD 응용 프로그램 갤러리의 새로운 프로 비전 커넥터-10 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** 타사 통합
 
다음과 같은 통합된 새 앱에 대한 사용자 계정을 만들고, 업데이트하고, 삭제하는 작업을 자동화할 수 있습니다.

- [Apple Business Manager](../saas-apps/apple-business-manager-provision-tutorial.md)
- [Apple School Manager](../saas-apps/apple-school-manager-provision-tutorial.md)
- [Code42](../saas-apps/code42-provisioning-tutorial.md)
- [AlertMedia](../saas-apps/alertmedia-provisioning-tutorial.md)
- [OpenText Directory Services](../saas-apps/open-text-directory-services-provisioning-tutorial.md)
- [Cinode](../saas-apps/cinode-provisioning-tutorial.md)
- [글로벌 릴레이 ID 동기화](../saas-apps/global-relay-identity-sync-provisioning-tutorial.md)

자동화된 사용자 계정 프로비저닝을 사용하여 조직의 보안을 강화하는 방법에 대한 자세한 내용은 [Azure AD를 사용하여 SaaS 애플리케이션에 대한 사용자 프로비저닝 자동화](../app-provisioning/user-provisioning.md)를 참조하세요.
 
---

### <a name="integration-assistant-for-azure-ad-b2c"></a>Azure AD B2C 용 Integration assistant

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
이제 Azure AD B2C 앱 등록에서 Integration Assistant (미리 보기) 환경을 사용할 수 있습니다. 이 환경에서는 일반적인 시나리오에 맞게 응용 프로그램을 구성 하는 방법을 안내 합니다. [Microsoft id 플랫폼 모범 사례 및 권장 사항](../develop/identity-platform-integration-checklist.md)에 대해 자세히 알아보세요.
 
---

### <a name="view-role-template-id-in-azure-portal-ui"></a>Azure Portal UI에서 역할 템플릿 ID 보기

**유형:** 새로운 기능  
**서비스 범주:** Azure 역할  
**제품 기능:** 액세스 제어
 

이제 Azure Portal에서 각 Azure AD 역할의 템플릿 ID를 볼 수 있습니다. Azure AD에서 선택한 역할에 대 한  **설명** 을 선택 합니다. 

고객은 표시 이름 대신 PowerShell 스크립트 및 코드에서 역할 템플릿 Id를 사용 하는 것이 좋습니다. 역할 템플릿 ID는 역할 및 [Roledefinition](/graph/api/resources/unifiedroledefinition?view=graph-rest-beta) 개체를 [directoryroles](/graph/api/resources/directoryrole) 에 사용할 수 있도록 지원 됩니다. 역할 템플릿 Id에 대 한 자세한 내용은 [역할 템플릿 id](../roles/permissions-reference.md#role-template-ids)를 참조 하십시오.

---

### <a name="api-connectors-for-azure-ad-b2c-sign-up-user-flows-is-now-in-public-preview"></a>Azure AD B2C 등록 사용자 흐름에 대 한 API 커넥터는 현재 공개 미리 보기로 제공 됩니다.

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 

이제 API 커넥터를 Azure Active Directory B2C 사용할 수 있습니다. API 커넥터를 사용 하면 웹 Api를 사용 하 여 등록 사용자 흐름을 사용자 지정 하 고 외부 클라우드 시스템과 통합할 수 있습니다. API 커넥터를 사용 하 여 다음을 수행할 수 있습니다.

- 사용자 지정 승인 워크플로와 통합
- 사용자 입력 데이터 유효성 검사
- 사용자 특성 덮어쓰기 
- 사용자 지정 비즈니스 논리 실행 

 [API 커넥터를 사용 하 여 등록 설명서를 사용자 지정 하 고 확장](../../active-directory-b2c/api-connectors-overview.md) 하 여 자세한 내용을 알아보세요.

---

### <a name="state-property-for-connected-organizations-in-entitlement-management"></a>자격 관리에서 연결 된 조직의 상태 속성

**유형:** 새로운 기능  
**서비스 범주:** 디렉터리 관리 **제품 기능:** 자격 관리
 

 이제 연결 된 모든 조직에는 "State" 라는 추가 속성이 있습니다. 상태는 "모든 구성 된 연결 된 조직"을 참조 하는 정책에서 연결 된 조직을 사용 하는 방법을 제어 합니다. 이 값은 "구성" (조직이 "all" 절을 사용 하는 정책 범위에 있음) 또는 "제안 됨" (조직이 범위에 있지 않음을 의미 함)입니다.  

수동으로 만든 연결 된 조직의 기본 설정은 "구성 됨"입니다. 한편, 인터넷의 모든 사용자가 액세스를 요청 하도록 허용 하는 정책을 통해 생성 된 자동으로 생성 된 항목은 기본적으로 "제안 됨"으로 나타납니다.  9 월 9 2020 일 이전에 생성 된 모든 연결 된 조직은 "구성 됨"으로 설정 됩니다. 관리자는 필요에 따라이 속성을 업데이트할 수 있습니다. [자세히 알아보기](../governance/entitlement-management-organization.md#managing-a-connected-organization-programmatically).
 

---

### <a name="azure-active-directory-external-identities-now-has-premium-advanced-security-settings-for-b2c"></a>이제 Azure Active Directory 외부 Id에 B2C에 대 한 프리미엄 고급 보안 설정이 있습니다.

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
Id 보호의 위험 기반 조건부 액세스 및 위험 검색 기능을 이제 [Azure AD B2C](../..//active-directory-b2c/conditional-access-identity-protection-overview.md)에서 사용할 수 있습니다. 이제 고객은 다음과 같은 고급 보안 기능을 사용 하 여 다음을 수행할 수 있습니다.
- Intelligent insights를 활용 하 여 B2C apps 및 최종 사용자 계정으로 위험을 평가 합니다. 검색에는 비정상적인 이동, 익명 IP 주소, 맬웨어 연결 IP 주소 및 Azure AD 위협 인텔리전스가 포함 됩니다. 포털 및 API 기반 보고서를 사용할 수도 있습니다.
- B2C 사용자에 대 한 적응 인증 정책을 구성 하 여 위험을 자동으로 해결 합니다. 앱 개발자와 관리자는 검색 된 사용자 위험 수준에 따라 MFA (multi-factor authentication)를 요구 하거나 액세스를 차단 하 여 실시간 위험을 완화 하 고, 위치, 그룹 및 앱을 기반으로 하 여 추가 제어를 사용할 수 있습니다.
- Azure AD B2C 사용자 흐름 및 사용자 지정 정책과 통합 합니다. Azure AD B2C의 기본 제공 사용자 흐름에서 조건을 트리거하거나 B2C 사용자 지정 정책에 통합할 수 있습니다. B2C 사용자 흐름의 다른 측면에서와 마찬가지로 최종 사용자 환경 메시지를 사용자 지정할 수 있습니다. 사용자 지정은 조직의 음성, 브랜드 및 완화 대안에 따라 지정 됩니다.
 
---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---october-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-10 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합
 
2020 년 10 월에 앱 갤러리에 페더레이션 지원과 함께 다음 27 개의 새 응용 프로그램을 추가 했습니다.

[](../saas-apps/sentry-tutorial.md) [Bumblebee-생산성 슈퍼 앱](https://app.yellowmessenger.com/user/login), [ABBYY FlexiCapture Cloud](../saas-apps/abbyy-flexicapture-cloud-tutorial.md), [EAComposer](../saas-apps/eacomposer-tutorial.md), [genesys는 Azure](https://apps.mypurecloud.com/msteams-integration/), [영역 기술 포털](https://portail.zonetechnologie.com/signin), [Beautiful.ai](../saas-apps/beautiful.ai-tutorial.md), [Datawiza Access Broker](https://console.datawiza.com/), [zokri](https://app.zokri.com/), [checkproof](../saas-apps/checkproof-tutorial.md), [Ecochallenge.org](https://events.ecochallenge.org/users/login), [Atspoke](http://atspoke.com/login), [약속 미리 알림](https://app.appointmentreminder.co.nz/account/login), [클라우드. 시장](https://cloud.market/), [TravelPerk](../saas-apps/travelperk-tutorial.md), [Greetly](https://app.greetly.com/), [OrgVitality SSO](../saas-apps/orgvitality-sso-tutorial.md), [웹 Cargo Air](../saas-apps/web-cargo-air-tutorial.md), [루프 흐름 CRM](../saas-apps/loop-flow-crm-tutorial.md), [starmind](../saas-apps/starmind-tutorial.md), [워크](https://hrm.workstem.com/login), [소매 Zipline](../saas-apps/retail-zipline-tutorial.md), [hoxhunt](../saas-apps/hoxhunt-tutorial.md), [mevisio](../saas-apps/mevisio-tutorial.md), [Samsara](../saas-apps/samsara-tutorial.md), [Nimbus](../saas-apps/nimbus-tutorial.md), [펄스 보안 가상 Traffic Manager](../saas-apps/pulse-secure-virtual-traffic-manager-tutorial.md)

여기에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다. https://aka.ms/AppsTutorial

Azure AD 앱 갤러리에서 응용 프로그램을 나열 하려면 여기에서 세부 정보를 읽으십시오. https://aka.ms/AzureADAppRequest

---

### <a name="provisioning-logs-can-now-be-streamed-to-log-analytics"></a>이제 프로 비전 로그를 log analytics로 스트리밍할 수 있습니다.

**유형:** 새로운 기능  
**서비스 범주:** 보고  
**제품 기능:** 모니터링 및 보고
 

프로 비전 로그를 log analytics에 게시 하 여 다음을 수행 합니다.
- 30 일 넘게 프로 비전 로그 저장
- 사용자 지정 경고 및 알림 정의
- 로그를 시각화 하는 대시보드 빌드
- 복잡 한 쿼리를 실행 하 여 로그 분석 

기능을 사용 하는 방법을 알아보려면 [프로 비전이 Azure Monitor 로그와 통합 하는 방법 이해](../app-provisioning/application-provisioning-log-analytics.md)를 참조 하세요.
 
---

### <a name="provisioning-logs-can-now-be-viewed-by-application-owners"></a>이제 응용 프로그램 소유자가 프로 비전 로그를 볼 수 있습니다.

**유형:** 변경된 기능  
**서비스 범주:** 보고  
**제품 기능:** 모니터링 및 보고
 
이제 응용 프로그램 소유자가 프로 비전 서비스에서 작업을 모니터링 하 고, 권한 있는 역할을 제공 하거나 병목 상태를 제공 하지 않고 문제를 해결할 수 있습니다. [자세히 알아보기](../reports-monitoring/concept-provisioning-logs.md).
 
---

### <a name="renaming-10-azure-active-directory-roles"></a>10 개의 Azure Active Directory 역할 이름 바꾸기

**유형:** 변경된 기능  
**서비스 범주:** Azure 역할  
**제품 기능:** 액세스 제어
 
일부 AD (Azure Active Directory) 기본 제공 역할에는 Microsoft 365 관리 센터, Azure AD 포털 및 Microsoft Graph에 표시 되는 이름과 다른 이름이 있습니다. 이러한 불일치는 자동화 된 프로세스에서 문제를 일으킬 수 있습니다. 이 업데이트를 사용 하면 10 개의 역할 이름 이름을 바꿔서 일관 되도록 합니다. 다음 표에는 새 역할 이름이 있습니다.

![새 역할 이름 표](media/whats-new/azure-role.png)

---

### <a name="azure-ad-b2c-support-for-auth-code-flow-for-spas-using-msal-js-2x"></a>MSAL JS 2.x를 사용 하는 것 처럼 SPAs 인증 코드 흐름에 대 한 지원 Azure AD B2C

**유형:** 변경된 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
MSAL.js 버전 2.x에는 이제 SPAs (단일 페이지 웹 앱)에 대 한 인증 코드 흐름 지원이 포함 됩니다. Azure AD B2C는 이제 Azure Portal에서 SPA 앱 유형 사용을 지원 하 고 단일 페이지 앱에 대해 PKCE에서 MSAL.js 인증 코드 흐름을 사용할 수 있습니다. 이렇게 하면 Azure AD B2C를 사용 하 여 최신 브라우저로 SSO를 유지 하 고 최신 인증 프로토콜 권장 사항을 준수 하는 데 사용할 수 있습니다. [Azure Active Directory B2C 자습서의 SPA (단일 페이지 응용 프로그램) 등록](../../active-directory-b2c/tutorial-register-spa.md) 을 시작 하세요.

---

### <a name="updates-to-remember-multi-factor-authentication-mfa-on-a-trusted-device-setting"></a>신뢰할 수 있는 장치 설정에서 Multi-Factor Authentication (MFA)를 기억할 업데이트

**유형:** 변경된 기능  
**서비스 범주:** MFA  
**제품 기능:** Id 보안 & 보호
 

최근 최대 365 일 동안 인증을 확장 하도록 신뢰할 수 있는 장치 기능에서 [MFA (기억을 Multi-Factor Authentication](../authentication/howto-mfa-mfasettings.md#remember-multi-factor-authentication) )를 업데이트 했습니다. Azure AD (Azure Active Directory) 프리미엄 라이선스는 재인증 설정에 더 많은 유연성을 제공 하는 [조건부 액세스 – 로그인 빈도 정책을](../conditional-access/howto-conditional-access-session-lifetime.md#user-sign-in-frequency) 사용할 수도 있습니다.

최적의 사용자 환경에서는 신뢰할 수 있는 장치에 대 한 MFA 기억을 설정 하는 대신 조건부 액세스 로그인 빈도를 사용 하 여 신뢰할 수 있는 장치, 위치 또는 낮은 위험 세션에서 세션 수명을 연장 하는 것이 좋습니다. 시작 하려면 [재인증 환경 최적화에 대 한 최신 지침](../authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime.md)을 검토 하세요.

---

## <a name="september-2020"></a>2020년 9월

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---september-2020"></a>Azure AD 응용 프로그램 갤러리의 새로운 프로 비전 커넥터-9 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** 타사 통합
 
다음과 같은 통합된 새 앱에 대한 사용자 계정을 만들고, 업데이트하고, 삭제하는 작업을 자동화할 수 있습니다.

- [Coda](../saas-apps/coda-provisioning-tutorial.md)
- [Cofense 수신자 동기화](../saas-apps/cofense-provision-tutorial.md)
- [InVision](../saas-apps/invision-provisioning-tutorial.md)
- [myday](../saas-apps/myday-provision-tutorial.md)
- [SAP Analytics Cloud](../saas-apps/sap-analytics-cloud-provisioning-tutorial.md)
- [Webroot 보안 인식](../saas-apps/webroot-security-awareness-training-provisioning-tutorial.md)

자동화된 사용자 계정 프로비저닝을 사용하여 조직의 보안을 강화하는 방법에 대한 자세한 내용은 [Azure AD를 사용하여 SaaS 애플리케이션에 대한 사용자 프로비저닝 자동화](../app-provisioning/user-provisioning.md)를 참조하세요.
 
---
### <a name="cloud-provisioning-public-preview-refresh"></a>클라우드 프로 비전 공개 미리 보기 새로 고침

**유형:** 새로운 기능  
**서비스 범주:** Azure AD 클라우드 프로 비전 **제품 기능:** Id 수명 주기 관리
 
Azure AD Connect 클라우드 프로 비전 공개 미리 보기 새로 고침 기능을 통해 사용자 의견에서 개발 된 두 가지 주요 향상 기능 

- Azure Portal를 통한 특성 매핑 환경

    IT 관리자는이 기능을 통해 현재 제공 되는 다양 한 매핑 유형을 사용 하 여 AD의 사용자, 그룹 또는 연락처 특성을 Azure AD에 매핑할 수 있습니다. 특성 매핑은 Active Directory에서 Azure Active Directory로 전달 되는 특성의 값을 표준화 하는 데 사용 되는 기능입니다. AD에서 Azure AD로 특성 값을 직접 매핑할지 또는 식을 사용 하 여 사용자를 프로 비전 할 때 특성 값을 변환할 수 있는지 여부를 결정할 수 있습니다. [자세한 정보](../cloud-provisioning/how-to-attribute-mapping.md)

- 주문형 프로 비전 또는 테스트 사용자 환경

    구성을 설정한 후에는 범위 내 모든 사용자에 게 적용 하기 전에 사용자 변환이 예상 대로 작동 하는지 테스트 하는 것이 좋습니다. 주문형 프로 비전을 사용 하 여 IT 관리자는 AD 사용자의 DN (고유 이름)을 입력 하 고 예상 대로 동기화 되는지 확인할 수 있습니다. 주문형 프로 비전을 사용 하면 이전에 수행한 특성 매핑이 예상 대로 작동 하는지 확인할 수 있습니다. [자세한 내용](../cloud-provisioning/how-to-on-demand-provision.md)
 
---

### <a name="audited-bitlocker-recovery-in-azure-ad---public-preview"></a>Azure AD에서 감사 되는 BitLocker 복구-공개 미리 보기

**유형:** 새로운 기능  
**서비스 범주:** 장치 액세스 관리  
**제품 기능:** 장치 수명 주기 관리
 
IT 관리자 또는 최종 사용자가 액세스할 수 있는 BitLocker 복구 키를 읽으면 Azure Active Directory은 이제 복구 키에 액세스 한 사용자를 캡처하는 감사 로그를 생성 합니다. 동일한 감사는 BitLocker 키가 연결 된 장치에 대 한 세부 정보를 제공 합니다.

최종 사용자는 [내 계정을 통해 복구 키에 액세스할](../user-help/my-account-portal-devices-page.md#view-a-bitlocker-key)수 있습니다. IT 관리자는 [베타의 BitLocker 복구 키 API](/graph/api/resources/bitlockerrecoverykey?view=graph-rest-beta) 또는 Azure AD 포털을 통해 복구 키에 액세스할 수 있습니다. 자세히 알아보려면 [AZURE AD 포털에서 BitLocker 키 보기 또는 복사](../devices/device-management-azure-portal.md#view-or-copy-bitlocker-keys)를 참조 하세요.

---

### <a name="teams-devices-administrator-built-in-role"></a>팀 장치 관리자 기본 제공 역할

**유형:** 새로운 기능  
**서비스 범주:** RBAC  
**제품 기능:** 액세스 제어
 
[팀 장치 관리자](../roles/permissions-reference.md#teams-devices-administrator) 역할을 가진 사용자는 팀 관리 센터에서 [팀 인증 장치](https://www.microsoft.com/microsoft-365/microsoft-teams/across-devices/devices) 를 관리할 수 있습니다. 

이 역할을 통해 사용자는 장치를 검색 하 고 필터링 할 수 있는 기능을 사용 하 여 모든 장치를 한 눈에 볼 수 있습니다. 또한 사용자는 로그인 한 계정 및 장치의 제조업체 및 모델을 포함 하 여 각 장치에 대 한 세부 정보를 확인할 수 있습니다. 사용자는 장치에서 설정을 변경 하 고 소프트웨어 버전을 업데이트할 수 있습니다. 이 역할은 팀 활동을 확인 하 고 장치의 품질을 호출할 수 있는 권한을 부여 하지 않습니다.
 
---

### <a name="advanced-query-capabilities-for-directory-objects"></a>디렉터리 개체에 대 한 고급 쿼리 기능

**유형:** 새로운 기능  
**서비스 범주:** MS 그래프  
**제품 기능:** 개발자 환경
 
이제 Azure AD Api의 디렉터리 개체에 대해 도입 된 모든 새 쿼리 기능을 v 1.0 끝점에서 사용할 수 있으며 프로덕션이 준비 됩니다. 개발자는 표준 OData 연산자를 사용 하 여 디렉터리 개체 및 관련 링크를 계산, 검색, 필터링 및 정렬할 수 있습니다.

자세한 내용은 [여기](https://aka.ms/BlogPostMezzoGA)에서 설명서를 참조 하 고,이 [간단한 설문 조사](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_yN8EPoGo5OpR1hgmCp1XxUMENJRkNQTk5RQkpWTE44NEk2U0RIV0VZRy4u)를 통해 사용자 의견을 보낼 수도 있습니다.
 
---

### <a name="public-preview-continuous-access-evaluation-for-tenants-who-configured-conditional-access-policies"></a>공개 미리 보기: 조건부 액세스 정책을 구성 하는 테 넌 트에 대 한 지속적인 액세스 평가

**유형:** 새로운 기능  
**서비스 범주:** 인증 (로그인)  
**제품 기능:** Id 보안 & 보호
 
이제 조건부 액세스 정책을 사용 하 여 Azure AD 테 넌 트에 대 한 공개 미리 보기에서 CAE (연속 액세스 평가)를 사용할 수 있습니다. CAE를 사용 하면 중요 한 보안 이벤트와 정책이 실시간으로 평가 됩니다. 계정 사용 안 함, 암호 재설정 및 위치 변경도 포함 됩니다. 자세히 알아보려면 [연속 액세스 평가](../conditional-access/concept-continuous-access-evaluation.md)를 참조 하세요.

---

### <a name="public-preview-ask-users-requesting-an-access-package-additional-questions-to-improve-approval-decisions"></a>공개 미리 보기: 액세스 패키지를 요청 하는 사용자에 게 승인 결정을 개선 하기 위한 추가 질문

**유형:** 새로운 기능  
**서비스 범주:** 사용자 액세스 관리  
**제품 기능:** 자격 관리
 
이제 관리자는 액세스 패키지를 요청 하는 사용자가 Azure AD 자격 관리의 내 액세스 포털에서 비즈니스 근거를 벗어나 추가 질문에 대답할 수 있도록 요구할 수 있습니다. 그러면 사용자의 답변이 승인자에 게 표시 되어 더 정확한 액세스 승인 결정을 내리는 데 도움이 됩니다. 자세히 알아보려면 [승인을 위한 추가 요청자 정보 수집 (미리 보기)](../governance/entitlement-management-access-package-approval-policy.md#collect-additional-requestor-information-for-approval-preview)을 참조 하세요.
 
---

### <a name="public-preview-enhanced-user-management"></a>공개 미리 보기: 향상 된 사용자 관리

**유형:** 새로운 기능  
**서비스 범주:** 사용자 관리  
**제품 기능:** 사용자 관리
 

Azure AD 포털은 모든 사용자 및 삭제 된 사용자 페이지에서 사용자를 쉽게 찾을 수 있도록 업데이트 되었습니다. 미리 보기의 변경 내용은 다음과 같습니다. 
- 개체 ID, 디렉터리 동기화 상태, 생성 유형 및 id 발급자를 비롯 한 더 보이는 사용자 속성
- 이제 검색에서 이름, 전자 메일 및 개체 Id의 결합 된 검색을 허용 합니다.
- 사용자 유형별 고급 필터링 (구성원, 게스트 및 없음), 디렉터리 동기화 상태, 생성 유형, 회사 이름 및 도메인 이름입니다.
- 이름, 사용자 계정 이름 및 삭제 날짜와 같은 속성에 대 한 새로운 정렬 기능.
- 검색 또는 필터를 사용 하 여 업데이트 되는 새 총 사용자 수입니다.

자세한 내용은 [Azure Active Directory의 사용자 관리 향상 기능 (미리 보기)](../enterprise-users/users-search-enhanced.md)을 참조 하세요.

---

### <a name="new-notes-field-for-enterprise-applications"></a>엔터프라이즈 응용 프로그램에 대 한 새 메모 필드

**유형:** 새로운 기능  
**서비스 범주:** Enterprise Apps **제품 기능:** SSO

엔터프라이즈 응용 프로그램에 자유 텍스트 메모를 추가할 수 있습니다. 엔터프라이즈 응용 프로그램에서 응용 프로그램을 관리 하는 데 도움이 되는 관련 정보를 추가할 수 있습니다. 자세한 내용은 [빠른 시작: Azure Active Directory (AZURE AD) 테 넌 트의 응용 프로그램에 대 한 속성 구성](../manage-apps/add-application-portal-configure.md)을 참조 하세요. 

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---september-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-9 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합

2020 년 9 월에 앱 갤러리에 페더레이션 지원과 함께 다음 34 새 응용 프로그램을 추가 했습니다.

[VMware 수평 통합 액세스 게이트웨이](), [펄스 보안 pc](../saas-apps/vmware-horizon-unified-access-gateway-tutorial.md), [Inventory360](../saas-apps/pulse-secure-pcs-tutorial.md), [Frontitude](https://services.enteksystems.de/sso/microsoft/signup), [bookwidgets](https://www.bookwidgets.com/sso/office365), [ZVD_Server](https://zaas.zenmutech.com/user/signin), [비즈니스에 대 한 HASHDATA](https://hashdata.app/login.xhtml), [Securelogin](https://securelogin.securelogin.nu/sso/azure/login), [CyberSolutions MAILBASEΣ/Cmss](../saas-apps/cybersolutions-mailbase-tutorial.md), [CyberSolutions CYBERMAILΣ](../saas-apps/cybersolutions-cybermail-tutorial.md), [LimbleCMMS](https://auth.limblecmms.com/), [Glint inc.](../saas-apps/glint-inc-tutorial.md), [zeroheight](../saas-apps/zeroheight-tutorial.md), [성별 적합성](https://app.genderfitness.com/), [Coeo 포털](https://my.coeo.com/), Grammarly [,](../saas-apps/fivetran-tutorial.md) [Fivetran,](../saas-apps/grammarly-tutorial.md) [Kumolus](../saas-apps/kumolus-tutorial.md), [RSA 궁 궁 Suite](../saas-apps/rsa-archer-suite-tutorial.md), [teamzskill](../saas-apps/teamzskill-tutorial.md), [raumfürraum](../saas-apps/raumfurraum-tutorial.md), [Saviynt](../saas-apps/saviynt-tutorial.md), [BizMerlinHR](https://marketplace.bizmerlin.net/bmone/signup), [Mobile 락커](../saas-apps/mobile-locker-tutorial.md), [Zengine](../saas-apps/zengine-tutorial.md), [cloudcadi](https://app.cloudcadi.com/login) [, PeopleSoft](https://simfonianalytics.com/accounts/microsoft/login/),, [개인 Identity & Access Management](https://my.priva.com/), [nitro Pro](https://www.gonitro.com/nps/product-details/downloads), [eventfinity](../saas-apps/eventfinity-tutorial.md), [fexa](../saas-apps/fexa-tutorial.md), 보안 [서명 Enterprise Portal](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [보안 서명 Enterprise Portal AAD 설정](https://www.securedsigning.com/aad/Auth/ExternalLogin/AdminPortal), [wistec Online](https://wisteconline.com/auth/oidc), [Oracle-F5 키로 보호](../saas-apps/oracle-peoplesoft-protected-by-f5-big-ip-apm-tutorial.md)

에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다 https://aka.ms/AppsTutorial .

Azure AD 앱 갤러리에서 응용 프로그램을 나열 하려면 여기에서 세부 정보를 참조 https://aka.ms/AzureADAppRequest 하세요.

---

### <a name="new-delegation-role-in-azure-ad-entitlement-management-access-package-assignment-manager"></a>Azure AD 자격 관리의 새 위임 역할: 액세스 패키지 할당 관리자

**유형:** 새로운 기능  
**서비스 범주:** 사용자 액세스 관리  
**제품 기능:** 자격 관리
 
Azure AD 자격 관리에 새 액세스 패키지 할당 관리자 역할이 추가 되어 할당을 관리할 수 있는 세부적인 권한을 제공 합니다. 이제 비즈니스 소유자에 게 액세스 패키지의 할당 관리를 위임할 수 있는 사용자에 게 작업을 위임할 수 있습니다. 그러나 액세스 패키지 할당 관리자는 관리자가 설정한 액세스 패키지 정책 또는 기타 속성을 변경할 수 없습니다. 

이 새로운 역할을 사용 하면 할당 관리를 위임 하 고 다른 모든 액세스 패키지 구성에 대 한 관리 제어를 유지 하는 데 필요한 최소한의 권한을 활용할 수 있습니다. 자세히 알아보려면 [권한 관리 역할](../governance/entitlement-management-delegate.md#entitlement-management-roles)을 참조 하세요.
 
---

### <a name="changes-to-privileged-identity-managements-onboarding-flow"></a>Privileged Identity Management의 온 보 딩 흐름에 대 한 변경 내용

**유형:** 변경된 기능  
**서비스 범주:** Privileged Identity Management  
**제품 기능:** Privileged Identity Management
 
이전에는 PIM (Privileged Identity Management)에 등록 하는 데 Azure AD MFA에 등록을 포함 하는 PIM의 블레이드에서 사용자 동의 및 온 보 딩 흐름이 필요 합니다. Azure AD 역할 및 관리자 블레이드에 최신 PIM 환경을 통합 하 여이 환경을 제거 하 고 있습니다. 유효한 P2 라이선스가 있는 테 넌 트는 PIM으로 자동 등록 됩니다.

PIM에 등록 하면 테 넌 트에 직접적인 부정적인 영향을 주지 않습니다. 다음과 같이 변경할 수 있습니다.
- PIM 또는 Azure AD 역할 및 관리자 블레이드에서 할당을 수행 하는 경우 활성 및 시작 및 종료 시간과 관련 된 추가 할당 옵션 
- 할당 환경에 직접 도입 된 관리 단위 및 사용자 지정 역할과 같은 추가 범위 지정 메커니즘입니다. 
- 전역 관리자 또는 권한 있는 역할 관리자 인 경우 PIM 주간 다이제스트와 같은 몇 가지 추가 전자 메일을 받을 수 있습니다. 
- 역할 할당과 관련 된 감사 로그에 ms-pim 서비스 사용자가 표시 될 수도 있습니다. 이 예상 변경 내용은 일반 워크플로에 영향을 주지 않습니다.

 자세한 내용은 [Privileged Identity Management 사용 시작](../privileged-identity-management/pim-getting-started.md)을 참조 하세요.

---

### <a name="azure-ad-entitlement-management-the-select-pane-of-access-package-resources-now-shows-by-default-the-resources-currently-in-the-selected-catalog"></a>Azure AD 자격 관리: 이제 액세스 패키지 리소스의 선택 창에는 현재 선택한 카탈로그에 있는 리소스가 기본적으로 표시 됩니다.

**유형:** 변경된 기능  
**서비스 범주:** 사용자 액세스 관리  
**제품 기능:** 자격 관리
 

액세스 패키지 생성 흐름의 리소스 역할 탭에서 창 선택 동작이 변경 됩니다. 현재 기본 동작은 사용자가 소유 하는 모든 리소스와 선택한 카탈로그에 추가 된 리소스를 표시 하는 것입니다. 

이 환경은 사용자가 카탈로그에서 리소스를 쉽게 선택할 수 있도록 기본적으로 카탈로그에 현재 추가 된 리소스만 표시 하도록 변경 됩니다. 업데이트는 액세스 패키지에 추가할 리소스를 검색 하는 데 도움이 되며 카탈로그의 일부가 아닌 사용자가 소유한 리소스를 실수로 추가 하는 위험을 줄일 수 있습니다. 자세히 알아보려면 [AZURE AD 자격 관리에서 새 액세스 패키지 만들기](../governance/entitlement-management-access-package-create.md#resource-roles)를 참조 하세요.
 
---

## <a name="august-2020"></a>2020년 8월 
 
### <a name="updates-to-azure-multi-factor-authentication-server-firewall-requirements"></a>Azure Multi-Factor Authentication 서버 방화벽 요구 사항에 대 한 업데이트

**유형:** 변경 계획  
**서비스 범주:** MFA  
**제품 기능:** Id 보안 & 보호
 
2020 년 10 월 1 일부 터 Azure MFA 서버 방화벽 요구 사항에는 추가 IP 범위가 필요 합니다.

조직에서 아웃 바운드 방화벽 규칙을 사용 하는 경우 MFA 서버가 필요한 모든 IP 범위와 통신할 수 있도록 규칙을 업데이트 합니다. IP 범위는 [Azure Multi-Factor Authentication 서버 방화벽 요구 사항](../authentication/howto-mfaserver-deploy.md#azure-multi-factor-authentication-server-firewall-requirements)에 설명 되어 있습니다.

---

### <a name="upcoming-changes-to-user-experience-in-identity-secure-score"></a>Id 보안 점수의 사용자 환경에 대 한 예정 된 변경 내용

**유형:** 변경 계획  
**서비스 범주:** Id 보호 **제품 기능:** id 보안 & 보호

Microsoft 보안 점수의 [새로운 릴리스에](/microsoft-365/security/mtp/microsoft-secure-score-whats-new)도입 된 변경 내용에 맞게 Id 보안 점수 포털을 업데이트 하 고 있습니다. 

변경 내용이 포함 된 미리 보기 버전은 9 월부터 사용할 수 있습니다. 미리 보기 버전의 변경 내용은 다음과 같습니다.
- Microsoft 보안 점수를 사용 하 여 브랜드 맞춤을 위해 "id 보안 점수"의 이름을 "Id 보안 점수"로 바꿨습니다.
- 표준 배율으로 정규화 되 고 점이 아닌 백분율로 보고 되는 점수

이 미리 보기에서는 고객이 기존 환경과 새 환경을 전환할 수 있습니다. 이 미리 보기는 11 월 2020이 끝날 때까지 지속 됩니다. 미리 보기 후에는 고객이 자동으로 새로운 UX 환경으로 이동 됩니다.

---

### <a name="new-restricted-guest-access-permissions-in-azure-ad---public-preview"></a>Azure AD에서 제한 된 새 게스트 액세스 권한-공개 미리 보기

**유형:** 새로운 기능  
**서비스 범주:** Access Control   
**제품 기능:** 사용자 관리

게스트 사용자에 대 한 디렉터리 수준 권한을 업데이트 했습니다. 이러한 사용 권한을 통해 관리자는 외부 게스트 사용자 액세스에 대 한 추가 제한 사항 및 제어를 요구할 수 있습니다. 이제 관리자는 외부 게스트의 사용자 및 그룹의 프로필 및 멤버 자격 정보에 대 한 추가 제한을 추가할 수 있습니다. 이 공개 미리 보기 기능을 사용 하면 고객은 게스트 사용자가 자신이 속한 그룹의 멤버 자격을 볼 수 없도록 제한 하는 것을 포함 하 여 난독 처리 그룹 멤버 자격을 통해 규모에 따라 외부 사용자 액세스를 관리할 수 있습니다.

자세히 알아보려면 [제한 된 게스트 액세스 권한](../enterprise-users/users-restrict-guest-permissions.md) 및 [사용자 기본 권한](./users-default-permissions.md)을 참조 하세요.
 
---

### <a name="general-availability-of-delta-queries-for-service-principals"></a>서비스 사용자에 대 한 델타 쿼리의 일반 가용성

**유형:** 새로운 기능  
**서비스 범주:** MS 그래프  
**제품 기능:** 개발자 환경
 
이제 Microsoft Graph 델타 쿼리가 v 1.0의 리소스 형식을 지원 합니다.
- 서비스 주체

이제 클라이언트는 해당 리소스에 대 한 변경 내용을 효율적으로 추적할 수 있으며, 해당 리소스에 대 한 변경 내용을 로컬 데이터 저장소와 동기화 하는 최상의 솔루션을 제공 합니다. 쿼리에서 이러한 리소스를 구성 하는 방법을 알아보려면 [델타 쿼리를 사용 하 여 Microsoft Graph 데이터의 변경 내용 추적](/graph/delta-query-overview)을 참조 하세요.
 
---

### <a name="general-availability-of-delta-queries-for-oauth2permissiongrant"></a>OAuth2PermissionGrant에 대 한 델타 쿼리의 일반 가용성

**유형:** 새로운 기능  
**서비스 범주:** MS 그래프  
**제품 기능:** 개발자 환경

이제 Microsoft Graph 델타 쿼리가 v 1.0의 리소스 형식을 지원 합니다.
- OAuth2PermissionGrant

클라이언트는 이제 해당 리소스에 대 한 변경 내용을 효율적으로 추적할 수 있으며, 로컬 데이터 저장소와 이러한 리소스의 변경 내용을 동기화 하는 최상의 솔루션을 제공 합니다. 쿼리에서 이러한 리소스를 구성 하는 방법을 알아보려면 [델타 쿼리를 사용 하 여 Microsoft Graph 데이터의 변경 내용 추적](/graph/delta-query-overview)을 참조 하세요.

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---august-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-8 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합

8 월 2020에 앱 갤러리에 페더레이션 지원이 포함 된 다음과 같은 25 개의 새로운 응용 프로그램이 추가 되었습니다.

[Backup365](https://portal.backup365.io/login), [soapbox](https://app.soapboxhq.com/create?step=auth&provider=azure-ad2-oauth2), [alma SIS](https://almau.getalma.com/), [enlyft Dynamics 365 커넥터](http://enlyft.com/), [serraview 공간 사용률 소프트웨어 솔루션](../saas-apps/serraview-space-utilization-software-solutions-tutorial.md), [전체 q](https://web.uniq.app/), [가시적](../saas-apps/visibly-tutorial.md), [zylo](../saas-apps/zylo-tutorial.md), [Edmentum-교육용 평가 정확한 경로](https://auth.edmentum.com/elf/login), [CyberLAB](https://cyberlab.evolvesecurity.com/#/welcome), [Altamira hrm](../saas-apps/altamira-hrm-tutorial.md), [WireWheel](../saas-apps/wirewheel-tutorial.md), [Zix 준수 및 캡처](https://sminstall.zixcorp.com/teams/teams.php?install_request=true&tenant_id=common), [Greenlight Enterprise Business Controls Platform](../saas-apps/greenlight-enterprise-business-controls-platform-tutorial.md), [genetec 클리어런스](https://www.clearance.network/), [ISAMS](../saas-apps/isams-tutorial.md), [Verasmart](../saas-apps/verasmart-tutorial.md), [amiko](https://amiko.web.rivero.app/), [twingate](https://auth.twingate.com/signup), [깔때기형 임대](https://nestiolistings.com/sso/oidc/azure/authorize/), [Scalefusion](https://scalefusion.com/users/sign_in/), [Bpanda](https://goto.bpanda.com/login), [vivun 일정 연결](https://app.vivun.com/dashboard/calendar/connect), [fortigate SSL VPN](../saas-apps/fortigate-ssl-vpn-tutorial.md), [Wandera 최종 사용자](https://www.wandera.com/)

여기에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다. https://aka.ms/AppsTutorial

Azure AD 앱 갤러리에서 응용 프로그램을 나열 하려면 여기에서 세부 정보를 읽으십시오. https://aka.ms/AzureADAppRequest

---

### <a name="resource-forests-now-available-for-azure-ad-ds"></a>이제 Azure AD DS에 리소스 포리스트 사용 가능 

**유형:** 새 기능 **서비스 범주:** Azure AD Domain Services   
**제품 기능:** Azure AD Domain Services
 
Azure AD Domain Services에서 리소스 포리스트의 기능이 이제 일반 공급 됩니다. 이제 스마트 카드 권한 부여를 비롯 하 여 Azure AD Domain Services를 사용 하기 위해 암호 해시 동기화 없이 권한 부여를 사용 하도록 설정할 수 있습니다. 자세한 내용은 [Azure Active Directory Domain Services에 대 한 복제본 집합 개념 및 기능 (미리 보기)](../../active-directory-domain-services/concepts-replica-sets.md)을 참조 하세요.
 
---

### <a name="regional-replica-support-for-azure-ad-ds-managed-domains-now-available"></a>이제 Azure AD DS 관리 되는 도메인에 대 한 지역 복제본 지원이 제공 됩니다.

**유형:** 새로운 기능   
**서비스 범주:** Azure AD Domain Services  
**제품 기능:** Azure AD Domain Services
 
관리되는 도메인을 확장하여 Azure AD 테넌트마다 복제본 세트를 2개 이상 포함할 수 있습니다. Azure AD Domain Services를 지 원하는 모든 Azure 지역의 피어 링 가상 네트워크에 복제본 집합을 추가할 수 있습니다. 다른 Azure 지역에 있는 추가 복제본 세트는 Azure 지역이 오프라인 상태가 될 때 레거시 애플리케이션에 대한 지리적 재해 복구를 제공합니다. 자세한 내용은 [Azure Active Directory Domain Services에 대 한 복제본 집합 개념 및 기능 (미리 보기)](../../active-directory-domain-services/concepts-replica-sets.md)을 참조 하세요.

---

### <a name="general-availability-of-azure-ad-my-sign-ins"></a>Azure AD 내 Sign-Ins의 일반 공급

**유형:** 새로운 기능  
**서비스 범주:** 인증 (로그인)  
**제품 기능:** 최종 사용자 환경
 
Azure AD 내 Sign-Ins는 엔터프라이즈 사용자가 로그인 기록을 검토 하 여 비정상적인 활동을 확인할 수 있도록 하는 새로운 기능입니다. 또한이 기능을 사용 하면 최종 사용자가 의심 스러운 활동에 대해 "This me" 또는 "This was"를 보고할 수 있습니다. 이 기능을 사용 하는 방법에 대해 자세히 알아보려면 [내 Sign-Ins 페이지에서 최근 로그인 활동 보기 및 검색](../user-help/my-account-portal-sign-ins-page.md#confirm-unusual-activity)을 참조 하세요.
 
---

### <a name="sap-successfactors-hr-driven-user-provisioning-to-azure-ad-is-now-generally-available"></a>Azure AD에 대 한 SAP SuccessFactors HR 기반 사용자 프로비저닝이 이제 일반 공급 됩니다.

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** Id 수명 주기 관리
 
이제 Azure AD를 사용 하 여 SAP SuccessFactors를 신뢰할 수 있는 id 원본으로 통합 하 고 새 채용 및 종료와 같은 HR 이벤트를 사용 하 여 종단 간 id 수명 주기를 자동화 하 여 Azure AD에서 계정 프로 비전 및 프로 비전 해제를 수행할 수 있습니다. 

Azure AD에 대 한 SAP SuccessFactors 인바운드 프로 비전을 구성 하는 방법에 대 한 자세한 내용은 [사용자 프로 비전을 ACTIVE DIRECTORY Sap SuccessFactors 구성](../saas-apps/sap-successfactors-inbound-provisioning-tutorial.md)자습서를 참조 하세요.
 
---

### <a name="custom-open-id-connect-ms-graph-api-support-for-azure-ad-b2c"></a>Azure AD B2C에 대 한 사용자 지정 Open ID Connect MS Graph API 지원

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
이전에는 사용자 지정 Open ID Connect 공급자를 Azure Portal 통해서만 추가 하거나 관리할 수 있었습니다. 이제 Azure AD B2C 고객이 Microsoft Graph Api 베타 버전을 통해 추가 하 고 관리할 수 있습니다. Api를 사용 하 여이 리소스를 구성 하는 방법을 알아보려면 [identityProvider 리소스 형식](/graph/api/resources/identityprovider?view=graph-rest-beta)을 참조 하세요.
 
---

### <a name="assign-azure-ad-built-in-roles-to-cloud-groups"></a>클라우드 그룹에 Azure AD 기본 제공 역할 할당

**유형:** 새로운 기능  
**서비스 범주:** Azure AD 역할  
**제품 기능:** 액세스 제어

이제이 새로운 기능을 사용 하 여 Azure AD 기본 제공 역할을 클라우드 그룹에 할당할 수 있습니다. 예를 들어 SharePoint 관리자 역할을 Contoso_SharePoint_Admins 그룹에 할당할 수 있습니다. 또한 PIM을 사용 하 여 그룹을 적절 한 액세스 권한을 부여 하는 대신 역할의 적격 멤버로 만들 수 있습니다. 이 기능을 구성 하는 방법을 알아보려면 [클라우드 그룹을 사용 하 여 Azure Active Directory에서 역할 할당 관리 (미리 보기)](../roles/groups-concept.md)를 참조 하세요.
 
---

### <a name="insights-business-leader-built-in-role-now-available"></a>Insights 비즈니스 리더 기본 제공 역할을 이제 사용할 수 있음

**유형:** 새로운 기능  
**서비스 범주:** Azure AD 역할  
**제품 기능:** 액세스 제어
 
Insights 비즈니스 리더 역할의 사용자는 [M365 insights 응용 프로그램](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics)을 통해 대시보드 및 통찰력 집합에 액세스할 수 있습니다. 여기에는 모든 대시보드에 대 한 모든 액세스 권한 및 제공 되는 정보 및 데이터 탐색 기능이 포함 됩니다. 그러나이 역할의 사용자는 정보 관리자 역할을 담당 하는 제품 구성 설정에 액세스할 수 없습니다. 이 역할에 대 한 자세한 내용은 [Azure Active Directory의 관리자 역할 권한](../roles/permissions-reference.md#insights-business-leader) 을 참조 하세요.
 
---

### <a name="insights-administrator-built-in-role-now-available"></a>이제 Insights 관리자 기본 제공 역할을 사용할 수 있음

**유형:** 새로운 기능  
**서비스 범주:** Azure AD 역할  
**제품 기능:** 액세스 제어
 
Insights 관리자 역할의 사용자는 [M365 Insights 응용 프로그램](https://www.microsoft.com/microsoft-365/partners/workplaceanalytics)의 전체 관리 기능 집합에 액세스할 수 있습니다. 이 역할의 사용자는 디렉터리 정보를 읽고, 서비스 상태를 모니터링 하 고, 파일 지원 티켓을 확인 하 고, 정보 관리자 설정 측면에 액세스할 수 있습니다. 이 역할에 대 한 자세한 내용은 [Azure Active Directory의 관리자 역할 권한](../roles/permissions-reference.md#insights-administrator) 을 참조 하세요.
 
--- 

### <a name="application-admin-and-cloud-application-admin-can-manage-extension-properties-of-applications"></a>응용 프로그램 관리자 및 클라우드 응용 프로그램 관리자는 응용 프로그램의 확장 속성을 관리할 수 있습니다.

**유형:** 변경된 기능  
**서비스 범주:** Azure AD 역할  
**제품 기능:** 액세스 제어
 
이전에는 전역 관리자만 [확장 속성](/graph/api/application-post-extensionproperty?view=graph-rest-beta&tabs=http)을 관리할 수 있었습니다. 이제 응용 프로그램 관리자 및 클라우드 응용 프로그램 관리자에 게이 기능을 사용 하도록 설정 하는 중입니다.
 
---

### <a name="mim-2016-sp2-hotfix-462630-and-connectors-1113010"></a>MIM 2016 SP2 핫픽스 4.6.263.0 및 커넥터 1.1.1301.0

**유형:** 변경된 기능  
**서비스 범주:** Microsoft Identity Manager  
**제품 기능:** Id 수명 주기 관리

[핫픽스 롤업 패키지 (build 4.6.263.0)](https://support.microsoft.com/help/4576473/hotfix-rollup-package-build-4-6-263-0-is-available-for-microsoft-ident) 는 MICROSOFT IDENTITY MANAGER (MIM) 2016 서비스 팩 2 (SP2)에서 사용할 수 있습니다. 이 롤업 패키지에는 MIM CM, MIM 동기화 관리자 및 PAM 구성 요소에 대 한 업데이트가 포함 되어 있습니다. 또한 MIM 일반 커넥터 1.1.1301.0 빌드에는 Graph 커넥터에 대 한 업데이트가 포함 되어 있습니다.

---
 
## <a name="july-2020"></a>2020년 7월

### <a name="as-an-it-admin-i-want-to-target-client-apps-using-conditional-access"></a>IT 관리자는 조건부 액세스를 사용 하 여 클라이언트 앱을 대상으로 합니다.

**유형:** 변경 계획   
**서비스 범주:** 조건부 액세스  
**제품 기능:** Id 보안 & 보호
 
조건부 액세스에서 클라이언트 앱 조건의 GA 릴리스를 사용 하면 이제 모든 클라이언트 응용 프로그램에 새 정책이 기본적으로 적용 됩니다. 여기에는 레거시 인증 클라이언트가 포함 됩니다. 기존 정책은 변경 되지 않고 그대로 유지 되지만, 정책에 따라 적용 되는 클라이언트 앱을 쉽게 확인 하기 위해 기존 정책에서 *예/아니요 구성* 토글이 제거 됩니다. 

새 정책을 만들 때 여전히 레거시 인증을 사용 하는 사용자 및 서비스 계정을 제외 해야 합니다. 그렇지 않으면 차단 됩니다. [자세히 알아보기](../conditional-access/concept-conditional-access-conditions.md).
 
---

### <a name="upcoming-scim-compliance-fixes"></a>예정 된 SCIM 준수 픽스

**유형:** 변경 계획  
**서비스 범주:** 앱 프로비전  
**제품 기능:** Id 수명 주기 관리
 
Azure AD 프로 비전 서비스는 응용 프로그램과 통합 하기 위해 SCIM 표준을 활용 합니다. SCIM 표준의 구현은 진화 하 고 있으며, 패치 작업을 수행 하는 방법에 대 한 동작을 변경 하 고 리소스에 "active" 속성을 설정 하는 것이 좋습니다. [자세히 알아보기](../app-provisioning/application-provisioning-config-problem-scim-compatibility.md).
 
---

### <a name="group-owner-setting-on-azure-admin-portal-will-be-changed"></a>Azure 관리 포털의 그룹 소유자 설정이 변경 됨

**유형:** 변경 계획  
**서비스 범주:** 그룹 관리  
**제품 기능:** 협업

그룹에 대 한 소유자 설정 일반 설정 페이지는 Azure 관리 포털 및 액세스 패널에서 소유자 할당 권한을 제한 된 사용자 그룹으로 제한 하도록 구성할 수 있습니다. 이러한 두 UX 포털 뿐만 아니라 그룹 소유자 권한을 할당 하는 기능이 곧 제공 될 예정 이며, PowerShell 및 Microsoft Graph 같은 끝점에서 일관 된 동작을 제공 하기 위해 백 엔드에서 정책을 적용할 수 있습니다. 

Microsoft는이를 사용 하지 않는 고객에 대 한 현재 설정을 사용 하지 않도록 설정 하 고, 향후 몇 개월 동안 그룹 소유자 권한으로 사용자의 범위를 설정 하는 옵션을 제공 합니다. 그룹 설정 업데이트에 대 한 지침은 [Azure Active Directory](./active-directory-groups-settings-azure-portal.md?context=azure%2factive-directory%2fusers-groups-roles%2fcontext%2fugr-context)를 사용 하 여 그룹 정보 편집을 참조 하세요.

---

### <a name="azure-active-directory-registration-service-is-ending-support-for-tls-10-and-11"></a>Azure Active Directory 등록 서비스가 TLS 1.0 및 1.1에 대 한 지원을 종료 합니다.

**유형:** 변경 계획  
**서비스 범주:** 장치 등록 및 관리  
**제품 기능:** 플랫폼

TLS (전송 계층 보안) 1.2 및 업데이트 서버와 클라이언트는 Azure Active Directory Device Registration 서비스와 곧 통신할 수 있습니다. Azure AD Device Registration service와 통신 하는 TLS 1.0 및 1.1에 대 한 지원은 사용 중지 됩니다.
- 모든 소 버린 클라우드의 2020 년 8 월 31 일 (GCC High, DoD 등)
- 모든 상용 클라우드의 2020 년 10 월 30 일

Azure AD 등록 서비스에 대 한 TLS 1.2에 대해 [자세히 알아보세요](../devices/reference-device-registration-tls-1-2.md) .

---

### <a name="windows-hello-for-business-sign-ins-visible-in-azure-ad-sign-in-logs"></a>Azure AD 로그인 로그에 표시 되는 비즈니스용 Windows Hello 로그인

**유형:** 고정  
**서비스 범주:** 보고  
**제품 기능:** 모니터링 및 보고
 
비즈니스용 windows Hello를 사용 하면 최종 사용자가 제스처 (예: PIN 또는 생체 인식)를 사용 하 여 Windows 컴퓨터에 로그인 할 수 있습니다. Azure AD 관리자는 조직의 경험을 통해 다른 Windows 로그인의 비즈니스용 Windows Hello 로그인을 암호 없는 인증으로 구분할 수 있습니다. 

이제 관리자는 Azure Portal의 Azure AD Sign-Ins 블레이드에서 Windows 로그인 이벤트에 대 한 인증 세부 정보 탭을 확인 하 여 Windows 인증에서 비즈니스용 Windows Hello를 사용 했는지 여부를 확인할 수 있습니다. 비즈니스용 Windows Hello 인증에는 인증 방법 필드에 "WindowsHelloForBusiness"가 포함 됩니다. Sign-In 로그를 해석 하는 방법에 대 한 자세한 내용은 [로그인 로그 설명서](../reports-monitoring/concept-sign-ins.md)를 참조 하세요.
 
---

### <a name="fixes-to-group-deletion-behavior-and-performance-improvements"></a>그룹 삭제 동작 및 성능 향상에 대 한 수정

**유형:** 고정  
**서비스 범주:** 앱 프로비전  
**제품 기능:** Id 수명 주기 관리
 
이전에는 그룹이 "범위 내"에서 "범위를 벗어났습니다."로 변경 되 고 관리자가 변경을 완료 하기 전에 다시 시작을 클릭 했을 때 그룹 개체를 삭제 하지 않았습니다. 이제 범위를 벗어나면 (사용 안 함, 삭제 됨, 할당 되지 않음 또는 범위 지정 필터를 전달 하지 않음) 그룹 개체가 대상 응용 프로그램에서 삭제 됩니다. [자세히 알아보기](../app-provisioning/how-provisioning-works.md#incremental-cycles).
 
---

### <a name="public-preview-admins-can-now-add-custom-content-in-the-email-to-reviewers-when-creating-an-access-review"></a>공개 미리 보기: 이제 관리자가 액세스 검토를 만들 때 검토자에 게 전자 메일의 사용자 지정 콘텐츠를 추가할 수 있습니다.

**유형:** 새로운 기능  
**서비스 범주:** 액세스 검토  
**제품 기능:** Id 거 버 넌 스
 
새 액세스 검토가 만들어지면 검토자는 액세스 검토를 완료 하도록 요청 하는 전자 메일을 받습니다. 대부분의 고객은 전자 메일에 사용자 지정 콘텐츠를 추가 하는 기능 (예: 연락처 정보 또는 기타 추가 지원 콘텐츠)을 요청 하 여 검토자를 안내 합니다. 

이제 공개 미리 보기로 제공 되는 관리자는 Azure AD 액세스 검토의 "고급" 섹션에서 콘텐츠를 추가 하 여 검토자에 게 보내는 전자 메일의 사용자 지정 콘텐츠를 지정할 수 있습니다. 액세스 검토를 만드는 방법에 대 한 지침은 [AZURE AD 액세스 검토에서 그룹 및 응용 프로그램에 대 한 액세스 검토 만들기](../governance/create-access-review.md)를 참조 하세요.
 
---

### <a name="authorization-code-flow-for-single-page-apps-available"></a>단일 페이지 앱에 대 한 인증 코드 흐름 사용 가능

**유형:** 새로운 기능  
**서비스 범주:** 인증 (로그인)  
**제품 기능:** 개발자 환경
 
최신 브라우저에서 Safari ITP와 같은 타사 쿠키 제한 사항 때문에, SPAs는 SSO를 유지 관리 하기 위해 암시적 흐름이 아닌 권한 부여 코드 흐름을 사용 해야 하 고 MSAL.js v 2. x는 이제 인증 코드 흐름을 지원 합니다. 

Azure Portal에 대 한 해당 업데이트가 있으므로 SPA를 "spa" 형식으로 업데이트 하 고 인증 코드 흐름을 사용할 수 있습니다. 추가 지침은 [인증 코드 흐름을 사용 하 여 사용자 로그인 및 JAVASCRIPT SPA에서 액세스 토큰 가져오기](../develop/quickstart-v2-javascript-auth-code.md) 를 참조 하세요.
 
---

### <a name="azure-ad-application-proxy-now-supports-the-remote-desktop-services-web-client"></a>이제 Azure AD 응용 프로그램 프록시 원격 데스크톱 서비스 웹 클라이언트를 지원 합니다.

**유형:** 새로운 기능  
**서비스 범주:** 응용 프로그램 프록시  
**제품 기능:** 액세스 제어

이제 Azure AD 응용 프로그램 프록시는 RDS (원격 데스크톱 서비스) 웹 클라이언트를 지원 합니다. 사용자는 RDS 웹 클라이언트를 사용 하 여 Microsoft Edge, Internet Explorer 11, Google Chrome 등의 HTLM5 지원 브라우저를 통해 원격 데스크톱 인프라에 액세스할 수 있습니다. 사용자는 어디서 나 로컬 장치를 사용 하는 것 처럼 원격 앱 또는 데스크톱과 상호 작용할 수 있습니다. Azure AD 응용 프로그램 프록시을 사용 하 여 모든 유형의 리치 클라이언트 앱에 대 한 사전 인증 및 조건부 액세스 정책을 적용 하 여 RDS 배포의 보안을 강화할 수 있습니다. 지침은 [Azure AD 응용 프로그램 프록시를 사용 하 여 원격 데스크톱 게시](../manage-apps/application-proxy-integrate-with-remote-desktop-services.md)를 참조 하세요.
 
---

### <a name="next-generation-azure-ad-b2c-user-flows-in-public-preview"></a>공개 미리 보기로 제공 되는 다음 세대 Azure AD B2C 사용자 흐름

**유형:** 새로운 기능  
**서비스 범주:** B2C - 소비자 ID 관리  
**제품 기능:** B2B/B2C
 
간소화 된 사용자 흐름 환경에는 미리 보기 기능을 제공 하는 기능 패리티가 제공 되며 새로운 모든 기능을 위한 홈입니다. 사용자는 동일한 사용자 흐름 내에서 새로운 기능을 사용 하도록 설정할 수 있으므로 모든 새 기능 릴리스에서 여러 버전을 만들 필요가 없습니다. 마지막으로, 사용자에 게 친숙 한 새 UX를 사용 하면 사용자 흐름을 간편 하 게 선택 하 고 만들 수가 있습니다. 이제 [사용자 흐름을 만들어](../../active-directory-b2c/tutorial-create-user-flows.md)사용해 보세요. 

사용자 흐름에 대 한 자세한 내용은 [Azure Active Directory B2C 사용자 흐름 버전](../../active-directory-b2c/user-flow-versions.md)을 참조 하세요.

---

### <a name="new-federated-apps-available-in-azure-ad-application-gallery---july-2020"></a>Azure AD 응용 프로그램 갤러리에서 사용할 수 있는 새로운 페더레이션된 앱-7 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 엔터프라이즈 앱  
**제품 기능:** 타사 통합
 
7 월 2020에 앱 갤러리에 페더레이션 지원과 함께 다음 55 새 응용 프로그램을 추가 했습니다.

[사용자의 손을 ap](http://www.rmit.com.ar/), [Appreiz](https://microsoftteams.appreiz.com/), [Inextor 자격 증명 모음](https://inexto.com/inexto-suite/inextor) [Beekast](https://my.beekast.com/), [Templafy openid connect Connect](https://app.templafy.com/), [PeterConnects 접수원](https://msteams.peterconnects.com/), a [Hac-coa](https://appfusions.alohacloud.com/auth), [Control 타워](https://bpm.tnxcorp.com/sso/microsoft), [cocoom](https://start.cocoom.com/), [동전 건설 클라우드](https://sso.coinsconstructioncloud.com/#login/), [Medxnote MT](https://task.teamsmain.medx.im/authorization), [Reflekt](https://reflekt.konsolute.com/login), [rever](https://app.reverscore.net/access), [MyCompanyArchive](https://login.mycompanyarchive.com/), [GReminders](https://app.greminders.com/o365-oauth), [Titanfile](../saas-apps/titanfile-tutorial.md), [Wootric](../saas-apps/wootric-tutorial.md), [SolarWinds Orion](https://support.solarwinds.com/SuccessCenter/s/orion-platform?language=en_US), OpenText  [Directory Services](../saas-apps/opentext-directory-services-tutorial.md), [Coite](../saas-apps/datasite-tutorial.md), [blogin](../saas-apps/blogin-tutorial.md), [IntSights](../saas-apps/intsights-tutorial.md), [Kpifire](../saas-apps/kpifire-tutorial.md), [Textline](../saas-apps/textline-tutorial.md), [Cloud 아카데미-SSO](../saas-apps/cloud-academy-sso-tutorial.md), [Community Spark](../saas-apps/community-spark-tutorial.md), [작업](../saas-apps/chatwork-tutorial.md), [cloudsign](../saas-apps/cloudsign-tutorial.md), [C3M Cloud Control](../saas-apps/c3m-cloud-control-tutorial.md), [SmartHR](https://smarthr.jp/), [numlyengage](../saas-apps/numlyengage-tutorial.md), [Michigan Data hubs Single Sign-on](../saas-apps/michigan-data-hub-single-sign-on-tutorial.md), [송신](../saas-apps/egress-tutorial.md), [Sendsafely](../saas-apps/sendsafely-tutorial.md), [Eletive](https://app.eletive.com/), [Right 사이버 보안 ADI](https://right-hand.ai/), [Fyde Enterprise Authentication](https://enterprise.fyde.com/), [verme](../saas-apps/verme-tutorial.md), [Lenses.io](../saas-apps/lensesio-tutorial.md), [Momenta](../saas-apps/momenta-tutorial.md), [uprise](https://app.uprise.co/sign-in), [Q](https://q.moduleq.com/login), [cloudsign](../saas-apps/cloudcords-tutorial.md), [TellMe 봇](https://tellme365liteweb.azurewebsites.net/), [영감](https://app.inspiresoftware.com/), [maverics id Orchestrator SAML 커넥터](https://www.strata.io/identity-fabric/), [smartschool (school Management System)](https://smartschoolz.com/login), [Zepto-Intelligent 계측](https://user.zepto-ai.com/signin), [Studi.ly](https://studi.ly/), [plan](http://www.trackplanfm.com/), [Skedda](../saas-apps/skedda-tutorial.md) [, WhosOnLocation,](../saas-apps/whos-on-location-tutorial.md) [Coggle](../saas-apps/coggle-tutorial.md), [kemp loadmaster](https://kemptechnologies.com/cloud-load-balancer/), [browserstack Single sign-on](../saas-apps/browserstack-single-sign-on-tutorial.md)

여기에서 모든 응용 프로그램의 설명서를 찾을 수도 있습니다. https://aka.ms/AppsTutorial

Azure AD 앱 갤러리에 응용 프로그램을 나열 하려면 여기에서 세부 정보를 참조 하세요. https://aka.ms/AzureADAppRequest

---

### <a name="new-provisioning-connectors-in-the-azure-ad-application-gallery---july-2020"></a>Azure AD 응용 프로그램 갤러리의 새로운 프로 비전 커넥터-7 월 2020

**유형:** 새로운 기능  
**서비스 범주:** 앱 프로비전  
**제품 기능:** 타사 통합

이제 새로 통합 된 앱 [LinkedIn Learning](../saas-apps/linkedin-learning-provisioning-tutorial.md)에 대 한 사용자 계정을 만들고, 업데이트 하 고, 삭제할 수 있습니다.

자동화된 사용자 계정 프로비저닝을 사용하여 조직의 보안을 강화하는 방법에 대한 자세한 내용은 [Azure AD를 사용하여 SaaS 애플리케이션에 대한 사용자 프로비저닝 자동화](../app-provisioning/user-provisioning.md)를 참조하세요.

---

### <a name="view-role-assignments-across-all-scopes-and-ability-to-download-them-to-a-csv-file"></a>모든 범위에서 역할 할당을 확인 하 고 csv 파일로 다운로드할 수 있습니다.

**유형:** 변경된 기능  
**서비스 범주:** Azure AD 역할  
**제품 기능:** 액세스 제어
 
이제 Azure AD 포털의 "역할 및 관리자" 탭에서 역할에 대 한 모든 범위에서 역할 할당을 볼 수 있습니다. 각 역할에 대 한 역할 할당을 CSV 파일로 다운로드할 수도 있습니다. 역할 할당을 보고 추가 하는 방법에 대 한 지침은 [Azure Active Directory에서 관리자 역할 보기 및 할당](../roles/manage-roles-portal.md)을 참조 하세요.
 
---

### <a name="azure-multi-factor-authentication-software-development-azure-mfa-sdk-deprecation"></a>Azure Multi-Factor Authentication 소프트웨어 개발 (Azure MFA SDK) 사용 중단

**유형:** 사용되지 않음  
**서비스 범주:** MFA  
**제품 기능:** Id 보안 & 보호
 
Azure MFA SDK (Multi-Factor Authentication 소프트웨어 개발)는 11 월 2017에 처음 발표 된 2018 년 11 월 14 일에 종료 되었습니다. Microsoft는 2020 년 9 월 30 일에 적용 되는 SDK 서비스를 종료 합니다. SDK에 대 한 모든 호출이 실패 합니다.

조직에서 Azure MFA SDK를 사용 하는 경우 2020 년 9 월 30 일까 지 마이그레이션 해야 합니다.
- MIM 용 Azure MFA SDK: MIM에서 SDK를 사용 하는 경우 다음 [지침](/microsoft-identity-manager/working-with-mfaserver-for-mim)에 따라 Azure mfa 서버로 마이그레이션하고 PAM (Privileged Access Management)을 활성화 해야 합니다.   
- 사용자 지정 된 앱 용 azure MFA SDK: Azure AD에 앱을 통합 하 고 조건부 액세스를 사용 하 여 MFA를 적용 하는 것이 좋습니다. 시작 하려면이 [페이지](../manage-apps/plan-an-application-integration.md)를 검토 합니다. 

---

