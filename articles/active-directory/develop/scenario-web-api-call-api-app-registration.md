---
title: 웹 Api를 호출 하는 웹 API 등록 | Microsoft
titleSuffix: Microsoft identity platform
description: 다운스트림 웹 Api (앱 등록)를 호출 하는 web API를 빌드하는 방법에 대해 알아봅니다.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 8349b7a53eb7b03b27c695bb24c8cb9bc665a1ac
ms.sourcegitcommit: 5cdd0b378d6377b98af71ec8e886098a504f7c33
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2021
ms.locfileid: "98756350"
---
# <a name="a-web-api-that-calls-web-apis-app-registration"></a>웹 Api를 호출 하는 웹 API: 앱 등록

다운스트림 웹 api를 호출 하는 web API는 보호 된 웹 API와 동일한 등록을 포함 합니다. 따라서 [보호 된 웹 API](scenario-protected-web-api-app-registration.md)의 지침에 따라 앱을 등록 해야 합니다.

웹 앱은 이제 웹 Api를 호출 하므로 기밀 클라이언트 응용 프로그램이 됩니다. 그 이유는 추가 등록 정보가 필요 하기 때문입니다. 앱은 Microsoft id 플랫폼과 암호 (클라이언트 자격 증명)를 공유 해야 합니다.

[!INCLUDE [Pre-requisites](../../../includes/active-directory-develop-scenarios-registration-client-secrets.md)]

## <a name="api-permissions"></a>API 사용 권한

웹 앱은 전달자 토큰을 받은 사용자를 대신 하 여 Api를 호출 합니다. 웹 앱은 위임 된 권한을 요청 해야 합니다. 자세한 내용은 [웹 API에 액세스할 수 있는 권한 추가](quickstart-configure-app-access-web-apis.md#add-permissions-to-access-your-web-api)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

이 시나리오에서 [앱 코드 구성](scenario-web-api-call-api-app-configuration.md)의 다음 문서로 이동 합니다.
