---
title: Azure Front 도어에서 HTTP 헤더에 대 한 프로토콜 지원 | Microsoft Docs
description: 이 문서에서는 Front 도어가 지 원하는 HTTP 헤더 프로토콜에 대해 설명 합니다.
services: frontdoor
documentationcenter: ''
author: duongau
ms.service: frontdoor
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/04/2020
ms.author: duau
ms.openlocfilehash: 7f40b48473c04238d504288307039948fcacf90a
ms.sourcegitcommit: 63d0621404375d4ac64055f1df4177dfad3d6de6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97511147"
---
# <a name="protocol-support-for-http-headers-in-azure-front-door"></a>Azure 전면 도어의 HTTP 헤더에 대 한 프로토콜 지원
이 문서에서는 프런트 도어가 호출 경로의 일부를 사용 하 여 지 원하는 프로토콜에 대해 간략하게 설명 합니다 (이미지 참조). 다음 섹션에서는 Front 도어가 지 원하는 HTTP 헤더에 대 한 자세한 정보를 제공 합니다.

:::image type="content" source="./media/front-door-http-headers-protocol/front-door-protocol-summary.png" alt-text="Azure Front 도어 HTTP 헤더 프로토콜":::

>[!IMPORTANT]
>전면 도어는 여기에 설명 되지 않은 HTTP 헤더를 인증 하지 않습니다.

## <a name="client-to-front-door"></a>클라이언트-Front Door
전방 도어는 들어오는 요청을 수정 하지 않고 대부분의 헤더를 허용 합니다. 헤더를 포함 하 여 송신 하는 경우 들어오는 요청에서 X-FD-* 접두사가 포함 된 일부 예약 된 헤더가 제거 됩니다.

## <a name="front-door-to-backend"></a>Front Door-백 엔드

들어오는 요청에 대 한 헤더를 포함 하는 프런트 도어는 제한 때문에 제거 되지 않습니다. 또한 앞 도어는 다음 헤더를 추가 합니다.

| 헤더  | 예제 및 설명 |
| ------------- | ------------- |
| Via |  *Via: 1.1 Azure* </br> 프런트 도어는 클라이언트의 HTTP 버전을 Via 헤더에 대 한 *값으로 추가* 합니다. 이 헤더는 클라이언트의 HTTP 버전을 나타내며 Front 도어가 클라이언트와 백 엔드 간의 요청을 위한 중간 수신자 였습니다.  |
| X-Azure-ClientIP | *X-y: 127.0.0.1* </br> 처리 중인 요청과 연결 된 클라이언트 IP 주소를 나타냅니다. 예를 들어 프록시에서 들어오는 요청은 원본 호출자의 IP 주소를 나타내기 위해 X로 전달 된 헤더를 추가할 수 있습니다. |
| SocketIP |  *SocketIP: 127.0.0.1* </br> 현재 요청이 시작 된 TCP 연결과 관련 된 소켓 IP 주소를 나타냅니다. 요청의 클라이언트 IP 주소는 사용자가 임의로 덮어쓸 수 있으므로 해당 소켓 IP 주소와 다를 수 있습니다.|
| X-Azure-참조 | *X-y-Ref: 0zxV + XAAAAABKMMOjBv2NT4TY6SQVjC0zV1NURURHRTA2MTkANDM3YzgyY2QtMzYwYS00YTU0LTk0YzMtNWZmNzA3NjQ3Nzgz* </br> Front 도어가 제공 하는 요청을 식별 하는 고유한 참조 문자열입니다. 액세스 로그를 검색 하는 데 사용 되며 문제 해결을 위해 중요 합니다.|
| X-Azure-RequestChain | *X-Azure-RequestChain: 홉 = 1* </br> 프런트 도어가 요청 루프를 검색 하는 데 사용 하는 헤더 이며, 사용자가 종속성을 사용 하지 않아야 합니다. |
| X-Azure-FDID | *X-Azure-FDID: 55ce4ed1-4b06-4bf1-b40e-4638452104da* <br/> 특정 전방 도어 리소스에서 가져온 요청을 식별 하는 참조 문자열입니다. 값은 Azure Portal에서 보거나 관리 API를 사용 하 여 검색할 수 있습니다. 이 헤더를 IP Acl과 함께 사용 하 여 특정 Front 도어 리소스의 요청만 수락 하도록 끝점을 잠글 수 있습니다. [자세한](front-door-faq.md#how-do-i-lock-down-the-access-to-my-backend-to-only-azure-front-door) 내용은 FAQ를 참조 하세요. |
| X-Forwarded-For | *X 전달-의 경우: 127.0.0.1* </br> X로 전달 된 (XFF) HTTP 헤더 필드는 HTTP 프록시 또는 부하 분산 장치를 통해 웹 서버에 연결 하는 클라이언트의 원래 IP 주소를 식별 하는 경우가 많습니다. 기존 XFF 헤더가 있는 경우 Front 도어가 클라이언트 소켓 IP를 추가 하거나 클라이언트 소켓 IP를 사용 하 여 XFF 헤더를 추가 합니다. |
| X-Forwarded-Host | *X 전달-호스트: contoso.azurefd.net* </br> X 전달 된 호스트 HTTP 헤더 필드는 호스트 HTTP 요청 헤더에서 클라이언트에 의해 요청 된 원래 호스트를 식별 하는 데 사용 되는 일반적인 방법입니다. 이는 프런트 도어의 호스트 이름이 요청을 처리 하는 백 엔드 서버에 대해 다를 수 있기 때문입니다. |
| X-Forwarded-Proto | *X 전달-프로토콜: http* </br> X 전달-프로토콜 HTTP 헤더 필드는 일반적으로 HTTP 요청의 원래 프로토콜을 식별 하는 데 사용 됩니다. 구성을 기반으로 하는 프런트 도어는 HTTPS를 사용 하 여 백 엔드와 통신할 수 있습니다. 역방향 프록시에 대 한 요청이 HTTP 인 경우에도 마찬가지입니다. |
| X FD-HealthProbe | HealthProbe HTTP 헤더 필드는 전면 도어에서 상태 프로브를 식별 하는 데 사용 됩니다. 이 헤더가 1로 설정 되 면 요청이 상태 프로브입니다. X 전달-호스트 헤더 필드를 사용 하 여 특정 전방 도어에서 엄격한 액세스를 원할 때를 사용할 수 있습니다. |
| X-Azure-FDID | *437c82cd-360a-4a54-94c3-5ff707647783* </br> 이 필드에는 들어오는 요청을 보낸 전방 도어를 식별 하는 데 사용할 수 있는 frontdoorID 포함 되어 있습니다. 이 필드는 Front 도어 서비스에 의해 채워집니다. | 

## <a name="front-door-to-client"></a>Front Door-클라이언트

백 엔드에서 프런트 도어로 전송 되는 모든 헤더도 클라이언트에 전달 됩니다. 다음은 프런트 도어에서 클라이언트로 전송 되는 헤더입니다.

| 헤더  | 예제 및 설명 |
| ------------- | ------------- |
| X-Azure-참조 |  *X-y-Ref: 0zxV + XAAAAABKMMOjBv2NT4TY6SQVjC0zV1NURURHRTA2MTkANDM3YzgyY2QtMzYwYS00YTU0LTk0YzMtNWZmNzA3NjQ3Nzgz* </br> 이는 액세스 로그를 검색 하는 데 사용 되므로 문제 해결에 중요 한, Front 도어가 제공 하는 요청을 식별 하는 고유한 참조 문자열입니다.|
| X 캐시 | *X 캐시: TCP_HIT* </br> 이 헤더는 요청의 캐시 상태를 설명 하며,이를 통해 응답 콘텐츠가 프런트 도어 캐시에서 제공 되는지 여부를 식별할 수 있습니다. |

다음과 같은 선택적 응답 헤더를 사용 하도록 설정 하려면 "DebugInfo: 1" 요청 헤더를 전송 해야 합니다.

| 헤더  | 예제 및 설명 |
| ------------- | ------------- |
| OriginStatusCode |  *OriginStatusCode: 503* </br> 이 헤더는 백 엔드에서 반환한 HTTP 상태 코드를 포함 합니다. 이 헤더를 사용 하 여 백 엔드 로그를 거치지 않고 백 엔드에서 실행 되는 응용 프로그램에서 반환 된 HTTP 상태 코드를 식별할 수 있습니다. 이 상태 코드는 프런트 도어로 클라이언트에 보낸 응답의 HTTP 상태 코드와 다를 수 있습니다. 이 헤더를 사용 하 여 백 엔드가 오동작 또는 Front 도어 서비스와 관련 된 문제 인지 확인할 수 있습니다. |
| X-Azure-InternalError | 이 헤더에는 요청을 처리할 때 Front 문이 제공 하는 오류 코드가 포함 됩니다. 이 오류는 프론트 도어 서비스/인프라의 내부 문제를 나타냅니다. 지원할 문제를 보고 합니다.  |
| X-Azure-ExternalError | *X-Azure-ExternalError: 0x830c1011, 인증 기관에 익숙하지 않습니다.* </br> 이 헤더는 프런트 도어 서버에서 요청을 처리 하기 위해 백 엔드 서버에 대 한 연결을 설정 하는 동안 발생 하는 오류 코드를 보여 줍니다. 이 헤더는 프런트 도어와 백 엔드 응용 프로그램 간의 연결 문제를 식별 하는 데 도움이 됩니다. 이 헤더에는 백 엔드에 대 한 연결 문제를 식별 하는 데 도움이 되는 자세한 오류 메시지가 포함 됩니다 (예: DNS 확인, 잘못 된 인증서 등). |

## <a name="next-steps"></a>다음 단계

- [Front Door 만들기](quickstart-create-front-door.md)
- [프런트 도어 작동 방법](front-door-routing-architecture.md)
