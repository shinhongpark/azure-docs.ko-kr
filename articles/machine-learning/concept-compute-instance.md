---
title: Azure Machine Learning 컴퓨팅 인스턴스란?
titleSuffix: Azure Machine Learning
description: 완전 관리형 클라우드 기반 워크스테이션인 Azure Machine Learning 컴퓨팅 인스턴스에 대해 알아봅니다.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.author: sgilley
author: sdgilley
ms.date: 10/02/2020
ms.openlocfilehash: 54da62ce961156b64c917b448557c17e7516e222
ms.sourcegitcommit: aeba98c7b85ad435b631d40cbe1f9419727d5884
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2021
ms.locfileid: "97862140"
---
# <a name="what-is-an-azure-machine-learning-compute-instance"></a>Azure Machine Learning 컴퓨팅 인스턴스란?

Azure Machine Learning 계산 인스턴스는 데이터 과학자을 위한 관리 되는 클라우드 기반 워크스테이션입니다.

컴퓨팅 인스턴스를 사용하면 Azure Machine Learning 개발을 손쉽게 시작할 수 있을 뿐만 아니라 IT 관리자에게 관리 및 엔터프라이즈 준비 기능을 제공할 수 있습니다.  

기계 학습을 위해 클라우드에서 완전히 구성 되 고 관리 되는 개발 환경으로 계산 인스턴스를 사용 합니다. 개발 및 테스트 목적으로 학습 및 추론 계산 대상으로 사용할 수도 있습니다.  

프로덕션 등급 모델 학습의 경우 다중 노드 크기 조정 기능이 포함 된 [Azure Machine Learning 계산 클러스터](how-to-create-attach-compute-cluster.md) 를 사용 합니다. 프로덕션 등급 모델 배포의 경우 [Azure Kubernetes Service 클러스터](how-to-deploy-azure-kubernetes-service.md)를 사용 합니다.

컴퓨팅 인스턴스 Jupyter 기능이 작동하려면 웹 소켓 통신이 비활성화되어 있지 않아야 합니다. 네트워크에서 *. instances.azureml.net 및 *. instances.azureml.ms에 대 한 websocket 연결을 허용 하는지 확인 하세요.

## <a name="why-use-a-compute-instance"></a>컴퓨팅 인스턴스를 사용하는 이유

계산 인스턴스는 machine learning 개발 환경에 최적화 된 완전히 관리 되는 클라우드 기반 워크스테이션입니다. 다음과 같은 이점을 제공합니다.

|주요 이점|설명|
|----|----|
|생산성|Azure Machine Learning studio에서 통합 된 노트북 및 다음 도구를 사용 하 여 모델을 빌드 및 배포할 수 있습니다.<br/>-  Jupyter<br/>-  JupyterLab<br/>-RStudio (미리 보기)<br/>계산 인스턴스는 Azure Machine Learning 작업 영역 및 스튜디오와 완전히 통합 됩니다. 작업 영역의 다른 데이터 과학자와 전자 필기장 및 데이터를 공유할 수 있습니다.<br/> 계산 인스턴스와 [VS Code](https://techcommunity.microsoft.com/t5/azure-ai/power-your-vs-code-notebooks-with-azml-compute-instances/ba-p/1629630) 를 사용할 수도 있습니다.
|관리 및 보안|보안 공간을 줄이고 엔터프라이즈 보안 요구 사항에 따라 규정 준수를 추가합니다. 컴퓨팅 인스턴스는 다음과 같은 강력한 관리 정책과 보안 네트워킹 구성을 제공합니다.<br/><br/>-리소스 관리자 템플릿 또는 Azure Machine Learning SDK에서 autoprovisioning 비전<br/>- [Azure 역할 기반 access control (Azure RBAC)](../role-based-access-control/overview.md)<br/>- [가상 네트워크 지원](./how-to-secure-training-vnet.md#compute-instance)<br/>- SSH 액세스를 사용하거나 사용하지 않도록 설정하는 SSH 정책<br/>TLS 1.2 사용 |
|&nbsp;ML 용으로 미리 구성 된 &nbsp;|사전 구성된 최신 ML 패키지, 딥 러닝 프레임워크 및 GPU 드라이버를 통해 설치 작업에 드는 시간을 절약할 수 있습니다.|
|완전한 사용자 지정 기능|GPU를 비롯한 Azure VM 형식에 대한 광범위한 지원과 패키지 및 드라이버 설치와 같은 지속형의 하위 수준 사용자 지정을 통해 고급 시나리오를 간편하게 만들 수 있습니다. |

[계산 인스턴스](how-to-create-manage-compute-instance.md?tabs=python#create) 를 직접 만들 수도 있고 관리자가 [계산 인스턴스를 만들](how-to-create-manage-compute-instance.md?tabs=python#create-on-behalf-of-preview)수도 있습니다.

## <a name="tools-and-environments"></a><a name="contents"></a>도구 및 환경

> [!IMPORTANT]
> 이 문서에서 (미리 보기)로 표시 된 항목은 현재 공개 미리 보기로 제공 됩니다.
> 미리 보기 버전은 서비스 수준 계약 없이 제공되며 프로덕션 워크로드에는 권장되지 않습니다. 특정 기능이 지원되지 않거나 기능이 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure Preview에 대한 추가 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.

Azure Machine Learning 컴퓨팅 인스턴스를 사용하면 작업 영역의 완전 통합형 Notebook 환경에서 모델을 작성, 학습 및 배포할 수 있습니다.

SSH가 필요 없는 원격 서버로 계산 인스턴스를 사용 하 여 [VS Code](https://techcommunity.microsoft.com/t5/azure-ai/power-your-vs-code-notebooks-with-azml-compute-instances/ba-p/1629630) 에서 Jupyter 노트북을 실행할 수 있습니다. [원격 SSH 확장](https://devblogs.microsoft.com/python/enhance-your-azure-machine-learning-experience-with-the-vs-code-extension/)을 통해 VS Code 통합을 사용 하도록 설정할 수도 있습니다.

패키지를 [설치](how-to-create-manage-compute-instance.md#install-packages) 하 고 계산 인스턴스에 [커널을 추가할](how-to-create-manage-compute-instance.md#add-new-kernels) 수 있습니다.  

다음 도구 및 환경은 계산 인스턴스에 이미 설치 되어 있습니다. 

|일반적인 도구 및 환경|세부 정보|
|----|:----:|
|드라이버|`CUDA`</br>`cuDNN`</br>`NVIDIA`</br>`Blob FUSE` |
|Intel MPI 라이브러리||
|Azure CLI ||
|Azure Machine Learning 샘플 ||
|Docker||
|Nginx||
|NCCL 2.0 ||
|Protobuf|| 

|**R** 도구 및 환경|세부 정보|
|----|:----:|
|RStudio Server 오픈 소스 버전 (미리 보기)||
|R 커널||
|R용 Azure Machine Learning SDK|[azuremlsdk](https://azure.github.io/azureml-sdk-for-r/reference/index.html)</br>SDK 샘플|

|**PYTHON** 도구 및 환경|세부 정보|
|----|----|
|Anaconda Python||
|Jupyter 및 확장||
|Jupyterlab 및 확장||
[Python용 Azure Machine Learning SDK](/python/api/overview/azure/ml/intro?preserve-view=true&view=azure-ml-py)</br>PyPI에서|대부분의 azureml 추가 패키지가 포함됩니다.  전체 목록을 보려면 [컴퓨팅 인스턴스에서 터미널 창을 열고](how-to-run-jupyter-notebooks.md#terminal) 다음을 실행합니다. <br/> `conda list -n azureml_py36 azureml*` |
|기타 PyPI 패키지|`jupytext`</br>`tensorboard`</br>`nbconvert`</br>`notebook`</br>`Pillow`|
|Conda 패키지|`cython`</br>`numpy`</br>`ipykernel`</br>`scikit-learn`</br>`matplotlib`</br>`tqdm`</br>`joblib`</br>`nodejs`</br>`nb_conda_kernels`|
|딥 러닝 패키지|`PyTorch`</br>`TensorFlow`</br>`Keras`</br>`Horovod`</br>`MLFlow`</br>`pandas-ml`</br>`scrapbook`|
|ONNX 패키지|`keras2onnx`</br>`onnx`</br>`onnxconverter-common`</br>`skl2onnx`</br>`onnxmltools`|
|Azure Machine Learning Python 및 R SDK 샘플||

Python 패키지는 **Python 3.6 - AzureML** 환경에 모두 설치됩니다.  

## <a name="accessing-files"></a>파일에 액세스

Notebook 및 R 스크립트는 Azure 파일 공유에서 작업 영역의 기본 스토리지 계정에 저장됩니다.  이러한 파일은 “사용자 파일” 디렉터리 아래에 있습니다. 이 스토리지를 사용하면 컴퓨팅 인스턴스 간에 Notebook을 쉽게 공유할 수 있습니다. 스토리지 계정은 컴퓨팅 인스턴스를 중지하거나 삭제하는 경우에도 Notebook을 안전하게 유지합니다.

작업 영역의 Azure 파일 공유 계정은 컴퓨팅 인스턴스에 드라이브로 탑재됩니다. 이 드라이브는 Jupyter, Jupyter Labs 및 RStudio의 기본 작업 디렉터리입니다. 즉, Jupyter, JupyterLab 또는 RStudio에서 만든 노트북 및 기타 파일은 자동으로 파일 공유에 저장 되 고 다른 계산 인스턴스에서만 사용할 수 있습니다.

파일 공유의 파일은 동일한 작업 영역의 모든 컴퓨팅 인스턴스에서 액세스할 수 있습니다. 컴퓨팅 인스턴스에서 이러한 파일에 대한 모든 변경 내용은 안정적으로 파일 공유에 다시 저장됩니다.

또한 작업 영역 파일 공유의 사용자 파일 디렉터리 아래에 있는 폴더에 최신 Azure Machine Learning 샘플을 복제할 수 있습니다.

작은 파일을 작성 하는 것은 계산 인스턴스 로컬 디스크 자체에 쓰는 것 보다 네트워크 드라이브에서 속도가 느릴 수 있습니다.  많은 작은 파일을 작성하는 경우 `/tmp` 디렉터리와 같이 컴퓨팅 인스턴스에서 직접 디렉터리를 사용해보세요. 참고 이러한 파일은 다른 계산 인스턴스에서 액세스할 수 없습니다. 

`/tmp`임시 데이터에 대해 계산 인스턴스의 디렉터리를 사용할 수 있습니다.  그러나 계산 인스턴스의 OS 디스크에는 데이터의 많은 파일을 쓰지 마십시오.  대신 [데이터 저장소](concept-azure-machine-learning-architecture.md#datasets-and-datastores) 를 사용 해야 합니다. JupyterLab git 확장을 설치한 경우 계산 인스턴스 성능이 저하 될 수도 있습니다.

## <a name="managing-a-compute-instance"></a>컴퓨팅 인스턴스 관리

Azure Machine Learning Studio의 작업 영역에서 **컴퓨팅** 을 선택한 다음, 맨 위에 있는 **컴퓨팅 인스턴스** 를 선택합니다.

![컴퓨팅 인스턴스 관리](./media/concept-compute-instance/manage-compute-instance.png)

다음 작업을 수행할 수 있습니다.

* [계산 인스턴스를 만듭니다](#create). 
* 계산 인스턴스 탭을 새로 고칩니다.
* 계산 인스턴스를 시작, 중지 및 다시 시작 합니다.  인스턴스가 실행 될 때마다 해당 인스턴스에 대 한 비용을 지불 합니다. 계산 인스턴스를 사용 하 여 비용을 줄일 수 없는 경우 중지 합니다. 계산 인스턴스를 중지 하면 할당을 취소 합니다. 그런 다음, 필요할 때 다시 시작합니다. 계산 인스턴스를 중지 하면 계산 시간에 대 한 청구를 중지 하지만 디스크, 공용 IP 및 표준 부하 분산 장치에 대 한 요금이 계속 청구 됩니다.
* 계산 인스턴스를 삭제 합니다.
* 생성 한 계산만 표시 되도록 인스턴스 생성 목록을 필터링 합니다.

사용할 수 있는 작업 영역의 각 계산 인스턴스에 대해 다음을 수행할 수 있습니다.

* 컴퓨팅 인스턴스에서 Jupyter, JupyterLab, RStudio에 액세스합니다.
* SSH를 컴퓨팅 인스턴스로 실행합니다. SSH 액세스는 기본적으로 사용하지 않도록 설정되어 있지만 컴퓨팅 인스턴스 생성 시 사용하도록 설정할 수 있습니다. SSH 액세스에는 공개/프라이빗 키 메커니즘이 사용됩니다. 탭에 IP 주소, 사용자 이름 및 포트 번호와 같은 SSH 연결에 대한 세부 정보가 제공됩니다.
* 특정 컴퓨팅 인스턴스에 대한 세부 정보(예: IP 주소 및 지역)를 가져옵니다.

[AZURE RBAC](../role-based-access-control/overview.md) 를 사용 하면 작업 영역에서 계산 인스턴스를 만들고 삭제, 시작, 중지 및 다시 시작할 수 있는 사용자를 제어할 수 있습니다. 작업 영역 기여자 및 소유자 역할의 모든 사용자는 작업 영역에서 컴퓨팅 인스턴스를 만들고, 삭제, 시작, 중지 및 다시 시작할 수 있습니다. 그러나 특정 계산 인스턴스의 작성자나 사용자를 대신 하 여 생성 된 사용자만 해당 계산 인스턴스의 Jupyter, JupyterLab 및 RStudio에 액세스할 수 있습니다. 계산 인스턴스는 루트 액세스 권한이 있는 단일 사용자 전용 이며 Jupyter/JupyterLab/RStudio를 통해에서 터미널 할 수 있습니다. 계산 인스턴스는 단일 사용자 로그인을 포함 하 고 모든 작업은 Azure RBAC 및 실험 실행의 특성에 해당 사용자의 id를 사용 합니다. SSH 액세스는 공개/프라이빗 키 메커니즘을 통해 제어됩니다.

이러한 작업은 Azure RBAC를 통해 제어할 수 있습니다.
* *Microsoft.MachineLearningServices/workspaces/computes/read*
* *Microsoft.MachineLearningServices/workspaces/computes/write*
* *Microsoft.MachineLearningServices/workspaces/computes/delete*
* *MachineLearningServices/작업 영역/계산/시작/작업*
* *MachineLearningServices/작업 영역/계산/중지/작업*
* *MachineLearningServices/작업 영역/계산/다시 시작/작업*

계산 인스턴스를 만들려면 다음 동작에 대 한 사용 권한이 있어야 합니다.
* *Microsoft.MachineLearningServices/workspaces/computes/write*
* *MachineLearningServices/작업 영역/checkComputeNameAvailability/작업*


### <a name="create-a-compute-instance"></a><a name="create"></a>계산 인스턴스 만들기

Azure Machine Learning studio의 작업 영역에서, 노트북 중 하나를 실행할 준비가 되 면 **계산** 섹션 또는 **노트북** 섹션에서 [새 계산 인스턴스를 만듭니다](how-to-create-attach-compute-studio.md#compute-instance) . 

인스턴스를 만들 수도 있습니다.
* [통합 된 노트북 환경](tutorial-1st-experiment-sdk-setup.md#azure) 에서 직접
* Azure Portal에서
* Azure Resource Manager 템플릿에서 예제 템플릿은 [Azure Machine Learning 계산 인스턴스 만들기 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-machine-learning-compute-create-computeinstance)을 참조 하세요.
* [AZURE MACHINE LEARNING SDK](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/machine-learning/concept-compute-instance.md) 사용
* [Azure Machine Learning에 대 한 CLI 확장](reference-azure-machine-learning-cli.md#computeinstance) 에서

VM 제품군 할당량 당 지역별 전용 코어 및 계산 인스턴스 생성에 적용 되는 총 지역 할당량은 통합 되 고 Azure Machine Learning 교육 계산 클러스터 할당량과 공유 됩니다. 계산 인스턴스를 중지 하는 경우에는 계산 인스턴스를 다시 시작할 수 있도록 할당량을 해제 하지 않습니다.


### <a name="create-on-behalf-of-preview"></a>(미리 보기)를 대신 하 여 만들기

관리자는 데이터 과학자를 대신 하 여 계산 인스턴스를 만들고 다음을 사용 하 여 인스턴스를 할당할 수 있습니다.
* [Azure Resource Manager 템플릿입니다](https://github.com/Azure/azure-quickstart-templates/tree/master/101-machine-learning-compute-create-computeinstance).  이 템플릿에 필요한 TenantID 및 ObjectID를 찾는 방법에 대 한 자세한 내용은 [인증 구성에 대 한 id 개체 Id 찾기](../healthcare-apis/find-identity-object-ids.md)를 참조 하세요.  Azure Active Directory 포털에서 이러한 값을 찾을 수도 있습니다.
* REST API

계산 인스턴스를 만드는 데이터 과학자에는 다음과 같은 Azure RBAC 권한이 필요 합니다. 
* *MachineLearningServices/작업 영역/계산/시작/작업*
* *MachineLearningServices/작업 영역/계산/중지/작업*
* *MachineLearningServices/작업 영역/계산/다시 시작/작업*
* *MachineLearningServices/작업 영역/계산/applicationaccess/작업*

데이터 과학자는 계산 인스턴스를 시작, 중지 및 다시 시작할 수 있습니다. 다음에 대해 계산 인스턴스를 사용할 수 있습니다.
* Jupyter
* JupyterLab
* RStudio
* 통합 노트북

## <a name="compute-target"></a>컴퓨팅 대상

컴퓨팅 인스턴스는 Azure Machine Learning 컴퓨팅 학습 클러스터와 유사하게 [학습 컴퓨팅 대상](concept-compute-target.md#train)으로 사용할 수 있습니다. 

계산 인스턴스:
* 작업 큐가 있습니다.
* 회사에서 SSH 포트를 열지 않아도 가상 네트워크 환경에서 작업을 안전 하 게 실행 합니다. 작업은 컨테이너 화 된 환경에서 실행 되며 모델 종속성을 Docker 컨테이너에 패키지 합니다.
* 여러 작은 작업을 병렬로 실행할 수 있습니다 (미리 보기).  코어 당 두 작업은 병렬로 실행할 수 있으며 나머지 작업은 큐에 대기 합니다.
* 단일 노드 다중 GPU 분산 학습 작업 지원

계산 인스턴스는 테스트/디버그 시나리오에 대 한 로컬 추론 배포 대상으로 사용할 수 있습니다.


## <a name="what-happened-to-notebook-vm"></a><a name="notebookvm"></a>Notebook VM의 변경 내용

컴퓨팅 인스턴스가 Notebook VM을 대체하고 있습니다.  

작업 영역 파일 공유에 저장된 모든 Notebook 파일과 작업 영역 데이터 저장소의 데이터는 컴퓨팅 인스턴스에서 액세스할 수 있습니다. 그러나 노트북 VM에 이전에 설치 된 사용자 지정 패키지는 모두 계산 인스턴스에 다시 설치 해야 합니다. 계산 클러스터 만들기에 적용 되는 할당량 제한은 계산 인스턴스 생성에도 적용 됩니다.

새 Notebook VM을 만들 수 없습니다. 그러나 전체 기능을 사용하여 만든 Notebook VM에는 계속 액세스하여 사용할 수 있습니다. 컴퓨팅 인스턴스를 기존 Notebook VM과 동일한 작업 영역에 만들 수 있습니다.


## <a name="next-steps"></a>다음 단계

* [계산 인스턴스 만들기 및 관리](how-to-create-manage-compute-instance.md)
* [자습서: 첫 번째 ML 모델 학습](tutorial-1st-experiment-sdk-train.md)에서는 통합 Notebook으로 컴퓨팅 인스턴스를 사용하는 방법을 보여 줍니다.
