---
title: 국가 클라우드 앱에서 MSAL 사용 | Microsoft
titleSuffix: Microsoft identity platform
description: 응용 프로그램 개발자는 MSAL (Microsoft 인증 라이브러리)을 사용 하 여 보안 웹 Api를 호출 하기 위해 토큰을 획득할 수 있습니다. 이러한 웹 Api는 Microsoft Graph, 다른 Microsoft Api, 파트너 웹 api 또는 고유한 web API 일 수 있습니다. MSAL은 다수의 애플리케이션 아키텍처와 플랫폼을 지원합니다.
services: active-directory
author: negoe
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 11/22/2019
ms.author: negoe
ms.reviewer: marsma, nacanuma
ms.custom: aaddev
ms.openlocfilehash: 5a032f45027cc4bffc7f2bc46c6ea1a69a1b83e4
ms.sourcegitcommit: c136985b3733640892fee4d7c557d40665a660af
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98178622"
---
# <a name="use-msal-in-a-national-cloud-environment"></a>국가별 클라우드 환경에서 MSAL 사용

소 버린 클라우드 라고도 하는 [국가별 클라우드](authentication-national-cloud.md)는 물리적으로 격리 된 Azure 인스턴스입니다. 이러한 Azure 지역에서는 데이터 상주, 주권 및 규정 준수 요구 사항이 지리적 경계 내에서 적용 되는지 확인 합니다.

Microsoft의 전 세계 클라우드 외에도 MSAL (Microsoft 인증 라이브러리)을 사용 하면 국가 클라우드의 응용 프로그램 개발자가 보안 웹 Api를 인증 하 고 호출 하기 위해 토큰을 획득할 수 있습니다. 이러한 웹 Api는 Microsoft Graph 또는 다른 Microsoft Api 일 수 있습니다.

글로벌 클라우드를 포함 하 여 Azure AD (Azure Active Directory)는 다음 국가 클라우드에 배포 됩니다.  

- Azure Government
- Azure 중국 21Vianet
- Azure 독일

이 가이드에서는 회사 및 학교 계정에 로그인 하 고, 액세스 토큰을 가져오고, [Azure Government 클라우드](https://azure.microsoft.com/global-infrastructure/government/) 환경에서 Microsoft Graph API를 호출 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

시작 하기 전에 이러한 필수 구성 요소를 충족 하는지 확인 합니다.

### <a name="choose-the-appropriate-identities"></a>적절 한 id 선택

[Azure Government](../../azure-government/index.yml) 응용 프로그램은 Azure ad 정부 Id 및 Azure ad 공용 id를 사용 하 여 사용자를 인증할 수 있습니다. 이러한 id 중 하나를 사용할 수 있으므로 시나리오에 대해 선택 해야 하는 기관 끝점을 결정 해야 합니다.

- Azure AD Public: 조직에 Microsoft 365 (공용 또는 GCC) 또는 다른 응용 프로그램을 지원 하기 위한 Azure AD 공용 테 넌 트가 이미 있는 경우 일반적으로 사용 됩니다.
- Azure AD 정부: 조직에 이미 Office 365 (GCC High 또는 DoD)를 지원 하기 위한 Azure AD 정부 테 넌 트가 있는 경우 또는 Azure AD 정부에서 새 테 넌 트를 만드는 경우 일반적으로 사용 됩니다.

결정 한 후에는 앱 등록을 수행 하는 특별 한 고려 사항이 있습니다. Azure Government 응용 프로그램에 대해 Azure AD 공용 id를 선택 하는 경우 Azure AD 공용 테 넌 트에서 응용 프로그램을 등록 해야 합니다.

### <a name="get-an-azure-government-subscription"></a>Azure Government 구독 가져오기

Azure Government 구독을 가져오려면 [Azure Government에서 구독 관리 및 연결](../../azure-government/compare-azure-government-global-azure.md)을 참조 하세요.

Azure Government 구독이 없는 경우 시작 하기 전에 [무료 계정](https://azure.microsoft.com/global-infrastructure/government/request/) 을 만듭니다.

특정 프로그래밍 언어에서 국가 클라우드를 사용 하는 방법에 대 한 자세한 내용은 해당 언어와 일치 하는 탭을 선택 합니다.

## <a name="net"></a>[.NET](#tab/dotnet)

MSAL.NET를 사용 하 여 사용자를 로그인 하 고 토큰을 획득 하 고 국가별 클라우드에서 Microsoft Graph API를 호출할 수 있습니다.

다음 자습서에서는 .NET Core 2.2 MVC 웹 앱을 빌드하는 방법을 보여 줍니다. 앱은 Openid connect Connect를 사용 하 여 국가 클라우드에 속한 조직의 회사 및 학교 계정으로 사용자를 로그인 합니다.

- 사용자를 로그인 하 고 토큰을 획득 하려면 [Microsoft id 플랫폼을 사용 하 여 소 버린 클라우드에서 ASP.NET Core 웹 앱 로그인 사용자 빌드](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/1-WebApp-OIDC/1-4-Sovereign#build-an-aspnet-core-web-app-signing-in-users-in-sovereign-clouds-with-the-microsoft-identity-platform)자습서를 따르세요.
- Microsoft Graph API를 호출 하려면이 자습서를 수행 합니다. microsoft [id 플랫폼을 사용 하 여 Microsoft 국가별 클라우드에서 회사 및 학교 계정을 사용 하 여 사용자가 로그인 하는 대신 microsoft id 플랫폼을 사용 하 여 ASP.NET Core 2.x 웹 앱에서 MICROSOFT GRAPH API를 호출](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-4-Sovereign-Call-MSGraph#using-the-microsoft-identity-platform-to-call-the-microsoft-graph-api-from-an-an-aspnet-core-2x-web-app-on-behalf-of-a-user-signing-in-using-their-work-and-school-account-in-microsoft-national-cloud)합니다.

## <a name="javascript"></a>[JavaScript](#tab/javascript)

소 버린 클라우드에 대해 MSAL.js 응용 프로그램을 사용 하도록 설정 하려면:

### <a name="step-1-register-your-application"></a>1단계: 애플리케이션 등록

1. <a href="https://portal.azure.us/" target="_blank">Azure Portal<span class="docon docon-navigate-external x-hidden-focus"></span></a>에 로그인합니다.

   다른 국가별 클라우드의 Azure Portal 끝점을 찾으려면 [앱 등록 끝점](authentication-national-cloud.md#app-registration-endpoints)을 참조 하세요.

1. 여러 테넌트에 액세스할 수 있는 경우 위쪽 메뉴의 **디렉터리 + 구독** 필터 :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false":::를 사용하여 애플리케이션을 등록하려는 테넌트를 선택합니다.
1. **Azure Active Directory** 를 검색하고 선택합니다.
1. **관리** 아래에서 **앱 등록** > **새 등록** 을 선택합니다.
1. 애플리케이션의 **이름** 을 입력합니다. 이 이름은 앱의 사용자에게 표시될 수 있으며 나중에 변경할 수 있습니다.
1. **지원되는 계정 유형** 에서 **모든 조직 디렉터리의 계정** 을 선택합니다.
1. **리디렉션 URI** 섹션에서 **웹** 플랫폼을 선택 하 고 웹 서버에 따라 응용 프로그램의 URL로 값을 설정 합니다. Visual Studio 및 노드에서 리디렉션 URL을 설정 하 고 가져오는 방법에 대 한 지침은 다음 섹션을 참조 하세요.
1. **등록** 을 선택합니다.
1. **개요** 페이지에서 나중에 사용할 **응용 프로그램 (클라이언트) ID** 값을 적어 둡니다.
    이 자습서에서는 [암시적 부여 흐름](v2-oauth2-implicit-grant-flow.md)을 사용 하도록 설정 해야 합니다. 
1. **관리** 에서 **인증** 을 선택합니다.
1. **암시적 권한 부여** 에서 **ID 토큰** 및 **액세스 토큰** 을 선택 합니다. ID 토큰 및 액세스 토큰은이 앱이 사용자에 게 로그인 하 고 API를 호출 해야 하기 때문에 필요 합니다.
1. **저장** 을 선택합니다.

### <a name="step-2--set-up-your-web-server-or-project"></a>2 단계: 웹 서버 또는 프로젝트 설정

- 노드와 같은 로컬 웹 서버에 대 한 [프로젝트 파일을 다운로드](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/quickstart.zip) 합니다.

  또는

- [Visual Studio 프로젝트를 다운로드](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/vsquickstart.zip)합니다.

그런 다음 코드 샘플을 실행 하기 전에 구성 하도록 [JAVASCRIPT SPA 구성](#step-4-configure-your-javascript-spa) 으로 건너뜁니다.

### <a name="step-3-use-the-microsoft-authentication-library-to-sign-in-the-user"></a>3 단계: Microsoft 인증 라이브러리를 사용 하 여 사용자 로그인

[JavaScript 자습서](tutorial-v2-javascript-spa.md#create-your-project) 의 단계를 수행 하 여 프로젝트를 만들고 msal과 통합 하 여 사용자를 로그인 합니다.

### <a name="step-4-configure-your-javascript-spa"></a>4 단계: JavaScript SPA 구성

프로젝트 설정 중에 생성된 `index.html` 파일에서 애플리케이션 등록 정보를 추가합니다. 맨 위에 있는 다음 코드를 `index.html` 파일 본문의 `<script></script>` 태그 내에 추가합니다.

```javascript
const msalConfig = {
    auth:{
        clientId: "Enter_the_Application_Id_here",
        authority: "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here",
        }
}

const graphConfig = {
        graphEndpoint: "https://graph.microsoft.us",
        graphScopes: ["user.read"],
}

// create UserAgentApplication instance
const myMSALObj = new UserAgentApplication(msalConfig);
```

해당 코드에서 다음을 수행 합니다.

- `Enter_the_Application_Id_here` 등록 한 응용 프로그램에 대 한 **응용 프로그램 (클라이언트) ID** 값입니다.
- `Enter_the_Tenant_Info_Here` 는 다음 옵션 중 하나로 설정됩니다.
    - 응용 프로그램이 **이 조직 디렉터리에서 계정을** 지 원하는 경우이 값을 테 넌 트 ID 또는 테 넌 트 이름 (예: contoso.microsoft.com)으로 바꿉니다.
    - 응용 프로그램에서 **조직 디렉터리의 계정을** 지 원하는 경우이 값을로 바꿉니다 `organizations` .

    모든 국가별 클라우드의 인증 끝점을 찾으려면 [AZURE AD 인증 끝점](./authentication-national-cloud.md#azure-ad-authentication-endpoints)을 참조 하세요.

    > [!NOTE]
    > 개인 Microsoft 계정은 국가별 클라우드에서 지원 되지 않습니다.

- `graphEndpoint` 는 미국 정부의 Microsoft 클라우드의 Microsoft Graph 끝점입니다.

   모든 국가별 클라우드의 Microsoft Graph 끝점을 찾으려면 [국가별 클라우드의 Microsoft Graph 끝점](/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints)을 참조 하세요.

## <a name="python"></a>[Python](#tab/python)

소 버린 클라우드 용 MSAL Python 응용 프로그램을 사용 하도록 설정 하려면:

- 클라우드에 따라 특정 포털에 응용 프로그램을 등록 합니다. 포털을 선택 하는 방법에 대 한 자세한 내용은 [앱 등록 끝점](authentication-national-cloud.md#app-registration-endpoints) 을 참조 하세요.
- 다음에 설명 된 클라우드에 따라 구성에 대 한 몇 가지 변경 내용이 포함 된 리포지토리의 [샘플](https://github.com/AzureAD/microsoft-authentication-library-for-python/tree/dev/sample) 을 사용 합니다.
- 응용 프로그램을 등록 한 클라우드에 따라 특정 권한을 사용 합니다. 다른 클라우드의 기관에 대 한 자세한 내용은 [Azure AD 인증 끝점](authentication-national-cloud.md#azure-ad-authentication-endpoints)을 참조 하세요.

    권한 예는 다음과 같습니다.

    ```json
    "authority": "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here"
    ```

- Microsoft Graph API를 호출 하려면 사용 중인 클라우드와 관련 된 끝점 URL이 필요 합니다. 모든 국가별 클라우드의 Microsoft Graph 끝점을 찾으려면 [Microsoft Graph 및 그래프 탐색기 서비스 루트 끝점](/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints)을 참조 하세요.

    다음은 범위가 있는 Microsoft Graph 끝점의 예입니다.

    ```json
    "endpoint" : "https://graph.microsoft.us/v1.0/me"
    "scope": "User.Read"
    ```

## <a name="java"></a>[Java](#tab/java)

소 버린 클라우드 용 Java 응용 프로그램에 대해 MSAL을 사용 하도록 설정 하려면 다음을 수행 합니다.

- 클라우드에 따라 특정 포털에 응용 프로그램을 등록 합니다. 포털을 선택 하는 방법에 대 한 자세한 내용은 [앱 등록 끝점](authentication-national-cloud.md#app-registration-endpoints) 을 참조 하세요.
- 다음에 언급 된 클라우드에 따라 구성에 대 한 몇 가지 변경 내용이 포함 된 리포지토리의 [샘플](https://github.com/AzureAD/microsoft-authentication-library-for-java/tree/dev/src/samples) 을 사용 합니다.
- 응용 프로그램을 등록 한 클라우드에 따라 특정 권한을 사용 합니다. 다른 클라우드의 기관에 대 한 자세한 내용은 [Azure AD 인증 끝점](authentication-national-cloud.md#azure-ad-authentication-endpoints)을 참조 하세요.

권한 예는 다음과 같습니다.

```json
"authority": "https://login.microsoftonline.us/Enter_the_Tenant_Info_Here"
```

- Microsoft Graph API를 호출 하려면 사용 중인 클라우드와 관련 된 끝점 URL이 필요 합니다. 모든 국가별 클라우드의 Microsoft Graph 끝점을 찾으려면 [Microsoft Graph 및 그래프 탐색기 서비스 루트 끝점](/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints)을 참조 하세요.

다음은 범위를 포함 하는 그래프 끝점의 예입니다.

```json
"endpoint" : "https://graph.microsoft.us/v1.0/me"
"scope": "User.Read"
```

## <a name="objective-c"></a>[Objective-C](#tab/objc)

IOS 및 macOS 용 MSAL을 사용 하 여 국가별 클라우드에서 토큰을 가져올 수 있지만 만들 때 추가 구성이 필요 `MSALPublicClientApplication` 합니다.

예를 들어 응용 프로그램을 국가 클라우드의 다중 테 넌 트 응용 프로그램 (미국 정부 기관)으로 만들려면 다음을 작성할 수 있습니다.

```objc
MSALAADAuthority *aadAuthority =
                [[MSALAADAuthority alloc] initWithCloudInstance:MSALAzureUsGovernmentCloudInstance
                                                   audienceType:MSALAzureADMultipleOrgsAudience
                                                      rawTenant:nil
                                                          error:nil];

MSALPublicClientApplicationConfig *config =
                [[MSALPublicClientApplicationConfig alloc] initWithClientId:@"<your-client-id-here>"
                                                                redirectUri:@"<your-redirect-uri-here>"
                                                                  authority:aadAuthority];

NSError *applicationError = nil;
MSALPublicClientApplication *application =
                [[MSALPublicClientApplication alloc] initWithConfiguration:config error:&applicationError];
```

## <a name="swift"></a>[Swift](#tab/swift)

IOS 및 macOS 용 MSAL을 사용 하 여 국가별 클라우드에서 토큰을 가져올 수 있지만 만들 때 추가 구성이 필요 `MSALPublicClientApplication` 합니다.

예를 들어 응용 프로그램을 국가 클라우드의 다중 테 넌 트 응용 프로그램 (미국 정부 기관)으로 만들려면 다음을 작성할 수 있습니다.

```swift
let authority = try? MSALAADAuthority(cloudInstance: .usGovernmentCloudInstance, audienceType: .azureADMultipleOrgsAudience, rawTenant: nil)

let config = MSALPublicClientApplicationConfig(clientId: "<your-client-id-here>", redirectUri: "<your-redirect-uri-here>", authority: authority)
if let application = try? MSALPublicClientApplication(configuration: config) { /* Use application */}
```

---

## <a name="next-steps"></a>다음 단계

각 클라우드의 Azure Portal Url 및 토큰 끝점 목록은 [국가별 클라우드 인증 끝점](authentication-national-cloud.md) 을 참조 하세요.

국가별 클라우드 설명서:

- [Azure Government](../../azure-government/index.yml)
- [Azure China 21Vianet](/azure/china/)
- [Azure 독일](../../germany/index.yml)