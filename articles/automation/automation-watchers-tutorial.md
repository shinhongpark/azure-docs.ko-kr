---
title: Azure Automation 감시자 태스크로 업데이트된 파일 추적
description: 이 문서에서는 폴더에 생성된 새 파일을 감시하도록 Azure Automation 계정에 감시자 태스크를 만드는 방법을 알아봅니다.
services: automation
ms.subservice: process-automation
ms.topic: conceptual
ms.date: 12/17/2020
ms.openlocfilehash: ca4c4013e0044811a5bac8786996761b8a5c45f1
ms.sourcegitcommit: e0ec3c06206ebd79195d12009fd21349de4a995d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97682751"
---
# <a name="track-updated-files-with-a-watcher-task"></a>감시자 태스크를 사용하여 업데이트된 파일 추적

Azure Automation은 감시자 태스크를 사용하여 이벤트를 찾고 PowerShell Runbook을 사용하여 작업을 트리거합니다. 감시자 태스크에는 감시자 및 작업의 두 부분이 포함됩니다. 감시자 Runbook은 감시자 태스크에 정의된 간격으로 실행되며 작업 Runbook에 데이터를 출력합니다.

> [!NOTE]
> 감시자 태스크는 Azure 중국 Vianet 21에서 지원되지 않습니다.

> [!IMPORTANT]
> 2020 년 5 월부터 Azure Logic Apps 사용 하 여 이벤트를 모니터링 하 고, 되풀이 작업을 예약 하 고, 작업을 트리거할 수 있는 권장 되는 방법입니다. [Azure Logic Apps를 사용하여 반복적인 자동화 태스크, 프로세스 및 워크플로 예약 및 실행](../logic-apps/concepts-schedule-automated-recurring-tasks-workflows.md)을 참조하세요.

이 문서에서는 새 파일이 디렉터리에 추가 되는 시기를 모니터링 하는 감시자 작업을 만드는 과정을 안내 합니다. 다음 방법을 알아봅니다.

* 감시자 Runbook 가져오기
* Automation 변수 만들기
* 작업 Runbook 만들기
* 감시자 태스크 만들기
* 감시자 트리거
* 출력 검사

## <a name="prerequisites"></a>사전 요구 사항

이 문서를 완료 하려면 다음이 필요 합니다.

* 동작합니다. 구독이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 등록할 수 있습니다.
* 감시자 및 작업 Runbook과 감시자 태스크를 포함하는 [Automation 계정](./index.yml)
* 감시자 작업이 실행되는 [하이브리드 Runbook 작업자](automation-hybrid-runbook-worker.md)
* PowerShell runbooks PowerShell 워크플로 Runbook은 감시자 태스크에서 지원되지 않습니다.

## <a name="import-a-watcher-runbook"></a>감시자 Runbook 가져오기

이 문서에서는 **조사식-NewFile** 이라는 감시자 runbook을 사용 하 여 디렉터리에서 새 파일을 찾습니다. 감시자 Runbook은 폴더의 파일에 마지막으로 쓴 것으로 알려진 시간을 검색하고 해당 워터마크보다 최근 버전의 파일을 찾습니다.

[Azure Automation GitHub 조직](https://github.com/azureautomation)에서 runbook을 다운로드할 수 있습니다.

1. [Watch-NewFile.ps1](https://github.com/azureautomation/watcher-action-that-processes-events-triggerd-by-a-watcher-runbook)에 대 한 Azure Automation GitHub 조직 페이지로 이동 합니다.
2. GitHub에서 runbook을 다운로드 하려면 페이지 오른쪽에서 **코드** 를 선택 하 고 **zip 다운로드** 를 선택 하 여 전체 코드를 zip 파일로 다운로드 합니다.
3. 콘텐츠를 추출 하 고 [runbook을 가져옵니다](manage-runbooks.md#import-a-runbook-from-the-azure-portal).

다음 단계를 사용 하 여 포털에서이 runbook을 Automation 계정으로 가져올 수도 있습니다.

1. Automation 계정을 열고 Runbook 페이지를 클릭합니다.
2. **갤러리 찾아보기** 를 클릭 하 고 **원본** 드롭다운 목록에서 **GitHub** 를 선택 합니다.
3. **감시자 Runbook** 을 검색하고 **디렉터리에서 새 파일을 찾는 감시자 Runbook** 을 선택한 후 **가져오기** 를 클릭합니다.
4. Runbook 이름과 설명을 입력하고 **확인** 을 클릭하여 Runbook을 Automation 계정으로 가져옵니다.
5. **편집** 을 선택하고 **게시** 를 클릭합니다. 메시지가 표시되면 **예** 를 클릭하여 Runbook을 게시합니다.

## <a name="create-an-automation-variable"></a>Automation 변수 만들기

[Automation 변수](./shared-resources/variables.md) 는 이전 runbook이 각 파일에서 읽고 저장 하는 타임 스탬프를 저장 하는 데 사용 됩니다.

1. **공유 리소스** 아래에서 **변수** 를 선택하고 **+ 변수 추가** 를 클릭합니다.
1. 이름에 대해 **Watch-NewFileTimestamp** 를 입력 합니다.
1. 형식에서 날짜/시간을 선택합니다.
1. **만들기** 를 클릭하여 Automation 변수를 만듭니다.

## <a name="create-an-action-runbook"></a>작업 Runbook 만들기

작업 Runbook은 감시자 Runbook에서 전달된 데이터에 대한 작업을 수행하기 위해 감시자 태스크에서 사용됩니다. [Azure Automation GitHub 조직](https://github.com/azureautomation)에서 **프로세스-NewFile** 이라는 미리 정의 된 작업 runbook을 가져와야 합니다.

작업 Runbook을 만들려면 다음을 수행합니다.

1. [Process-NewFile.ps1](https://github.com/azureautomation/watcher-action-that-processes-events-triggerd-by-a-watcher-runbook)에 대 한 Azure Automation GitHub 조직 페이지로 이동 합니다.
2. GitHub에서 runbook을 다운로드 하려면 페이지 오른쪽에서 **코드** 를 선택 하 고 **zip 다운로드** 를 선택 하 여 전체 코드를 zip 파일로 다운로드 합니다.
3. 콘텐츠를 추출 하 고 [runbook을 가져옵니다](manage-runbooks.md#import-a-runbook-from-the-azure-portal).

Azure Portal에서 이 Runbook을 Automation 계정으로 가져올 수도 있습니다.

1. Automation 계정으로 이동하여 **프로세스 자동화** 아래에서 **Runbook** 을 선택합니다.
1. **갤러리 찾아보기** 를 클릭 하 고 **원본** 드롭다운 목록에서 **GitHub** 를 선택 합니다.
1. **감시자 작업** 을 검색한 후 **감시자 Runbook에 의해 트리거되는 이벤트를 처리하는 감시자 작업** 을 선택하고 **가져오기** 를 클릭합니다.
1. Runbook 이름과 설명을 입력하고 **확인** 을 클릭하여 Runbook을 Automation 계정으로 가져옵니다.
1. **편집** 을 선택하고 **게시** 를 클릭합니다. 메시지가 표시되면 **예** 를 클릭하여 Runbook을 게시합니다.

## <a name="create-a-watcher-task"></a>감시자 태스크 만들기

이 단계에서는 이전 섹션에서 정의한 감시자 및 작업 Runbook을 참조하는 감시자 태스크를 구성합니다.

1. Automation 계정으로 이동하여 **프로세스 자동화** 아래에서 **감시자 태스크** 를 선택합니다.
1. 감시자 태스크 페이지를 선택하고 **+ 감시자 태스크 추가** 를 클릭합니다.
1. 이름으로 **WatchMyFolder** 를 입력합니다.

1. **감시자 구성**, **Watch-NewFile** Runbook을 차례로 선택합니다.

1. 매개 변수에 대해 다음 값을 입력합니다.

   * **FOLDERPATH** - 새 파일을 만들 Hybrid Runbook Worker의 폴더입니다(예: **d:\examplefiles**).
   * **EXTENSION** - 구성의 확장명입니다. 모든 파일 확장명을 처리하려면 비워 둡니다.
   * **RECURSE** - 재귀 작업입니다. 이 값은 기본값으로 유지합니다.
   * **RUN SETTINGS** - Runbook을 실행하기 위한 설정입니다. 하이브리드 작업자를 선택합니다.

1. **확인**, **선택** 을 차례로 클릭하여 감시자 페이지로 돌아갑니다.
1. **작업 구성** 을 선택하고 **Process-NewFile** Runbook을 선택합니다.
1. 매개 변수에 대해 다음 값을 입력합니다.

   * **EVENTDATA** - 이벤트 데이터입니다. 비워 둡니다. 데이터는 감시자 Runbook에서 제공됩니다.
   * **Run Settings** - Runbook을 실행하기 위한 설정입니다. 이 Runbook이 Azure Automation에서 실행되므로 Azure로 유지합니다.

1. **확인**, **선택** 을 차례로 클릭하여 감시자 페이지로 돌아갑니다.
1. **확인** 을 클릭하여 감시자 태스크를 만듭니다.

    ![UI에서 감시자 작업 구성](media/automation-watchers-tutorial/watchertaskcreation.png)

## <a name="trigger-a-watcher"></a>감시자 트리거

감시자 태스크가 제대로 작동하도록 아래에 설명된 대로 테스트를 실행해야 합니다. 

1. Hybrid Runbook Worker에 원격으로 연결합니다.
2. **PowerShell** 을 열고 폴더에 테스트 파일을 만듭니다.

```azurepowerShell-interactive
New-Item -Name ExampleFile1.txt
```

다음 예제에는 테스트가 정상적으로 완료된 경우의 결과가 나와 있습니다.

```output
    Directory: D:\examplefiles


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       12/11/2017   9:05 PM              0 ExampleFile1.txt
```

## <a name="inspect-the-output"></a>출력 검사

1. Automation 계정으로 이동하여 **프로세스 자동화** 아래에서 **감시자 태스크** 를 선택합니다.
1. 감시자 태스크 **WatchMyFolder** 를 선택합니다.
1. **스트림** 아래에서 **감시자 스트림 보기** 를 클릭하여 감시자가 새 파일을 찾았으며 작업 Runbook을 시작했음을 확인합니다.
1. 작업 Runbook 작업을 확인하려면 **감시자 작업 보기** 를 클릭합니다. 각 작업을 선택하면 작업 세부 정보를 확인할 수 있습니다.

   ![UI의 감시자 작업](media/automation-watchers-tutorial/WatcherActionJobs.png)

다음 예에는 새 파일을 찾은 경우 표시되는 출력이 나와 있습니다.

```output
Message is Process new file...

Passed in data is @{FileName=D:\examplefiles\ExampleFile1.txt; Length=0}
```

## <a name="next-steps"></a>다음 단계

Runbook을 직접 작성 하는 방법에 대 한 자세한 내용은 [PowerShell Runbook 만들기](learn/automation-tutorial-runbook-textual-powershell.md)를 참조 하세요.
