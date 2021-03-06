---
title: 작업 및 태스크 오류 확인
description: 작업 및 태스크를 확인 하 고 해결 하는 방법에 대해 알아봅니다.
author: mscurrell
ms.topic: how-to
ms.date: 11/23/2020
ms.author: markscu
ms.openlocfilehash: d8cf3b5e28d4455e00e0bdcbae2063771d3e8acd
ms.sourcegitcommit: 1bf144dc5d7c496c4abeb95fc2f473cfa0bbed43
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95736802"
---
# <a name="job-and-task-error-checking"></a>작업 및 태스크 오류 검사

작업 및 태스크를 추가할 때 발생할 수 있는 다양한 오류가 있습니다. 이러한 작업에서는 오류를 쉽게 검색할 수 있습니다. API, CLI 또는 UI에서 오류가 즉시 반환되기 때문입니다. 그러나 나중에 작업과 태스크가 예약 되 고 실행 되는 경우에도 오류가 발생할 수 있습니다.

이 문서에서는 작업과 태스크가 제출 된 후에 발생할 수 있는 오류와이를 확인 하 고 처리 하는 방법을 설명 합니다.

## <a name="jobs"></a>작업

작업은 실행 되는 명령줄을 실제로 지정 하는 태스크를 포함 하는 하나 이상의 태스크를 그룹화 한 것입니다.

작업을 추가하는 경우 작업이 실패할 수 있는 방법에 영향을 줄 수 있는 다음 매개 변수를 지정할 수 있습니다.

- [작업 제약 조건](/rest/api/batchservice/job/add#jobconstraints)
  - 선택적으로 `maxWallClockTime` 속성을 지정하여 작업을 활성화하거나 실행할 수 있는 최대 시간을 설정할 수 있습니다. 이를 초과하면 작업에 대한 [executionInfo](/rest/api/batchservice/job/get#cloudjob)에 설정된 `terminateReason` 속성과 함께 작업이 종료됩니다.
- [작업 준비 태스크](/rest/api/batchservice/job/add#jobpreparationtask)
  - 지정된 경우 작업 준비 태스크는 노드의 작업에 대해 작업을 처음 실행할 때 실행됩니다. 작업 준비 태스크가 실패할 수 있으며 이로 인해 태스크가 실행되지 않고 작업이 완료되지 않습니다.
- [작업 릴리스 태스크](/rest/api/batchservice/job/add#jobreleasetask)
  - 작업 준비 태스크가 구성된 경우에만 작업 릴리스 태스크를 지정할 수 있습니다. 작업이 종료되면 작업 준비 태스크가 실행된 각 풀 노드에서 작업 릴리스 태스크가 실행됩니다. 작업 릴리스 태스크가 실패할 수 있지만 작업은 여전히 `completed` 상태로 전환됩니다.

### <a name="job-properties"></a>작업 속성

다음 작업 속성에 오류가 있는지 확인해야 합니다.

- '[executionInfo](/rest/api/batchservice/job/get#jobexecutioninformation)':
  - `terminateReason` 속성은 작업 제약 조건에 지정된 `maxWallClockTime`이 초과하여 작업이 종료되었음을 나타내는 값을 가질 수 있습니다. 작업 `onTaskFailure` 속성이 적절하게 설정된 경우 태스크가 실패했음을 나타내도록 설정할 수도 있습니다.
  - [schedulingError](/rest/api/batchservice/job/get#jobschedulingerror) 속성은 예약 오류가 발생한 경우에 설정됩니다.

### <a name="job-preparation-tasks"></a>작업 준비 태스크

작업에 대해 작업 준비 태스크가 지정된 경우 해당 작업의 태스크가 한 노드에서 처음으로 실행될 때 해당 태스크의 인스턴스가 실행됩니다. 작업에 대해 구성된 작업 준비 태스크는 풀의 노드 수까지 실행되는 여러 작업 준비 태스크 인스턴스와 함께 태스크 템플릿으로 간주할 수 있습니다.

오류가 있는지 확인하려면 작업 준비 태스크 인스턴스를 확인해야 합니다.

- 작업 준비 태스크를 실행하는 경우 작업 준비 태스크를 트리거한 태스크는 `preparing`의 [상태](/rest/api/batchservice/task/get#taskstate)로 이동됩니다. 작업 준비 태스크가 실패하면 트리거 태스크가 `active` 상태로 되돌아가고 실행되지 않습니다.
- 실행된 작업 준비 태스크의 모든 인스턴스는 [목록 준비 및 릴리스 태스크 상태](/rest/api/batchservice/job/listpreparationandreleasetaskstatus) API를 사용하여 작업에서 가져올 수 있습니다. 모든 태스크와 마찬가지로 `failureInfo`, `exitCode`, `result` 등의 속성과 함께 사용 가능한 [실행 정보](/rest/api/batchservice/job/listpreparationandreleasetaskstatus#jobpreparationandreleasetaskexecutioninformation)가 있습니다.
- 작업 준비 태스크가 실패하는 경우 트리거 작업 태스크가 실행되지 않으며 작업이 완료되지 않고 중지됩니다. 예약할 수 있는 태스크가 있는 다른 작업이 없는 경우 풀이 사용되지 않을 수 있습니다.

### <a name="job-release-tasks"></a>작업 릴리스 태스크

작업에 대해 작업 해제 태스크가 지정 된 경우 작업이 종료 될 때 작업 준비 태스크가 실행 된 각 풀 노드에서 작업 해제 태스크의 인스턴스가 실행 됩니다. 오류가 있는지 확인하려면 작업 릴리스 태스크 인스턴스를 확인해야 합니다.

- 실행 중인 작업 릴리스 태스크의 모든 인스턴스는 [목록 준비 및 릴리스 태스크 상태](/rest/api/batchservice/job/listpreparationandreleasetaskstatus) API를 사용하여 작업에서 가져올 수 있습니다. 모든 태스크와 마찬가지로 `failureInfo`, `exitCode`, `result` 등의 속성과 함께 사용 가능한 [실행 정보](/rest/api/batchservice/job/listpreparationandreleasetaskstatus#jobpreparationandreleasetaskexecutioninformation)가 있습니다.
- 하나 이상의 작업 릴리스 태스크가 실패한 경우에도 작업이 종료되고 `completed` 상태로 전환됩니다.

## <a name="tasks"></a>작업

여러 가지 이유로 작업 태스크가 실패할 수 있습니다.

- 태스크 명령줄이 실패하고 0이 아닌 종료 코드를 반환합니다.
- `resourceFiles`작업에 대해가 지정 되었지만 하나 이상의 파일을 다운로드 하지 못한 오류가 발생 했습니다.
- `outputFiles`태스크에 대해가 지정 되었지만 하나 이상의 파일을 업로드 하지 못한 오류가 발생 했습니다.
- 태스크 [제약 조건](/rest/api/batchservice/task/add#taskconstraints)에서 `maxWallClockTime` 속성으로 지정된 태스크에 대해 경과된 시간을 초과했습니다.

모든 경우에서 오류 및 오류에 대한 정보를 확인하려면 다음 속성을 확인해야 합니다.

- 태스크 [executionInfo](/rest/api/batchservice/task/get#taskexecutioninformation) 속성에는 오류에 대한 정보를 제공하는 여러 속성이 포함되어 있습니다. [결과](/rest/api/batchservice/task/get#taskexecutionresult)는 태스크가 `exitCode` 및 `failureInfo`와 함께 어떤 이유로 실패했는지 여부를 나타내어 오류에 대한 자세한 정보를 제공합니다.
- 태스크는 성공 또는 실패 여부에 관계 없이 항상 `completed` [상태](/rest/api/batchservice/task/get#taskstate)로 이동됩니다.

작업에 대한 태스크 실패의 영향과 태스크 종속성을 고려해야 합니다. 종속성 및 작업에 대한 동작을 구성하는 태스크에 대해 [exitConditions](/rest/api/batchservice/task/add#exitconditions) 속성을 지정할 수 있습니다.

- 종속성의 경우 [DependencyAction](/rest/api/batchservice/task/add#dependencyaction)은 실패한 태스크에 종속된 태스크가 차단되는지 아니면 실행되는지를 제어합니다.
- 작업의 경우 [JobAction](/rest/api/batchservice/task/add#jobaction)은 실패한 태스크에서 작업을 사용하지 않도록 설정하거나, 종료하거나, 그대로 유지할지 여부를 제어합니다.

### <a name="task-command-line-failures"></a>태스크 명령줄 오류

태스크 명령줄이 실행되면 출력은 `stderr.txt` 및 `stdout.txt`에 기록됩니다. 또한 애플리케이션에서 애플리케이션 관련 로그 파일에 쓸 수 있습니다.

태스크가 실행된 풀 노드가 여전히 있는 경우 로그 파일을 가져와 볼 수 있습니다. 예를 들어 Azure Portal은 태스크 또는 풀 노드에 대한 로그 파일을 나열하고 볼 수 있습니다. 여러 API를 사용하여 [태스크에서 가져오기](/rest/api/batchservice/file/getfromtask)와 같은 태스크 파일을 나열하고 가져올 수 있습니다.

풀 및 풀 노드는 자주 삭제 되 고 노드를 계속 추가 하 고 삭제 하므로 로그 파일을 저장 하는 것이 좋습니다. [태스크 출력 파일](./batch-task-output-files.md)은 로그 파일을 Azure Storage에 저장하는 편리한 방법입니다.

계산 노드의 태스크에 의해 실행 되는 명령줄은 셸에서 실행 되지 않으므로 기본적으로 환경 변수 확장과 같은 셸 기능을 활용할 수 없습니다. 이러한 기능을 활용 하려면 [명령줄에서 셸을 호출](batch-compute-node-environment-variables.md#command-line-expansion-of-environment-variables)해야 합니다.

### <a name="output-file-failures"></a>출력 파일 오류

모든 파일 업로드에서 Batch는 두 개의 로그 파일을 `fileuploadout.txt` 및 `fileuploaderr.txt` 컴퓨팅 노드에 씁니다. 이러한 로그 파일을 검사하여 특정 오류에 대해 자세히 확인할 수 있습니다. 예를 들어 태스크 자체가 실행되지 않아 파일 업로드를 시도할 수 없는 경우에는 이러한 로그 파일이 존재하지 않습니다.  

## <a name="next-steps"></a>다음 단계

- 애플리케이션에서 포괄적인 오류 검사를 구현하는지 확인합니다. 즉시 문제를 검색하고 진단하는 것이 중요할 수 있습니다.
- [작업 및 태스크](jobs-and-tasks.md)에 대해 자세히 알아보세요.