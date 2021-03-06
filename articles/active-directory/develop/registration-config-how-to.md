---
title: Azure AD 앱 등록에 대 한 끝점 가져오기
titleSuffix: Microsoft identity platform
description: Azure AD에 개발 하거나 등록 중인 사용자 지정 응용 프로그램에 대 한 인증 끝점을 찾는 방법입니다.
services: active-directory
author: rwike77
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.custom: aaddev
ms.workload: identity
ms.topic: conceptual
ms.date: 05/07/2020
ms.author: ryanwi
ROBOTS: NOINDEX
ms.openlocfilehash: 3afaf654228511a357461a9e762be0b04acc65c6
ms.sourcegitcommit: 2488894b8ece49d493399d2ed7c98d29b53a5599
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98064167"
---
# <a name="how-to-discover-endpoints"></a>끝점을 검색 하는 방법

[Azure Portal](https://portal.azure.com)에서 애플리케이션의 인증 엔드포인트를 찾을 수 있습니다.

1. <a href="https://portal.azure.com/" target="_blank">Azure Portal<span class="docon docon-navigate-external x-hidden-focus"></span></a>에 로그인합니다.
1. **Azure Active Directory** 를 선택합니다.
1. **관리** 에서 **앱 등록** 를 선택 하 고 최상위 메뉴에서 **끝점** 을 선택 합니다.

    **끝점** 페이지가 표시 되 고 테 넌 트의 인증 끝점이 표시 됩니다.
    
    응용 프로그램과 관련 된 인증 요청을 만들 수 있도록 **응용 프로그램 (클라이언트) ID** 와 함께 사용 하는 인증 프로토콜과 일치 하는 끝점을 사용 합니다.

**국가별 클라우드** (예: Azure ad 중국, 독일 및 미국 정부)에는 고유한 앱 등록 포털과 Azure AD 인증 끝점이 있습니다. [국가별 클라우드 개요](authentication-national-cloud.md)에서 자세히 알아보세요.

## <a name="next-steps"></a>다음 단계

다른 Azure 환경의 끝점에 대 한 자세한 내용은 [국가별 클라우드 개요](authentication-national-cloud.md)를 참조 하세요.
