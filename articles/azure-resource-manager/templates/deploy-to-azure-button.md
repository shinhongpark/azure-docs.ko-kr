---
title: Azure 단추에 배포
description: GitHub 리포지토리에서 Azure Resource Manager 템플릿을 배포 하려면 단추를 사용 합니다.
ms.topic: conceptual
ms.date: 11/10/2020
ms.openlocfilehash: abe59f377474540e9209691df8b1d1a7b806c26d
ms.sourcegitcommit: e46f9981626751f129926a2dae327a729228216e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98028746"
---
# <a name="use-a-deployment-button-to-deploy-templates-from-github-repository"></a>배포 단추를 사용 하 여 GitHub 리포지토리에서 템플릿 배포

이 문서에서는 **Azure에 배포** 단추를 사용 하 여 GitHub 리포지토리에서 템플릿을 배포 하는 방법을 설명 합니다. GitHub 리포지토리의 _README.md_ 파일에 직접 단추를 추가할 수 있습니다. 또는 리포지토리를 참조 하는 웹 페이지에 단추를 추가할 수 있습니다.

배포 범위는 템플릿 스키마에 의해 결정 됩니다. 자세한 내용은 다음을 참조하십시오.

- [리소스 그룹](deploy-to-resource-group.md)
- [등에](deploy-to-subscription.md)
- [관리 그룹](deploy-to-management-group.md)
- [테 넌 트](deploy-to-tenant.md)

## <a name="use-common-image"></a>공통 이미지 사용

웹 페이지 또는 리포지토리에 단추를 추가 하려면 다음 이미지를 사용 합니다.

```markdown
![Deploy to Azure](https://aka.ms/deploytoazurebutton)
```

```html
<img src="https://aka.ms/deploytoazurebutton"/>
```

이미지는 다음과 같이 표시 됩니다.

![Azure 단추에 배포](https://aka.ms/deploytoazurebutton)

## <a name="create-url-for-deploying-template"></a>템플릿을 배포 하기 위한 URL 만들기

템플릿에 대 한 URL을 만들려면 리포지토리의 템플릿에 대 한 원시 URL로 시작 합니다. 원시 URL을 보려면 **raw** 를 선택 합니다.

:::image type="content" source="./media/deploy-to-azure-button/select-raw.png" alt-text="원시 선택":::

URL 형식은 다음과 같습니다.

```html
https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```

그런 다음 url을 URL로 인코딩된 값으로 변환 합니다. 온라인 인코더를 사용 하거나 명령을 실행할 수 있습니다. 다음 PowerShell 예제에서는 값을 URL로 인코딩하는 방법을 보여 줍니다.

```powershell
$url = "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json"
[uri]::EscapeDataString($url)
```

URL을 인코딩할 때 예제 URL의 값은 다음과 같습니다.

```html
https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-storage-account-create%2Fazuredeploy.json
```

각 링크는 동일한 기준 URL로 시작 합니다.

```html
https://portal.azure.com/#create/Microsoft.Template/uri/
```

URL로 인코딩된 템플릿 링크를 기본 URL의 끝에 추가 합니다.

```html
https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-storage-account-create%2Fazuredeploy.json
```

링크에 대 한 전체 URL이 있습니다.

일반적으로 공용 리포지토리에서 템플릿을 호스팅합니다. 개인 리포지토리를 사용 하는 경우 템플릿의 원시 콘텐츠를 액세스 하는 토큰을 포함 해야 합니다. GitHub에 의해 생성 된 토큰은 짧은 시간 동안만 유효 합니다. 링크를 자주 업데이트 해야 합니다.

GitHub 리포지토리 대신 [Azure Repos에서 Git](/azure/devops/repos/git/) 를 사용 하는 경우 **Azure에 배포** 단추를 계속 사용할 수 있습니다. 리포지토리가 공용 인지 확인 합니다. [항목 작업](/rest/api/azure/devops/git/items/get) 을 사용 하 여 템플릿을 가져옵니다. 요청은 다음 형식 이어야 합니다.

```http
https://dev.azure.com/{organization-name}/{project-name}/_apis/git/repositories/{repository-name}/items?scopePath={url-encoded-path}&api-version=6.0
```

이 요청 URL을 인코딩합니다.

## <a name="create-deploy-to-azure-button"></a>Azure에 배포 단추 만들기

마지막으로 링크와 이미지를 함께 배치 합니다.

GitHub 리포지토리 또는 웹 페이지의 _README.md_ 파일에서 Markdown를 사용 하 여 단추를 추가 하려면 다음을 사용 합니다.

```markdown
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-storage-account-create%2Fazuredeploy.json)
```

HTML의 경우 다음을 사용 합니다.

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-storage-account-create%2Fazuredeploy.json" target="_blank">
  <img src="https://aka.ms/deploytoazurebutton"/>
</a>
```

Azure 리포지토리를 사용 하는 Git의 경우 단추는 다음과 같은 형식입니다.

```markdown
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fdev.azure.com%2Forgname%2Fprojectname%2F_apis%2Fgit%2Frepositories%2Freponame%2Fitems%3FscopePath%3D%2freponame%2fazuredeploy.json%26api-version%3D6.0)
```

## <a name="deploy-the-template"></a>템플릿 배포

전체 솔루션을 테스트 하려면 다음 단추를 선택 합니다.

[![Azure에 배포](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-storage-account-create%2Fazuredeploy.json)

포털에는 매개 변수 값을 쉽게 제공할 수 있는 창이 표시 됩니다. 매개 변수는 템플릿의 기본값으로 미리 채워져 있습니다.

![포털을 사용 하 여 배포](./media/deploy-to-azure-button/portal.png)

## <a name="next-steps"></a>다음 단계

- 템플릿에 대한 자세한 내용은 [ARM 템플릿의 구조 및 구문 이해](template-syntax.md)를 참조하세요.
