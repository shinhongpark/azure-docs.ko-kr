---
title: Azure 이미지 작성기 (미리 보기)를 사용 하 여 기존 이미지 버전에서 새 이미지 버전 만들기
description: Windows에서 Azure 이미지 작성기를 사용 하 여 기존 이미지 버전에서 새 VM 이미지 버전을 만듭니다.
author: cynthn
ms.author: cynthn
ms.date: 05/05/2020
ms.topic: how-to
ms.service: virtual-machines-windows
ms.openlocfilehash: 8ad463672660582f28e0fd758a2293ad4112a981
ms.sourcegitcommit: 2bd0a039be8126c969a795cea3b60ce8e4ce64fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98201878"
---
# <a name="preview-create-a-new-vm-image-version-from-an-existing-image-version-using-azure-image-builder-in-windows"></a>미리 보기: Windows에서 Azure 이미지 작성기를 사용 하 여 기존 이미지 버전에서 새 VM 이미지 버전 만들기

이 문서에서는 [공유 이미지 갤러리](shared-image-galleries.md)에서 기존 이미지 버전을 가져와서 업데이트 하 고 갤러리에 새 이미지 버전으로 게시 하는 방법을 보여 줍니다.

이미지를 구성하는 데 샘플 .json 템플릿을 사용합니다. 사용 중인. json 파일은 [helloImageTemplateforSIGfromWinSIG.js에](https://raw.githubusercontent.com/danielsollondon/azvmimagebuilder/master/quickquickstarts/2_Creating_a_Custom_Win_Shared_Image_Gallery_Image_from_SIG/helloImageTemplateforSIGfromWinSIG.json)있습니다. 

> [!IMPORTANT]
> Azure Image Builder는 현재 공개 미리 보기로 제공됩니다.
> 이 미리 보기 버전은 서비스 수준 계약 없이 제공되며 프로덕션 워크로드에는 사용하지 않는 것이 좋습니다. 특정 기능이 지원되지 않거나 기능이 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure Preview에 대한 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.

## <a name="register-the-features"></a>기능 등록
미리 보기 중에 Azure Image Builder를 사용하려면 이 새 기능을 등록해야 합니다.

```azurecli-interactive
az feature register --namespace Microsoft.VirtualMachineImages --name VirtualMachineTemplatePreview
```

기능 등록 상태를 확인합니다.

```azurecli-interactive
az feature show --namespace Microsoft.VirtualMachineImages --name VirtualMachineTemplatePreview | grep state
```

등록을 확인합니다.

```azurecli-interactive
az provider show -n Microsoft.VirtualMachineImages | grep registrationState
az provider show -n Microsoft.KeyVault | grep registrationState
az provider show -n Microsoft.Compute | grep registrationState
az provider show -n Microsoft.Storage | grep registrationState
```

등록되지 않은 경우 다음을 실행합니다.

```azurecli-interactive
az provider register -n Microsoft.VirtualMachineImages
az provider register -n Microsoft.Compute
az provider register -n Microsoft.KeyVault
az provider register -n Microsoft.Storage
```


## <a name="set-variables-and-permissions"></a>변수 및 사용 권한 설정

[이미지 만들기 및 공유 이미지 갤러리에 배포](image-builder-gallery.md) 를 사용 하 여 공유 이미지 갤러리를 만든 경우 필요한 변수를 이미 만들었습니다. 그렇지 않은 경우이 예제에 사용할 일부 변수를 설정 하세요.

미리 보기에서는 Image Builder가 원본 관리 이미지와 동일한 리소스 그룹에서 사용자 지정 이미지를 만드는 것만 지원합니다. 이 예제의 리소스 그룹 이름을 원본 관리 이미지와 동일한 리소스 그룹으로 업데이트합니다.

```azurecli-interactive
# Resource group name - we are using ibsigRG in this example
sigResourceGroup=myIBWinRG
# Datacenter location - we are using West US 2 in this example
location=westus
# Additional region to replicate the image to - we are using East US in this example
additionalregion=eastus
# name of the shared image gallery - in this example we are using myGallery
sigName=my22stSIG
# name of the image definition to be created - in this example we are using myImageDef
imageDefName=winSvrimages
# image distribution metadata reference name
runOutputName=w2019SigRo
# User name and password for the VM
username="user name for the VM"
vmpassword="password for the VM"
```

구독 ID에 대한 변수를 만듭니다. `az account show | grep id`를 사용하여 만들 수 있습니다.

```azurecli-interactive
subscriptionID=<Subscription ID>
```

업데이트 하려는 이미지 버전을 가져옵니다.

```azurecli-interactive
sigDefImgVersionId=$(az sig image-version list \
   -g $sigResourceGroup \
   --gallery-name $sigName \
   --gallery-image-definition $imageDefName \
   --subscription $subscriptionID --query [].'id' -o json | grep 0. | tr -d '"' | tr -d '[:space:]')
```

## <a name="create-a-user-assigned-identity-and-set-permissions-on-the-resource-group"></a>사용자 할당 ID 만들기 및 리소스 그룹에 대한 사용 권한 설정
이전 예제에서 사용자 id를 설정 하 고 나면 리소스 ID를 가져와야 합니다. 그런 다음 템플릿에 추가 됩니다.

```azurecli-interactive
#get identity used previously
imgBuilderId=$(az identity list -g $sigResourceGroup --query "[?contains(name, 'aibBuiUserId')].id" -o tsv)
```

사용자 고유의 공유 이미지 갤러리가 이미 있고 이전 예제를 따르지 않은 경우 리소스 그룹에 액세스할 수 있도록 이미지 작성기에 대 한 사용 권한을 할당 하 여 갤러리에 액세스할 수 있도록 해야 합니다. [이미지 만들기 및 공유 이미지 갤러리에 배포](image-builder-gallery.md) 예제의 단계를 검토 하세요.


## <a name="modify-helloimage-example"></a>HelloImage 예제 수정
에서 json 파일을 열어 사용 하려는 예제는 [이미지 작성기 템플릿 참조](../linux/image-builder-json.md)와 함께 [helloImageTemplateforSIGfromSIG.js에서](https://raw.githubusercontent.com/danielsollondon/azvmimagebuilder/master/quickquickstarts/2_Creating_a_Custom_Linux_Shared_Image_Gallery_Image_from_SIG/helloImageTemplateforSIGfromSIG.json) 검토할 수 있습니다. 


. Json 예제를 다운로드 하 고 변수로 구성 합니다. 

```azurecli-interactive
curl https://raw.githubusercontent.com/danielsollondon/azvmimagebuilder/master/quickquickstarts/8_Creating_a_Custom_Win_Shared_Image_Gallery_Image_from_SIG/helloImageTemplateforSIGfromWinSIG.json -o helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<subscriptionID>/$subscriptionID/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<rgName>/$sigResourceGroup/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<imageDefName>/$imageDefName/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<sharedImageGalName>/$sigName/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s%<sigDefImgVersionId>%$sigDefImgVersionId%g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<region1>/$location/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<region2>/$additionalregion/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s/<runOutputName>/$runOutputName/g" helloImageTemplateforSIGfromWinSIG.json
sed -i -e "s%<imgBuilderId>%$imgBuilderId%g" helloImageTemplateforSIGfromWinSIG.json
```

## <a name="create-the-image"></a>이미지 만들기

이미지 구성을 VM 이미지 빌더 서비스에 제출 합니다.

```azurecli-interactive
az resource create \
    --resource-group $sigResourceGroup \
    --properties @helloImageTemplateforSIGfromWinSIG.json \
    --is-full-object \
    --resource-type Microsoft.VirtualMachineImages/imageTemplates \
    -n imageTemplateforSIGfromWinSIG01
```

이미지 빌드를 시작합니다.

```azurecli-interactive
az resource invoke-action \
     --resource-group $sigResourceGroup \
     --resource-type  Microsoft.VirtualMachineImages/imageTemplates \
     -n imageTemplateforSIGfromWinSIG01 \
     --action Run 
```

다음 단계로 이동 하기 전에 이미지가 빌드되고 복제가 완료 될 때까지 기다립니다.


## <a name="create-the-vm"></a>VM 만들기

```azurecli-interactive
az vm create \
  --resource-group $sigResourceGroup \
  --name aibImgWinVm002 \
  --admin-username $username \
  --admin-password $vmpassword \
  --image "/subscriptions/$subscriptionID/resourceGroups/$sigResourceGroup/providers/Microsoft.Compute/galleries/$sigName/images/$imageDefName/versions/latest" \
  --location $location
```

## <a name="verify-the-customization"></a>사용자 지정 확인
VM을 만들 때 설정한 사용자 이름 및 암호를 사용하여 VM에 대한 원격 데스크톱 연결을 만듭니다. VM 내에서 cmd 프롬프트를 열고 다음을 입력합니다.

```console
dir c:\
```

이제 두 개의 디렉터리가 표시 됩니다.
- `buildActions` 첫 번째 이미지 버전에서 만든입니다.
- `buildActions2` 첫 번째 이미지 버전을 업데이트 하 여 두 번째 이미지 버전을 만드는 과정에서 생성 되었습니다.


## <a name="next-steps"></a>다음 단계

이 문서에 사용 된 json 파일의 구성 요소에 대해 자세히 알아보려면 [이미지 작성기 템플릿 참조](../linux/image-builder-json.md)를 참조 하세요.
