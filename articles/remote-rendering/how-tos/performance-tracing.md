---
title: 클라이언트 쪽 성능 추적 만들기
description: WPF를 사용 하 여 클라이언트 쪽 성능 프로 파일링에 대 한 모범 사례
author: florianborn71
ms.author: flborn
ms.date: 12/11/2019
ms.topic: conceptual
ms.openlocfilehash: 1d4ce68bdda5fbc3dfdb7396141289a58dab5bd1
ms.sourcegitcommit: 957c916118f87ea3d67a60e1d72a30f48bad0db6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92204098"
---
# <a name="create-client-side-performance-traces"></a>클라이언트 쪽 성능 추적 만들기

Azure 원격 렌더링의 성능이 원하는 만큼 적절 하지 않을 수 있는 많은 이유가 있습니다. 클라우드 서버의 순수 렌더링 성능 외에 특히 네트워크 연결의 품질은 환경에 상당한 영향을 미칩니다. 서버 성능을 프로 파일링 하려면 [서버 쪽 성능 쿼리](../overview/features/performance-queries.md)챕터를 참조 하세요.

이 장에서는를 통해 잠재적 클라이언트 쪽 병목 상태를 식별 하는 방법을 중점적으로 설명 *:::no-loc text="performance traces":::* 합니다.

## <a name="getting-started"></a>시작

Windows 기능을 처음 접하는 경우 :::no-loc text="performance tracing"::: 이 섹션에서는 가장 기본적인 용어와 응용 프로그램을 시작 하는 방법을 설명 합니다.

### <a name="installation"></a>설치

ARR을 사용 하 여 추적 하는 데 사용 되는 응용 프로그램은 모든 Windows 개발에 사용할 수 있는 범용 도구입니다. [Windows 성능 도구 키트](/windows-hardware/test/wpt/)를 통해 제공 됩니다. 이 도구 키트를 다운로드 하려면 [Windows 평가 및 배포 키트](/windows-hardware/get-started/adk-install)를 다운로드 하세요.

### <a name="terminology"></a>용어

성능 추적에 대 한 정보를 검색 하는 경우 다양 한 용어를 제공 합니다. 가장 중요 한 항목은 다음과 같습니다.

* `ETW`
* `ETL`
* `WPR`
* `WPA`

**ETW** 는 [ **W**windows에 **T**대 한 **E**환풍구](/windows/win32/etw/about-event-tracing)를 나타냅니다. Windows에 기본 제공 되는 효율적인 커널 수준 추적 기능에 대 한 단순한 이름입니다. ETW를 지 원하는 응용 프로그램에서 성능 문제를 추적 하는 데 도움이 될 수 있는 작업을 기록 하기 때문에 *이벤트* 추적 이라고 합니다. 기본적으로 운영 체제는 디스크 액세스, 작업 스위치 등과 같은 항목에 대 한 이벤트를 이미 내보냅니다. ARR과 같은 응용 프로그램은 사용자 지정 이벤트 (예: 삭제 된 프레임, 네트워크 지연 등)를 추가로 내보냅니다.

**ETL** 은 **E**배기 **T**레이스 **L**ogging을 나타냅니다. 단순히 추적이 수집 (기록) 되었으며 일반적으로 추적 데이터를 저장 하는 파일에 대 한 파일 확장명으로 사용 됨을 의미 합니다. 따라서 추적을 수행할 때 일반적으로 \* 나중에 .etl 파일을 갖게 됩니다.

**WPR** 는 [ **W**windows **P**성능 **R**ecorder](/windows-hardware/test/wpt/windows-performance-recorder) 를 나타내며,는 이벤트 추적 기록을 시작 하 고 중지 하는 응용 프로그램의 이름입니다. WPR는 \* 로깅할 정확한 이벤트를 구성 하는 프로필 파일 (.wggga)을 사용 합니다. 이러한 `wprp` 파일은 ARR SDK와 함께 제공 됩니다. 데스크톱 PC에서 추적을 수행할 때 WPR를 직접 시작할 수 있습니다. HoloLens에서 추적을 수행할 때 일반적으로 웹 인터페이스를 통해 이동 합니다.

**WPA** 는 [ **W**windows **P**성능 **A**nalyzer](/windows-hardware/test/wpt/windows-performance-analyzer) 를 나타내며, \* 데이터를 통해 etl 파일 및 자세히 살펴볼를 열어 성능 문제를 식별 하는 데 사용 되는 GUI 응용 프로그램의 이름입니다. WPA를 사용 하면 다양 한 조건에 따라 데이터를 정렬 하 고, 여러 가지 방법으로 데이터를 표시 하 고, 세부 정보를 확인 하 고, 정보를 연결할 수 있습니다

ETL 추적은 모든 Windows 장치 (로컬 PC, HoloLens, 클라우드 서버 등)에서 만들 수 있지만 일반적으로 디스크에 저장 되 고 데스크톱 PC에서 WPA를 사용 하 여 분석 됩니다. ETL 파일은 다른 개발자에 게 서 볼 수 있습니다. 그러나 파일 경로 및 IP 주소와 같은 중요 한 정보는 ETL 추적에서 캡처될 수 있습니다. ETW는 추적을 기록 하거나 추적을 분석 하는 두 가지 방법으로 사용할 수 있습니다. 기록을 추적 하는 것은 매우 간단 하며 최소한의 설정으로 수행 해야 합니다. 반면 추적을 분석 하는 경우에는 WPA 도구와 조사 중인 문제에 대 한 훌륭한 이해가 필요 합니다. WPA 학습에 대 한 일반적인 자료 뿐만 아니라 ARR 특정 추적을 해석 하는 방법에 대 한 지침을 제공 합니다.

## <a name="recording-a-trace-on-a-local-pc"></a>로컬 PC에서 추적 기록

ARR 성능 문제를 식별 하려면 HoloLens에서 직접 추적을 수행 하는 것이 좋습니다 .이는 진정한 성능 특성의 스냅숏을 가져오는 유일한 방법 이기 때문입니다. 그러나 특별히 HoloLens 성능 제한 없이 추적을 수행 하거나 WPA를 사용 하는 방법을 배우고 현실적인 추적이 필요 하지 않은 경우에는 다음을 수행 합니다.

### <a name="wpr-configuration"></a>WPR 구성

1. [:::no-loc text="Windows Performance Recorder":::](/windows-hardware/test/wpt/windows-performance-recorder) *시작 메뉴*에서를 시작 합니다.
1. **기타 옵션** 확장
1. **프로필 추가** ...를 클릭 합니다.
1. AzureRemoteRenderingNetworkProfiling 파일을 선택 합니다 *.* 이 파일은 ARR SDK의 *Tools/ETLProfiles*에서 찾을 수 있습니다.
   이제 프로필은 *사용자 지정 측정*아래 WPR에 나열 됩니다. 유일 하 게 사용할 수 있는 프로필 인지 확인 합니다.
1. *첫 번째 수준 심사*를 확장 합니다.
    * ARR 네트워킹 이벤트의 신속한 추적을 캡처하려면이 옵션을 **사용 하지 않도록 설정** 합니다.
    * ARR 네트워크 이벤트와 CPU 또는 메모리 사용량과 같은 다른 시스템 특성의 상관 관계를 설정 해야 하는 경우이 옵션을 **사용 하도록 설정** 합니다.
    * 이 옵션을 사용 하도록 설정 하는 경우 추적의 크기가 여러 기가바이트 이며 WPA에서 저장 하 고 여는 데 시간이 오래 걸릴 수 있습니다.

그런 다음 WPR 구성이 다음과 같이 표시 됩니다.

![WPR 구성](./media/wpr.png)

### <a name="recording"></a>기록 중

**시작** 을 클릭 하 여 추적 기록을 시작 합니다. 언제 든 지 기록을 시작 하 고 중지할 수 있습니다. 이 작업을 수행 하기 전에 응용 프로그램을 종료할 필요는 없습니다. 여기서 볼 수 있듯이, ETW는 항상 전체 시스템에 대 한 추적을 기록 하므로 추적할 응용 프로그램을 지정할 필요가 없습니다. `wprp`파일은 기록할 이벤트 유형을 지정 합니다.

**저장** 을 클릭 하 여 기록을 중지 하 고 ETL 파일을 저장할 위치를 지정 합니다.

이제 WPA에서 직접 열거나 다른 사용자에 게 보낼 수 있는 ETL 파일이 있습니다.

## <a name="recording-a-trace-on-a-hololens"></a>HoloLens에서 추적 기록

HoloLens에 추적을 기록 하려면 장치를 부팅 하 고 브라우저에 해당 IP 주소를 입력 하 여 *장치 포털*을 엽니다.

![디바이스 포털](./media/wpr-hl.png)

1. 왼쪽에서 *성능 > 성능 추적*으로 이동 합니다.
1. **사용자 지정 프로필** 선택
1. 클릭할 **:::no-loc text="Browse...":::**
1. AzureRemoteRenderingNetworkProfiling 파일을 선택 합니다 *.* 이 파일은 ARR SDK의 *Tools/ETLProfiles*에서 찾을 수 있습니다.
1. **추적 시작** 을 클릭 합니다.
1. HoloLens는 이제 추적을 기록 합니다. 조사 하려는 성능 문제를 트리거해야 합니다. 그런 다음 **추적 중지**를 클릭 합니다.
1. 추적은 웹 페이지의 맨 아래에 나열 됩니다. ETL 파일을 다운로드 하려면 오른쪽에 있는 디스크 아이콘을 클릭 합니다.

이제 WPA에서 직접 열거나 다른 사용자에 게 보낼 수 있는 ETL 파일이 있습니다.

## <a name="analyzing-traces-with-wpa"></a>WPA를 사용 하 여 추적 분석

### <a name="wpa-basics"></a>WPA 기본 사항

Windows 성능 분석기는 ETL 파일을 열고 추적을 검사 하는 표준 도구입니다. WPA 작동 방법에 대 한 설명은이 문서의 범위를 벗어났습니다. 시작 하려면 다음 리소스를 살펴보세요.

* 첫 번째 개요는 [소개 비디오](/windows-hardware/test/wpt/windows-performance-analyzer) 를 시청 하세요.
* WPA 자체에는 일반적인 단계를 설명 하는 *시작* 탭이 있습니다. 사용 가능한 항목을 살펴보세요. 특히 "데이터 보기"에서 특정 데이터에 대 한 그래프를 만드는 방법에 대 한 간략 한 소개를 볼 수 있습니다.
* [이 웹 사이트에](https://randomascii.wordpress.com/2015/09/24/etw-central/)대 한 유용한 정보가 있지만 일부는 초보자와 관련이 없습니다.

### <a name="graphing-data"></a>그래프 데이터

ARR 추적을 시작 하려면 다음 부분이 잘 알고 있어야 합니다.

![성능 그래프](./media/wpa-graph.png)

위의 이미지는 동일한 데이터의 그래프 표현과 추적 데이터의 테이블을 보여 줍니다.

아래쪽에 있는 표에서 노란색 (골든) 표시줄과 파란색 막대를 확인 합니다. 이러한 막대를 끌어 임의의 위치에 배치할 수 있습니다.

**노란색 표시줄의 왼쪽에 있는 모든 열** 은 **키**로 해석 됩니다. 키를 사용 하 여 왼쪽 위 창에서 트리를 구조화할 수 있습니다. 여기에는 "공급자 이름"과 "작업 이름" 이라는 두 개의 *키* 열이 있습니다. 따라서 왼쪽 위 창의 트리 구조는 수준 깊이가 두 수준입니다. 열의 순서를 변경 하거나 키 영역에서 열을 추가 하거나 제거 하는 경우 트리 뷰의 구조가 변경 됩니다.

**파란색 막대의 오른쪽에 있는 열** 은 오른쪽 위 창에 **표시** 되는 그래프를 표시 하는 데 사용 됩니다. 대부분의 경우 첫 번째 열만 사용 되지만 일부 그래프 모드에서는 데이터 열이 여러 개 필요 합니다. 선형 그래프가 작동 하려면 해당 열의 *집계 모드* 를 설정 해야 합니다. ' Avg ' 또는 ' Max '를 사용 합니다. 픽셀이 여러 이벤트를 포함 하는 범위를 포함 하는 경우 집계 모드는 지정 된 픽셀에서 그래프의 값을 확인 하는 데 사용 됩니다. 이는 집계를 ' 합계 '로 설정 하 고 확대/축소 하 여 관찰할 수 있습니다.

중간의 열에는 특별 한 의미가 없습니다.

![이벤트 보기](./media/wpa-event-view.png)

*일반 이벤트 보기 편집기* 에서 표시할 모든 열, 집계 모드, 정렬 및 키로 사용 되는 열, 그래프로 표시할 열을 구성할 수 있습니다. 위의 예에서는 **필드 2** 를 사용 하도록 설정 하 고 필드 3-6을 사용할 수 없습니다. 필드 2는 일반적으로 ETW 이벤트의 첫 번째 *사용자 지정 데이터* 필드 이므로 일부 네트워크 대기 시간 값을 나타내는 ARR "FrameStatistics" 이벤트의 경우입니다. 이 이벤트의 추가 값을 보려면 다른 "필드" 열을 사용 하도록 설정 합니다.

### <a name="presets"></a>기본 설정

추적을 제대로 분석 하려면 고유한 워크플로 및 기본 데이터 표시를 파악 해야 합니다. 그러나 ARR 관련 이벤트에 대 한 간략 한 개요를 얻기 위해 Windows 소프트웨어 보호 플랫폼 프로필 및 사전 설정 파일을 폴더 *도구/ETLProfiles*에 포함 합니다. 전체 프로필을 로드 하려면 WPA 메뉴 모음에서 *프로필 > 적용 ...* 을 선택 하거나 *내 기본 설정* 패널 (창에서*내 기본 설정 >*)을 열고 *가져오기*를 선택 합니다. 전자는 아래 이미지와 같이 전체 WPA 구성을 설정 합니다. 후자는 사용 가능한 다양 한 보기 구성에 대 한 기본 설정만 만들고 뷰를 빠르게 열어서 ARR 이벤트 데이터의 특정 부분을 확인할 수 있도록 합니다.

![기본 설정](./media/wpa-arr-trace.png)

위의 이미지는 다양 한 ARR 특정 이벤트와 전체 CPU 사용률의 뷰를 보여 줍니다.

## <a name="next-steps"></a>다음 단계

* [서버 쪽 성능 쿼리](../overview/features/performance-queries.md)