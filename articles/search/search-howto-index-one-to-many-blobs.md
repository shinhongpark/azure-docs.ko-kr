---
title: 여러 문서를 포함 하는 인덱스 blob
titleSuffix: Azure Cognitive Search
description: Azure Cognitive Search Blob 인덱서를 사용 하 여 Azure blob에서 텍스트 콘텐츠를 탐색 합니다. 여기서 각 blob은 하나 이상의 검색 인덱스 문서를 생성할 수 있습니다.
manager: nitinme
author: arv100kri
ms.author: arjagann
ms.devlang: rest-api
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 07/11/2020
ms.openlocfilehash: e5a69525c4bd0717c0561bc61ee3c52aa68e1c9d
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91533964"
---
# <a name="indexing-blobs-to-produce-multiple-search-documents"></a>여러 검색 문서를 생성 하는 blob 인덱싱
기본적으로 blob 인덱서는 blob의 내용을 단일 검색 문서로 처리 합니다. 특정 **parsingMode** 값은 개별 blob이 여러 검색 문서를 발생 시킬 수 있는 시나리오를 지원 합니다. 인덱서가 blob에서 둘 이상의 검색 문서를 추출할 수 있는 다양 한 유형의 **parsingMode** 는 다음과 같습니다.
+ `delimitedText`
+ `jsonArray`
+ `jsonLines`

## <a name="one-to-many-document-key"></a>일대다 문서 키
Azure Cognitive Search 인덱스에 표시 되는 각 문서는 문서 키로 고유 하 게 식별 됩니다. 

구문 분석 모드를 지정 하지 않고 인덱스의 키 필드에 대 한 명시적 매핑이 없으면 Azure Cognitive Search는 속성을 키로 자동으로 [매핑합니다](search-indexer-field-mappings.md) `metadata_storage_path` . 이 매핑은 각 blob이 고유한 검색 문서로 표시 되도록 합니다.

위에 나열 된 구문 분석 모드를 사용 하는 경우 하나의 blob이 "다" 검색 문서에 매핑되므로 blob 메타 데이터에만 적합 한 문서 키가 생성 됩니다. 이 제약 조건을 극복 하기 위해 Azure Cognitive Search는 blob에서 추출 된 각 개별 엔터티에 대해 "일 대 다" 문서 키를 생성할 수 있습니다. 이 속성은 이름이 지정 되 `AzureSearch_DocumentKey` 고 blob에서 추출 된 각 개별 엔터티에 추가 됩니다. 이 속성의 값은 _blob_ 의 개별 엔터티에 대해 고유 하 게 유지 되며 엔터티는 개별 검색 문서로 표시 됩니다.

기본적으로 키 인덱스 필드에 대 한 명시적 필드 매핑을 지정 하지 않으면 `AzureSearch_DocumentKey` 필드 매핑 함수를 사용 하 여이에 매핑됩니다 `base64Encode` .

## <a name="example"></a>예제
다음 필드를 사용 하 여 인덱스 정의가 있다고 가정 합니다.
+ `id`
+ `temperature`
+ `pressure`
+ `timestamp`

그리고 blob 컨테이너에는 다음 구조의 blob이 있습니다.

_Blob1.json_

```json
    { "temperature": 100, "pressure": 100, "timestamp": "2019-02-13T00:00:00Z" }
    { "temperature" : 33, "pressure" : 30, "timestamp": "2019-02-14T00:00:00Z" }
```

_Blob2.json_

```json
    { "temperature": 1, "pressure": 1, "timestamp": "2018-01-12T00:00:00Z" }
    { "temperature" : 120, "pressure" : 3, "timestamp": "2013-05-11T00:00:00Z" }
```

**parsingMode** `jsonLines` 키 필드에 대해 명시적 필드 매핑을 지정 하지 않고 인덱서를 만들고 parsingMode을로 설정 하면 다음 매핑이 암시적으로 적용 됩니다.

```http
    {
        "sourceFieldName" : "AzureSearch_DocumentKey",
        "targetFieldName": "id",
        "mappingFunction": { "name" : "base64Encode" }
    }
```

이 설치 프로그램은 다음 정보를 포함 하는 Azure Cognitive Search 인덱스를 생성 합니다 (간단 하 게 하기 위해 base64 인코딩 ID 단축).

| ID | 온도 | pressure | timestamp |
|----|-------------|----------|-----------|
| aHR0 ... YjEuanNvbjsx | 100 | 100 | 2019-02-13T00:00:00Z |
| aHR0 ... YjEuanNvbjsy | 33 | 30 | 2019-02-14T00:00:00Z |
| aHR0 ... YjIuanNvbjsx | 1 | 1 | 2018-01-12T00:00:00Z |
| aHR0 ... YjIuanNvbjsy | 120 | 3 | 2013-05-11T00:00:00Z |

## <a name="custom-field-mapping-for-index-key-field"></a>인덱스 키 필드에 대 한 사용자 지정 필드 매핑

이전 예제와 동일한 인덱스 정의를 가정 하 고 blob 컨테이너에 다음 구조의 blob이 있다고 가정 합니다.

_Blob1.json_

```json
    recordid, temperature, pressure, timestamp
    1, 100, 100,"2019-02-13T00:00:00Z" 
    2, 33, 30,"2019-02-14T00:00:00Z" 
```

_Blob2.json_

```json
    recordid, temperature, pressure, timestamp
    1, 1, 1,"2018-01-12T00:00:00Z" 
    2, 120, 3,"2013-05-11T00:00:00Z" 
```

ParsingMode를 사용 하 여 인덱서를 만들 때 다음과 `delimitedText` **parsingMode**같이 키 필드에 필드 매핑 함수를 설정 하는 것이 자연스럽 게 느껴질 수 있습니다.

```http
    {
        "sourceFieldName" : "recordid",
        "targetFieldName": "id"
    }
```

그러나이 매핑은 blob에서 고유 하지 않으므로 4 개의 문서가 인덱스에 표시 _되지_ 않습니다 `recordid` . _across blobs_ 따라서 속성에서 적용 된 암시적 필드 매핑을 `AzureSearch_DocumentKey` "일 대 다" 구문 분석 모드의 키 인덱스 필드에 사용 하는 것이 좋습니다.

명시적 필드 매핑을 설정 하려면 **모든 blob에서**각 개별 엔터티에 대해 _sourcefield_ 가 고유한 지 확인 합니다.

> [!NOTE]
> 추출 된 엔터티 별로 고유성이 보장 되는 방법에 따라 `AzureSearch_DocumentKey` 변경 될 수 있으므로 응용 프로그램의 요구에 따라이 값을 사용 하면 안 됩니다.

## <a name="help-us-make-azure-cognitive-search-better"></a>Azure Cognitive Search 향상에 도움을 주세요.
요청할 기능이 있거나 개선을 위한 아이디어가 있는 경우 [UserVoice](https://feedback.azure.com/forums/263029-azure-search/)에서 입력을 제공하세요. 기존 기능을 사용 하는 데 도움이 필요 하면 [Stack Overflow](https://stackoverflow.microsoft.com/questions/tagged/18870)에 질문을 게시 하세요.

## <a name="next-steps"></a>다음 단계

Blob 인덱싱의 기본 구조와 워크플로에 익숙하지 않은 경우 먼저 [Azure Cognitive Search를 사용 하 여 Azure Blob Storage 인덱싱](search-howto-index-json-blobs.md) 을 검토 해야 합니다. 다른 blob 내용 유형에 대 한 구문 분석 모드에 대 한 자세한 내용은 다음 문서를 검토 하세요.

> [!div class="nextstepaction"]
> [CSV Blob 인덱싱](search-howto-index-csv-blobs.md) 
>  [JSON Blob 인덱싱](search-howto-index-json-blobs.md)
