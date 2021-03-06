---
title: 관계를 사용하여 쌍 그래프 관리
titleSuffix: Azure Digital Twins
description: 디지털 쌍을 관계와 연결 하 여 그래프를 관리 하는 방법을 참조 하세요.
author: baanders
ms.author: baanders
ms.date: 11/03/2020
ms.topic: how-to
ms.service: digital-twins
ms.openlocfilehash: 037e7fd13f55a0f5de939197f71324221392bd55
ms.sourcegitcommit: fc401c220eaa40f6b3c8344db84b801aa9ff7185
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98601076"
---
# <a name="manage-a-graph-of-digital-twins-using-relationships"></a>관계를 사용 하 여 디지털 쌍의 그래프 관리

Azure Digital Twins의 핵심은 전체 환경을 나타내는 쌍 [그래프](concepts-twins-graph.md) 입니다. 쌍 그래프는 **관계** 를 통해 연결 되는 개별 디지털 쌍으로 구성 됩니다. 

[Azure digital 쌍 인스턴스가](how-to-set-up-instance-portal.md) 작동 하 고 클라이언트 앱에서 [인증](how-to-authenticate-client.md) 코드를 설정한 후에는 [**DigitalTwins api**](/rest/api/digital-twins/dataplane/twins) 를 사용 하 여 azure digital 쌍 인스턴스에서 디지털 쌍 및 해당 관계를 생성, 수정 및 삭제할 수 있습니다. [.Net (c #) SDK](/dotnet/api/overview/azure/digitaltwins/client?view=azure-dotnet&preserve-view=true)또는 [Azure DIGITAL twins CLI](how-to-use-cli.md)를 사용할 수도 있습니다.

이 문서에서는 관계와 그래프를 전체적으로 관리 하는 방법을 집중적으로 설명 합니다. 개별 디지털 쌍으로 작업 하려면 [*방법: 디지털 쌍 관리*](how-to-manage-twin.md)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

[!INCLUDE [digital-twins-prereq-instance.md](../../includes/digital-twins-prereq-instance.md)]

## <a name="ways-to-manage-graph"></a>그래프를 관리 하는 방법

[!INCLUDE [digital-twins-ways-to-manage.md](../../includes/digital-twins-ways-to-manage.md)]

또한 Azure Digital 쌍 (ADT) 탐색기 샘플을 사용 하 여 그래프를 변경할 수 있습니다 .이 샘플을 사용 하면 쌍과 그래프를 시각화 하 고, 백그라운드에서 SDK를 사용할 수 있습니다. 다음 섹션에서는이 샘플에 대해 자세히 설명 합니다.

[!INCLUDE [visualizing with Azure Digital Twins explorer](../../includes/digital-twins-visualization.md)]

## <a name="create-relationships"></a>관계 만들기

관계는 서로 다른 디지털 쌍이 서로 연결 되는 방법을 설명 하며,이는 쌍 그래프의 기본을 형성 합니다.

관계는 호출을 사용 하 여 생성 됩니다 `CreateOrReplaceRelationshipAsync()` . 

관계를 만들려면 다음을 지정 해야 합니다.
* 원본 쌍 ID ( `srcId` 아래 코드 샘플에서): 관계가 시작 되는 쌍의 id입니다.
* 대상 쌍 ID ( `targetId` 아래 코드 샘플에서): 관계가 도착 하는 쌍의 id입니다.
* 관계 이름 ( `relName` 아래 코드 샘플에서): 관계의 제네릭 형식 (예: _contains_)입니다.
* 관계 ID ( `relId` 아래 코드 샘플에서):이 관계에 대 한 특정 이름 (예: _Relationship1_)입니다.

관계 ID는 지정 된 원본 쌍 내에서 고유 해야 합니다. 전역적으로 고유할 필요는 없습니다.
예를 들어 쌍 *foo* 의 경우 각 특정 관계 ID는 고유 해야 합니다. 그러나 다른 쌍 *막대* 에는 동일한 *foo* 관계 ID와 일치 하는 나가는 관계가 있을 수 있습니다.

다음 코드 샘플에서는 Azure Digital Twins 인스턴스에서 관계를 만드는 방법을 보여 줍니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="CreateRelationshipMethod":::

이제 main 메서드에서 함수를 호출 `CreateRelationship()` 하 여 다음과 같이 _contains_ 관계를 만들 수 있습니다. 

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="UseCreateRelationship":::

여러 관계를 만들려는 경우에는 동일한 메서드에 대 한 호출을 반복 하 여 다른 관계 형식을 인수에 전달할 수 있습니다. 

도우미 클래스에 대 한 자세한 내용은 `BasicRelationship` [*방법: Azure Digital Twins Api 및 sdk 사용*](how-to-use-apis-sdks.md#serialization-helpers)을 참조 하세요.

### <a name="create-multiple-relationships-between-twins"></a>쌍 간에 여러 관계 만들기

관계는 다음 중 하나로 분류 될 수 있습니다. 

* 나가는 관계: 다른 쌍에 연결 하기 위해 바깥쪽을 가리키는이 쌍에 속하는 관계입니다. 메서드는 쌍 `GetRelationshipsAsync()` 의 나가는 관계를 가져오는 데 사용 됩니다.
* 들어오는 관계: "들어오는" 링크를 만들기 위해이 쌍을 가리키는 다른 쌍에 속하는 관계입니다. 메서드는 쌍 `GetIncomingRelationshipsAsync()` 의 들어오는 관계를 가져오는 데 사용 됩니다.

두 쌍 간에 가질 수 있는 관계 수에 대 한 제한은 없습니다. 즉, 사용자가 원하는 대로 쌍 간에 관계를 가질 수 있습니다. 

즉, 한 번에 두 쌍 간에 여러 유형의 관계를 표현할 수 있습니다. 예를 들어 쌍 *A는* 쌍으로 *저장* 된 관계와 *제조* 관계를 둘 다 가질 수 *있습니다.*

원하는 경우 동일한 두 쌍 사이에 동일한 관계 유형의 인스턴스를 여러 개 만들 수도 있습니다. 이 예에서는 관계가 서로 다른 관계 Id를 사용 하는 *한 쌍 a* 가 쌍 *B* 와 두 개의 다른 *저장* 관계를 가질 수 있습니다.

## <a name="list-relationships"></a>관계 목록

그래프의 지정 된 쌍에 대 한 **나가는** 관계의 목록에 액세스 하려면 다음과 같이 메서드를 사용할 수 있습니다 `GetRelationships()` .

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="GetRelationshipsCall":::

이는 `Azure.Pageable<T>` `Azure.AsyncPageable<T>` 호출의 동기 또는 비동기 버전을 사용 하는지에 따라 또는를 반환 합니다.

관계 목록을 검색 하는 예제는 다음과 같습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="FindOutgoingRelationshipsMethod":::

이제이 메서드를 호출 하 여 다음과 같이 쌍의 나가는 관계를 확인할 수 있습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="UseFindOutgoingRelationships":::

검색 된 관계를 사용 하 여 그래프의 다른 쌍으로 이동할 수 있습니다. 이렇게 하려면 `target` 반환 되는 관계에서 필드를 읽고에 대 한 다음 호출의 ID로 사용 `GetDigitalTwin()` 합니다.

### <a name="find-incoming-relationships-to-a-digital-twin"></a>디지털 쌍으로 들어오는 관계 찾기

Azure Digital Twins에는 지정 된 쌍으로 **들어오는** 모든 관계를 찾을 수 있는 API도 있습니다. 이는 역방향 탐색 이나 쌍을 삭제할 때 유용 합니다.

이전 코드 샘플은 쌍에서 나가는 관계를 찾는 데 중점을 두었습니다. 다음 예제는 유사 하 게 구성 되지만 대신 쌍으로 *들어오는* 관계를 찾습니다.

`IncomingRelationship`호출은 관계의 전체 본문을 반환 하지 않습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="FindIncomingRelationshipsMethod":::

이제이 메서드를 호출 하 여 다음과 같이 쌍의 들어오는 관계를 확인할 수 있습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="UseFindIncomingRelationships":::

### <a name="list-all-twin-properties-and-relationships"></a>모든 쌍 속성 및 관계 나열

위의 메서드를 사용 하 여 쌍으로 나가는 및 들어오는 관계를 나열 하 고 쌍의 속성 및 두 형식의 관계를 포함 하 여 전체 쌍 정보를 인쇄 하는 메서드를 만들 수 있습니다. `FetchAndPrintTwinAsync()`이 작업을 수행 하는 방법을 보여 주는 라는 예제 메서드는 다음과 같습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="FetchAndPrintMethod":::

이제 다음과 같이 main 메서드에서이 함수를 호출할 수 있습니다. 

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="UseFetchAndPrint":::

## <a name="delete-relationships"></a>관계 삭제

첫 번째 매개 변수는 원본 쌍 (관계가 시작 되는 쌍)을 지정 합니다. 다른 매개 변수는 관계 ID입니다. 관계 Id는 쌍의 범위 내 에서만 고유 하므로 쌍 ID와 관계 ID가 모두 필요 합니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="DeleteRelationshipMethod":::

이제이 메서드를 호출 하 여 다음과 같은 관계를 삭제할 수 있습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs" id="UseDeleteRelationship":::

## <a name="runnable-twin-graph-sample"></a>실행 가능한 쌍의 쌍 그래프 샘플

다음 실행 가능한 코드 조각은이 문서의 관계 작업을 사용 하 여 디지털 쌍 및 관계에서 쌍으로 된 쌍의 그래프를 만듭니다.

### <a name="set-up-the-runnable-sample"></a>실행 가능한 샘플 설정

이 코드 조각은 [*자습서: 샘플 클라이언트 앱을 사용 하 여 Azure Digital Twins 탐색*](tutorial-command-line-app.md)의 모델 정의에 [*대 한Room.js*](https://github.com/Azure-Samples/digital-twins-samples/blob/master/AdtSampleApp/SampleClientApp/Models/Room.json) 및 [*Floor.js*](https://github.com/azure-Samples/digital-twins-samples/blob/master/AdtSampleApp/SampleClientApp/Models/Floor.json) 를 사용 합니다. 이러한 링크를 사용 하 여 파일로 직접 이동 하거나 [여기](/samples/azure-samples/digital-twins-samples/digital-twins-samples/)에서 전체 종단 간 샘플 프로젝트의 일부로 다운로드할 수 있습니다. 

샘플을 실행 하기 전에 다음을 수행 합니다.
1. 모델 파일을 다운로드 하 고 프로젝트에 추가한 다음 `<path-to>` 아래 코드의 자리 표시자를 바꿔서 프로그램에서 찾을 위치를 알려 줍니다.
2. 자리 표시자를 `<your-instance-hostname>` Azure 디지털 Twins 인스턴스의 호스트 이름으로 바꿉니다.
3. Azure Digital Twins를 사용 하는 데 필요한 두 개의 종속성을 프로젝트에 추가 합니다. 첫 번째는 [Azure Digital Twins SDK for .net](/dotnet/api/overview/azure/digitaltwins/client?view=azure-dotnet&preserve-view=true)에 대 한 패키지이 고, 두 번째는 azure에 대 한 인증을 돕는 도구를 제공 합니다.

      ```cmd/sh
      dotnet add package Azure.DigitalTwins.Core
      dotnet add package Azure.Identity
      ```

또한 샘플을 직접 실행 하려면 로컬 자격 증명을 설정 해야 합니다. 다음 섹션에서는이 과정을 안내 합니다.
[!INCLUDE [Azure Digital Twins: local credentials prereq (outer)](../../includes/digital-twins-local-credentials-outer.md)]

### <a name="run-the-sample"></a>샘플 실행

위의 단계를 완료 한 후에는 다음 샘플 코드를 직접 실행할 수 있습니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graph_operations_sample.cs":::

위의 프로그램의 콘솔 출력은 다음과 같습니다. 

:::image type="content" source="./media/how-to-manage-graph/console-output-twin-graph.png" alt-text="쌍 세부 정보, 쌍의 들어오고 나가는 관계를 보여 주는 콘솔 출력입니다." lightbox="./media/how-to-manage-graph/console-output-twin-graph.png":::

> [!TIP]
> 쌍 그래프는 twins 간의 관계를 만드는 개념입니다. 쌍 그래프의 시각적 표시를 보려는 경우이 문서의 [*시각화*](how-to-manage-graph.md#visualization) 섹션을 참조 하세요. 

## <a name="create-graph-from-a-csv-file"></a>CSV 파일에서 그래프 만들기

실제로 사용 하는 경우에는 다른 데이터베이스에 저장 된 데이터 또는 스프레드시트나 CSV 파일에서 쌍 계층 구조가 생성 되는 경우가 많습니다. 이 섹션에서는 CSV 파일에서 데이터를 읽고 그 밖의 쌍을 만드는 방법을 보여 줍니다.

디지털 쌍 및 관계의 집합을 설명 하는 다음 데이터 표를 참조 하세요.

|  모델 ID    | 쌍 ID (고유 해야 함) | 관계 이름  | 대상 쌍 ID  | 쌍 초기화 데이터 |
| --- | --- | --- | --- | --- |
| dtmi: 예: 밑면; 1    | Floor1 | contains | Room1 | |
| dtmi: 예: 밑면; 1    | Floor0 | contains | Room0 | |
| dtmi: 예: Room; 1    | Room1 | | | {"온도": 80} |
| dtmi: 예: Room; 1    | Room0 | | | {"온도": 70} |

Azure Digital 쌍로이 데이터를 가져오는 한 가지 방법은 테이블을 CSV 파일로 변환 하 고 파일을 명령으로 해석 하는 코드를 작성 하 여 쌍와 관계를 만드는 것입니다. 다음 코드 샘플은 CSV 파일에서 데이터를 읽고 Azure Digital Twins에서 쌍 그래프를 만드는 방법을 보여 줍니다.

아래 코드에서는 CSV 파일을 *data.csv* 라고 하며, Azure Digital twins 인스턴스의 **호스트 이름을** 나타내는 자리 표시 자가 있습니다. 또한이 샘플에서는이 프로세스를 지원 하기 위해 프로젝트에 추가할 수 있는 여러 패키지를 사용 합니다.

:::code language="csharp" source="~/digital-twins-docs-samples/sdks/csharp/graphFromCSV.cs":::

## <a name="next-steps"></a>다음 단계

Azure Digital Twins 쌍 그래프를 쿼리 하는 방법에 대해 알아봅니다.
* [*개념: 쿼리 언어*](concepts-query-language.md)
* [*방법: 쌍 그래프 쿼리*](how-to-query-graph.md)