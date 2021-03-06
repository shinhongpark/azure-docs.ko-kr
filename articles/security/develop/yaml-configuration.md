---
title: Microsoft Azure 보안 코드 분석 작업 사용자 지정 가이드
description: 이 문서에서는 Microsoft 보안 코드 분석 확장에서 모든 작업을 사용자 지정 하기 위한 YAML 구성 옵션을 설명 합니다.
author: sukhans
manager: sukhans
ms.author: terrylan
ms.date: 11/29/2019
ms.topic: article
ms.service: security
services: azure
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.openlocfilehash: 6985107dd8f13e26875cf5ea7428b3280d00cea1
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "85367260"
---
# <a name="yaml-configuration-options-to-customize-the-build-tasks"></a>빌드 작업을 사용자 지정 하는 YAML 구성 옵션

이 문서에서는 각 빌드 작업에서 사용할 수 있는 모든 YAML 구성 옵션을 나열 합니다. 이 문서는 보안 코드 분석 도구에 대 한 작업으로 시작 합니다. 사후 처리 작업으로 끝납니다.

## <a name="anti-malware-scanner-task"></a>맬웨어 방지 스캐너 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| InputType | 선택 목록 | always | True | Basic | 기본, 사용자 지정 | 
| ScanType | 선택 목록 | InputType = 기본 | True | CustomScan | CustomScan, FullSystemScan, QuickScan, YourConfiguredScan | 맬웨어 방지 검사에 사용할 검색 유형입니다.
| FileDirPath | filePath | ScanType = CustomScan | True | $ (Build.stagingdirectory) |  | 검색할 파일 또는 디렉터리를 나타냅니다.
| DisableRemediation | boolean | ScanType = CustomScan | False | true |  | 선택 된 경우: 1) 파일 제외가 무시 됩니다. 2) 보관 파일이 검색 됩니다. 3) 검색 후에는 작업이 적용 되지 않습니다. 4) 검색 후 이벤트 로그 항목이 기록 되지 않습니다. 5) 사용자 지정 검색에서 검색은 사용자 인터페이스에 표시 되지 않습니다. 6) 콘솔 출력에 사용자 지정 검사의 검색 목록이 표시 됩니다.
| BootSectorScan | boolean | ScanType = CustomScan | False | false |  | 선택 하는 경우 부팅 섹터 검색을 사용 하도록 설정 합니다.
| 인수 | 문자열 | InputType = 사용자 지정 | True | -Scan-ScanType DisableRemediation-File $ (Build.stagingdirectory) |  | 명령줄 인수입니다. 여기서-File의 인수는 절대 경로 이거나 빌드 에이전트에 미리 정의 된 $ (Build.stagingdirectory)에 대 한 상대 경로입니다. 참고:-File에 대 한 인수를 마지막 인수로 제공 하지 않으면 $ (Build.stagingdirectory)로 기본 설정 됩니다. MpCmdRun.exe 도구에서 허용 하는 고유한 인수를 제공할 수도 있습니다.<br/><br/>이 도구에 대 한 명령줄 인수에 대 한 자세한 내용을 보려면 <strong>-h</strong> 또는 <strong>-?</strong> 를 입력 하십시오. 인수 필드에서를 실행 하 고 빌드 작업을 실행 합니다.
| EnableServices | boolean | always | True | false |  | 선택 하는 경우 사용 하지 않도록 설정 된 경우 Windows 업데이트에 필요한 서비스를 사용 하도록 설정 합니다.<br/>**참고**: 그룹 정책에서 서비스를 사용 하지 않도록 설정 하 고이 빌드를 실행 하는 계정에 관리자 권한이 있는지 확인 하십시오.
| SupportLogOnError | boolean | always | True | false |  | 선택 하는 경우 오류가 발생 했을 때 진단을 위한 지원 파일을 수집 합니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.<br/>**참고**:이 빌드가 실행 되 고 있는 계정에 관리자 권한이 있는지 확인 하세요.
| TreatSignatureUpdateFailureAs | 선택 목록 | always | True | Warning | 오류, 표준, 경고 | 런타임에 서명을 업데이트할 수 없는 경우 사용 되는 로그 수준입니다. **오류**로 설정 되 면 서명 업데이트에 실패 하면 빌드 작업이 실패 합니다. 서명이 상대적으로 최신 (3 시간 미만) 인 경우에도 호스트 된 빌드 에이전트에서 서명 업데이트가 실패 하는 것이 일반적입니다.
| SignatureFreshness | 선택 목록 | always | True | UpToDate | OneDay, ThreeDays, TwoDays, UpToDate | 맬웨어 방지 서명에 허용 되는 최대 기간입니다. 서명을 업데이트할 수 없고이 값 보다 오래 된 경우 빌드 작업은 **서명 확인 사용 기간** 필드에서 선택한 값에 따라 동작 합니다. 참고: **최신 버전을 선택 하**는 경우 서명은 최대 3 시간까지 허용 됩니다.
| TreatStaleSignatureAs | 선택 목록 | always | True | Error | 오류, 표준, 경고 | 서명 기간이 선택한 **맬웨어 방지 프로그램 서명 기간**보다 오래 된 경우 사용 되는 로그 수준입니다. 최신 서명이 맬웨어 방지 검사를 계속 하는 **경고** 또는 **정보** 로 처리 될 수 있지만이 방법은 사용 하지 않는 것이 좋습니다.

## <a name="binskim-task"></a>BinSkim 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| InputType | 선택 목록 | always | True | Basic | Basic, CommandLine | 
| 인수 | 문자열 | InputType = CommandLine | True |  |  | 실행할 표준 BinSkim 명령줄 인수입니다. 출력 경로가 제거 되 고 바뀝니다.<br>이 도구에 대 한 명령줄 인수에 대 한 자세한 내용을 보려면 인수 필드에 **도움말** 을 입력 하 고 빌드 작업을 실행 하십시오.
| 기능 | 선택 목록 | InputType = 기본 | True | 분석 | 분석, 덤프, exportConfig, exportRules | 
| AnalyzeTarget | filePath | InputType = Basic && Function = 분석 | True | $ (Build.artifactstagingdirectory) \* .dll;<br>$ (Build.artifactstagingdirectory) \* .exe |  | 분석할 하나 이상의 이진으로 확인 되는 파일, 디렉터리 또는 필터 패턴에 대 한 하나 이상의 지정자입니다. ('; ' 구분한 목록)
| AnalyzeSymPath | 문자열 | InputType = Basic && Function = 분석 | False |  |  | 대상에 대 한 기호 파일의 경로입니다.
| AnalyzeConfigPath | 문자열 | InputType = Basic && Function = 분석 | False | default |  | 분석을 구성 하는 데 사용 될 정책 파일의 경로입니다. 기본 제공 설정을 사용 하려면 ' 기본값 '의 값을 전달 합니다.
| AnalyzePluginPath | 문자열 | InputType = Basic && Function = 분석 | False |  |  | 분석 집합의 모든 대상에 대해 호출 되는 플러그 인의 경로입니다.
| AnalyzeRecurse | boolean | InputType = Basic && Function = 분석 | False | true |  | 파일 지정자 인수를 평가할 때 하위 디렉터리로 재귀 합니다.
| AnalyzeVerbose | boolean | InputType = Basic && Function = 분석 | False | false |  | 자세한 정보 출력을 내보냅니다. 결과 포괄적인 보고서는 규정 준수 시나리오에 대 한 적절 한 증거를 제공 하도록 설계 되었습니다.
| AnalyzeHashes | boolean | InputType = Basic && Function = 분석 | False | false |  | SARIF 보고서를 내보낼 때 분석 대상의 SHA-256 해시를 출력 합니다.
| AnalyzeStatistics | boolean | InputType = Basic && Function = 분석 | False | false |  | 분석 세션에 대 한 타이밍 및 기타 통계를 생성 합니다.
| AnalyzeEnvironment | boolean | InputType = Basic && Function = 분석 | False | false |  | 출력 파일에 대 한 실행의 컴퓨터 환경 세부 정보를 기록 합니다. 경고:이 옵션은 모든 환경 변수 값과 같은 잠재적으로 중요 한 정보를 내보낸 로그에 기록 합니다.
| ExportRulesOutputType | 선택 목록 | InputType = 기본 && 함수 = exportRules | False | SARIF | SARIF, SonarQube | 출력할 규칙 설명자 파일의 유형입니다. 이는 보안 분석 로그 빌드 게시 작업에서 게시 한 BinSkim logs 폴더에 포함 됩니다.
| 대상 \ 대상 | filePath | InputType = Basic && Function = dump | True | $ (Build.artifactstagingdirectory) |  | 분석할 하나 이상의 이진으로 확인 되는 파일, 디렉터리 또는 필터 패턴에 대 한 하나 이상의 지정자입니다. ('; ' 구분한 목록)
| DumpRecurse | boolean | InputType = Basic && Function = dump | False | true |  | 파일 지정자 인수를 평가할 때 하위 디렉터리로 재귀 합니다.
| 로깅 세부 정보 표시 | boolean | InputType = Basic && Function = dump | False | true |  | 자세한 정보 출력을 내보냅니다. 결과 포괄적인 보고서는 규정 준수 시나리오에 대 한 적절 한 증거를 제공 하도록 설계 되었습니다.
| toolVersion | 선택 목록 | always | False | 최신 버전 | 1.5.0, 최신, LatestPreRelease | 실행할 도구의 버전입니다.

## <a name="credential-scanner-task"></a>자격 증명 스캐너 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| outputFormat | 선택 목록 | always | False | pre | csv, pre, tsv | 자격 증명 스캐너 결과 파일의 출력 형식입니다.
| toolVersion | 선택 목록 | always | False | 최신 버전 | 1.27.7, 최신, LatestPreRelease | 실행할 도구의 버전입니다.
| scanFolder | filePath | always | False | $ (빌드용 디렉터리) |  | 자격 증명을 검색할 리포지토리의 폴더입니다.
| searchersFileType | 선택 목록 | always | False | 기본값 | 사용자 지정, 기본, DefaultAndCustom | 검색에 사용 되는 searchers 파일을 찾을 수 있는 옵션입니다.
| searchersFile | filePath | searchersFileType = = Custom 또는 searchersFileType = = DefaultAndCustom | False |  |  | 실행할 확인의 자격 증명 스캐너 searchers 구성 파일입니다. 자격 증명 스캐너 searchers 파일에 대 한 쉼표로 구분 된 경로 목록을 제공 하 여 여러 값을 포함 하 고 사용할 수 있습니다.
| suppressionsFile | filePath | always | False |  |  | 출력 로그에서 문제를 억제 하는 데 사용할 자격 증명 스캐너 비 표시 파일입니다.
| suppressAsError | boolean | always | False | false |  | 표시 되지 않는 일치 항목은 출력 파일 [-O]-일치 항목으로 출력 됩니다. 기본 억제 된 출력 파일 [-O]-표시 되지 않고 [-f]. [-f]. 기본값은 ' f a l s e '입니다.
| verboseOutput | boolean | always | False | false |  | 자세한 정보를 출력 합니다.
| batchSize | 문자열 | always | False |  |  | 자격 증명 스캐너를 병렬로 실행 하는 데 사용 되는 동시 스레드 수입니다. (기본값은 20)<br/>값은 1-2147483647 범위 내에 있어야 합니다.
| regexMatchTimeoutInSeconds | 문자열 | always | False |  |  | 확인을 중단 하기 전에 검색 자가 일치를 시도 하는 데 소요 되는 시간 (초)입니다.<br/>``-Co RegexMatchTimeoutInSeconds=<Value>``명령줄에를 추가 합니다.
| fileScanReadBufferSize | 문자열 | always | False |  |  | 콘텐츠를 읽는 동안 버퍼 크기 (바이트)입니다. (기본값은 524288)<br/>``-Co FileScanReadBufferSize=<Value>``명령줄에를 추가 합니다.
| maxFileScanReadBytes | 문자열 | always | False |  |  | 콘텐츠 분석 중 지정 된 파일에서 읽을 최대 바이트 수입니다. (기본값은 104857600)<br/>``-Co MaxFileScanReadBytes=<Value>``명령줄에를 추가 합니다.

## <a name="roslyn-analyzers-task"></a>Roslyn 분석기 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                   |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| userProvideBuildInfo | 선택 목록 | always | True | auto | auto, msBuildInfo | MSBuild 버전, MSBuild 아키텍처 및 Roslyn 분석을 위한 명령줄 빌드를 제공 하는 사용자를 위한 옵션입니다. **자동** 을 선택 하는 경우이 작업은 동일한 파이프라인의 이전 **MSBuild**, **vsbuild**및/또는 **.net Core** (빌드) 작업에서 빌드 정보를 검색 합니다.
| msBuildVersion | 선택 목록 | userProvideBuildInfo = = msBuildInfo | True | 16.0 | 15.0, 16.0 | MSBuild 버전입니다.
| msBuildArchitecture | 선택 목록 | userProvideBuildInfo = = msBuildInfo | True | x86 | DotNetCore, x64, x86 | MSBuild 아키텍처입니다. 참고: 빌드 명령줄에서 **dotnet.exe 빌드**를 호출 하는 경우 **Via .net Core** 옵션을 선택 합니다.
| msBuildCommandline | 문자열 | userProvideBuildInfo = = msBuildInfo | True |  |  | 솔루션 또는 프로젝트를 컴파일하기 위한 전체 빌드 명령줄입니다.<br/><br/>참고: 명령줄은 **MSBuild.exe** 또는 **dotnet.exe**에 대 한 전체 경로로 시작 해야 합니다.<br/>명령은 $ (빌드용 디렉터리)를 사용 하 여 작업 디렉터리로 실행 됩니다.
| rulesetName | 선택 목록 | always | False | 권장 | 사용자 지정, 없음, 권장, 필수 | 사용할 명명 된 규칙 집합입니다.<br/><br/>`Ruleset Configured In Your Visual Studio Project File(s)`를 선택 하면 VS 프로젝트 파일에 미리 구성 된 규칙 집합이 사용 됩니다. `Custom`를 선택 하면 사용자 지정 규칙 집합 경로 옵션을 설정할 수 있습니다.
| Rulesetversion이 | 선택 목록 | rulesetName = = Required 또는 rulesetName = = 권장 | False | 최신 버전 | 8.0, 8.1, 8.2, 최신, LatestPreRelease | 선택한 SDL 규칙 집합의 버전입니다.
| customRuleset 집합 | 문자열 | rulesetName = 사용자 지정 | False |  |  | 사용할 규칙 집합에 액세스할 수 있는 경로입니다. 상대 경로는 원본 리포지토리의 루트 ()로 정규화 됩니다 `$(Build.SourcesDirectory)` .<br/><br/>로 설정 된를 사용 하 여 규칙 집합을 지정 하는 경우 `Rules` `Actions` 에는 `Error` 빌드 작업이 실패 합니다. 이를 수행 하는 규칙 집합을 사용 하려면 `Continue on error` 빌드 작업의를 체크 인 하십시오 `Control Options` .
| microsoftAnalyzersVersion | 선택 목록 | always | False | 최신 버전 | 2.9.3, 2.9.4, 2.9.6, 최신, LatestPreRelease | 실행할 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) 패키지의 버전입니다.
| suppressionFileForCompilerWarnings | filePath | always | False |  |  | C # 및 VB 컴파일러 경고를 표시 하지 않는 비 표시 파일입니다.<br/><br/>각 경고 ID가 별도의 줄에 나열 된 일반 텍스트 파일입니다.<br/>컴파일러 경고의 경우 경고 식별자의 숫자 부분만 지정 합니다. 예를 들어 1018은 CS1018를 표시 하지 않으며 CA1501는 CA1501를 표시 하지 않습니다.<br/><br/>상대 파일 경로는 원본 리포지토리의 루트 ()에 추가 됩니다 `$(Build.SourcesDirectory)` .

## <a name="tslint-task"></a>TSLint 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RuleLibrary | 선택 목록 | always | True | tslint | 사용자 지정, microsoft, tslint | 모든 결과에는 선택한 버전의 TSLint와 함께 제공 되는 규칙이 포함 됩니다 (**기본 전용**).<br/><br/>**기준만-** TSLint와 함께 제공 되는 규칙만 제공 됩니다.<br/><br/>**Microsoft 규칙 포함-** 다운로드 [tslint-microsoft](https://github.com/Microsoft/tslint-microsoft-contrib) -tslint 실행에 사용할 수 있는 규칙을 포함 합니다. 이 옵션을 선택 하면 `Type Checking` Microsoft의 규칙에 필요 하므로 자동으로 사용 되는 확인란은 숨겨집니다. 또한 필드를 표시 하 여 `Microsoft Contribution Version` npm의 버전을 `tslint-microsoft-contrib` 선택할 수 [npm](https://www.npmjs.com/package/tslint-microsoft-contrib) 있습니다.<br/><br/>**사용자 지정 규칙 포함-** 표시 `Rules Directory` TSLint 실행에 사용할 수 있는 TSLint 규칙의 디렉터리에 액세스할 수 있는 경로를 허용 하는 필드입니다.<br/><br/>**참고:** 사용자가 Microsoft 규칙 집합을 구성 하는 데 문제가 발생 하 여 기본값이 tslint로 변경 되었습니다. 특정 버전 구성에 대 한 자세한 내용은 [tslint](https://github.com/microsoft/tslint-microsoft-contrib)을 참조 하세요.
| 규칙 디렉터리 | 문자열 | RuleLibrary = = 사용자 지정 | True |  |  | TSLint 실행에서 사용할 수 있는 추가 TSLint 규칙을 포함 하는 액세스 가능한 디렉터리입니다.
| 집합이 | 선택 목록 | RuleLibrary! = microsoft | True | tsrecommended | 사용자 지정, tslatest, tslatest | TypeScript 파일에 대해 실행할 규칙을 정의 합니다.<br/><br/>** [tslint: 최신](https://github.com/palantir/tslint/blob/master/src/configs/latest.ts)  - ** `tslint:recommended`모든 TSLint 릴리스의 최신 규칙에 대 한 구성을 포함 하도록 지속적으로 업데이트 됩니다. 이 구성을 사용 하면 코드에서 보풀이 실패를 야기 하는 새 규칙을 사용할 수 있으므로 사소한 릴리스에 대 한 주요 변경 내용이 발생할 수 있습니다. TSLint가 주 버전 범프에 도달 하면가 `tslint:recommended` 와 동일 하 게 업데이트 됩니다 `tslint:latest` .<br/><br/>** [tslint: 권장](https://github.com/palantir/tslint/blob/master/src/configs/recommended.ts)  - ** 일반적으로 일반적인 TypeScript 프로그래밍에 대해 권장 되는 안정 된 독단적인 규칙 집합입니다. 이 구성은 이후 `semver` 부 또는 패치 릴리스에 대 한 주요 변경 내용이 *없습니다* .
| RulesetMicrosoft | 선택 목록 | RuleLibrary = = microsoft | True | mssdlrequired | 사용자 지정, msrecommended, mssdlrecommended, mssdlrequired, tslatest, tslatest | TypeScript 파일에 대해 실행할 규칙을 정의 합니다.<br/><br/>** [microsoft: sdl-필수](https://github.com/Microsoft/tslint-microsoft-contrib/wiki/TSLint-and-the-Microsoft-Security-Development-Lifecycle)  - ** Tslint에서 제공 하는 사용 가능한 모든 검사를 실행 하 고, *필요한* [SDL (보안 개발 수명 주기)](https://www.microsoft.com/sdl/) 정책을 충족 하는 tslint-microsoft-역할 규칙을 실행 합니다.<br/><br/>** [microsoft: sdl-권장](https://github.com/Microsoft/tslint-microsoft-contrib/wiki/TSLint-and-the-Microsoft-Security-Development-Lifecycle)  - ** Tslint에서 제공 하는 사용 가능한 모든 검사를 실행 하 고, *필수 및 권장* [SDL (보안 개발 수명 주기)](https://www.microsoft.com/sdl/) 정책을 충족 하는 tslint-microsoft-역할 규칙을 실행 합니다.<br/><br/>**microsoft: 권장** Tslint-microsoft-역할 규칙의 작성자가 권장 하는 모든 검사입니다. 여기에는 보안 및 비보안 검사가 포함 됩니다.<br/><br/>** [tslint: 최신](https://github.com/palantir/tslint/blob/master/src/configs/latest.ts)  - ** `tslint:recommended`모든 TSLint 릴리스의 최신 규칙에 대 한 구성을 포함 하도록 지속적으로 업데이트 됩니다. 이 구성을 사용 하면 코드에서 보풀이 실패를 야기 하는 새 규칙을 사용할 수 있으므로 사소한 릴리스에 대 한 주요 변경 내용이 발생할 수 있습니다. TSLint가 주 버전 범프에 도달 하면가 `tslint:recommended` 와 동일 하 게 업데이트 됩니다 `tslint:latest` .<br/><br/>** [tslint: 권장](https://github.com/palantir/tslint/blob/master/src/configs/recommended.ts)  - ** 일반적으로 일반적인 TypeScript 프로그래밍에 대해 권장 되는 안정 된 독단적인 규칙 집합입니다. 이 구성은 이후 `semver` 부 또는 패치 릴리스에 대 한 주요 변경 내용이 *없습니다* .
| RulesetFile | 문자열 | 규칙 집합 = = 사용자 지정 또는 RulesetMicrosoft = = 사용자 지정 | True |  |  | 실행할 규칙을 지정 하는 [구성 파일](https://palantir.github.io/tslint/usage/cli/) 입니다.<br/><br/>구성에 대 한 경로는 [사용자 지정 규칙](https://palantir.github.io/tslint/develop/custom-rules/)에 대 한 경로로 추가 됩니다.
| FileSelectionType | 선택 목록 | always | True | fileGlob | fileGlob, projectFile | 
| Files | 문자열 | FileSelectionType = = fileGlob | True | **\*.tts |  | 처리할 파일을 결정 하는 [glob](https://www.npmjs.com/package/glob) 파일입니다. 경로는 값을 기준으로 `Build.SourcesDirectory` 합니다.<br/><br/>Microsoft의 기여 라이브러리를 사용 하려면 프로젝트 파일을 사용 해야 합니다. 옵션으로 Microsoft의 기여 라이브러리를 사용 하는 경우 `File Glob Pattern` 프로젝트 파일이 자동으로 생성 됩니다.
| ECMAScriptVersion | 선택 목록 | FileSelectionType = = fileGlob && RuleLibrary = = microsoft | True | ES3 | ES2015, ES2016, ES2017, ES3, ES5, ES6, ESNext | TypeScript 컴파일러를 사용 하 여 구성 된 ECMAScript의 대상 버전입니다. 프로젝트 파일을 사용 하는 경우 파일에 tsconfig.jsTypeScript의 compilerOptions 필드가 있습니다.
| 프로젝트 | 문자열 | FileSelectionType = = projectFile | True |  |  | TSLint를 실행할 TypeScript 파일을 지정 하는 파일 [ 에 대 한tsconfig.js](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html) 경로입니다. 경로는 값을 기준으로 `Build.SourcesDirectory` 합니다.
| TypeCheck | boolean | RuleLibrary! = microsoft && FileSelectionType = = projectFile | False | true |  | Lint 규칙을 실행할 때 형식 검사기를 사용 하도록 설정 합니다.
| ExcludeFiles | 문자열 | always | False |  |  | Lint에서 제외할 파일을 나타내는 [glob](https://www.npmjs.com/package/glob) 입니다. 경로는 값을 기준으로 `Build.SourcesDirectory` 합니다. 세미콜론으로 구분 하 여 여러 값을 지정할 수 있습니다.
| OutputFormat | 선택 목록 | always | True | json : | checkstyle, codeFrame, filesList, json, msbuild, pmd, prose, 세련 되 고 자세한 정보 표시, vso | 출력을 생성 하는 데 사용할 [포맷터](https://palantir.github.io/tslint/formatters/) 입니다. JSON 형식은 사후 분석과 호환 됩니다.
| NodeMemory | 문자열 | always | False |  |  | TSLint를 실행 하기 위해 노드에 할당할 명시적 메모리 양 (Mb)입니다. 예: 8000<br/><br/>인 `--max_old_space=<value>` 노드의 CLI 옵션에 매핑합니다 `v8 option` .
| ToolVersion | 선택 목록 | RuleLibrary! = microsoft | True | 최신 | 4.0.0, 4.0.1, 4.0.2, 4.1.0, 4.1.1, 4.2.0, 4.3.0, 4.3.1, 4.4.0, 4.4.1, 4.4.2, 4.5.0, 4.5.1, 5.0.0, 5.1.0, 5.2.0, 5.3.0, 5.3.2, 5.4.0, 5.4.1, 5.4.2, 5.4.3, 5.5.0, 최신 | 다운로드 하 여 실행할 TSLint의 [버전](https://github.com/palantir/tslint/releases) 입니다.
| TypeScriptVersion | 선택 목록 | always | True | 최신 | 0.8.0부터, 0.8.1, 0.8.2, 0.8.3, 0.9.0, 0.9.1, 0.9.5, 0.9.7, 1.0.0, 1.0.1, 1.3.0, 1.4.1, 1.5.3, 1.6.2, 1.7.3, 1.7.5, 1.8.0, 1.8.10, 1.8.2, 1.8.5, 1.8.6, 1.8.7, 1.8.9, 1.9.0, 2.0.0, v2.0.10, 2.0.2, 2.0.3 라이브러리가, 2.0.6, 2.0.7, 2.0.8 이상이 필요, 2.0.9, 2.1.1, 2.1.4, 2.1.5, 2.1.6, 2.2.0, 2.2.1, custom, 최신 | 다운로드 하 여 사용할 [typescript](https://www.npmjs.com/package/typescript) 의 버전입니다.<br/>**참고:** 코드를 컴파일하는 데 사용 되는 것과 동일한 버전의 TypeScript 여야 합니다.
| TypeScriptVersionCustom | 문자열 | TypeScriptVersion = = 사용자 지정 | True | 최신 |  | 다운로드 하 여 사용할 [typescript](https://www.npmjs.com/package/typescript) 의 버전입니다.<br/>**참고:** 코드를 컴파일하는 데 사용 되는 것과 동일한 버전의 TypeScript 여야 합니다.
| MicrosoftContribVersion | 선택 목록 | RuleLibrary = = microsoft |  | 최신 | 4.0.0, 4.0.1, 5.0.0, 5.0.1 용, 최신 | 다운로드 하 여 사용 하는 [tslint](https://www.npmjs.com/package/tslint-microsoft-contrib) (SDL 규칙)의 버전입니다.</br>**참고:** Tslint-microsoft-tslint에 대해 선택한 버전과 호환 되는 버전의 [tslint](https://www.npmjs.com/package/tslint) 가 선택 됩니다. Tslint에 대 한 업데이트는 테스트 기간이 발생할 때까지이 빌드 작업에 의해 제어 됩니다.

## <a name="publish-security-analysis-logs-task"></a>보안 분석 로그 게시 태스크

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ArtifactName | 문자열 | always | True | CodeAnalysisLogs |  | 만들 아티팩트의 이름입니다.
| ArtifactType | 선택 목록 | always | True | 컨테이너 | 컨테이너, FilePath | 만들 아티팩트의 형식입니다.
| TargetPath | 문자열 | ArtifactType = FilePath | False | \\my\share \$ (Build DefinitionName)<br>\$(빌드 BuildNumber) |  | 파일을 복사할 파일 공유
| AllTools | boolean | always | True | true |  | 모든 보안 개발 도구 빌드 작업에서 생성 된 결과를 게시 합니다.
| 프로그램이 | boolean | AllTools = false | True | true |  | 맬웨어 방지 빌드 작업에 의해 생성 된 결과를 게시 합니다.
| BinSkim | boolean | AllTools = false | True | true |  | BinSkim build 작업에 의해 생성 된 결과를 게시 합니다.
| CredScan | boolean | AllTools = false | True | true |  | 자격 증명 스캐너 빌드 작업으로 생성 된 결과를 게시 합니다.
| Rosl이상 분석기 | boolean | AllTools = false | True | false |  | Roslyn 분석기 빌드 작업에 의해 생성 된 결과를 게시 합니다.
| TSLint | boolean | AllTools = false | True | true |  | TSLint build 작업에 의해 생성 된 결과를 게시 합니다. JSON 형식의 TSLint 로그만 보고서에 대해 지원 됩니다. 다른 형식을 선택한 경우에는 TSLint 빌드 작업을 적절 하 게 업데이트 하세요.
| ToolLogsNotFoundAction | 선택 목록 | always | True | 표준 | 오류, 없음, 표준, 경고 | 도구를 실행 하지 않은 경우 선택 된 도구 (또는 모든 도구를 선택 하는 경우 도구)에 대 한 로그를 찾을 수 없는 경우 수행할 동작입니다.<br/><br/>**옵션:**<br/>**없음:** VSTS 변수 **system.object** 를 **true**로 설정 하 여 액세스할 수 있는 자세한 정보 출력 스트림에 메시지가 기록 됩니다.<br/>**Standard:** (기본값) 도구에 대 한 로그를 찾을 수 없는 표준 출력 메시지를 기록 합니다.<br/>**경고:** 빌드 요약 페이지에 경고로 표시 되는, 도구에 대 한 로그를 찾지 못한 노란색 경고 메시지를 씁니다.<br/>**오류:** 빨간색 오류 메시지를 기록 하 고 빌드를 중단 하는 예외를 throw 합니다. 이 옵션을 사용 하 여 개별 도구를 선택 하 여 실행 되는 도구를 확인 합니다.

## <a name="security-report-task"></a>보안 보고서 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| VstsConsole | boolean | always | False | true |  | 파이프라인 콘솔에 결과를 씁니다.
| TsvFile | boolean | always | False | true |  | 검색 된 결과와 결과에 대 한 정보를 구분 하는 탭이 하나씩 있는 tsv 파일 (탭으로 구분 된 값)을 생성 합니다.
| HtmlFile | boolean | always | False | true |  | Html 보고서 파일을 생성 합니다.
| AllTools | boolean | always | True | false |  | 모든 보안 개발 도구에서 생성 된 작업을 작성 하는 보고서 결과입니다.
| BinSkim | boolean | AllTools = false | True | false |  | BinSkim build 작업에 의해 생성 된 결과를 보고 합니다.
| 불균형 | 선택 목록 | AllTools = true 또는 BinSkim = true | True | Error | 오류, WarningAbove | 보고할 결과의 수준입니다.
| CredScan | boolean | AllTools = false | True | false |  | 자격 증명 스캐너 빌드 작업을 통해 생성 되는 보고서 결과입니다.
| Rosl이상 분석기 | boolean | AllTools = false | True | false |  | Roslyn Analyzer 빌드 작업에 의해 생성 된 결과를 보고 합니다.
| RoslynAnalyzersBreakOn | 선택 목록 | AllTools = true 또는 Rosl를 분석기 = true | True | Error | 오류, WarningAbove | 보고할 결과의 수준입니다.
| TSLint | boolean | AllTools = false | True | false |  | TSLint build 작업에 의해 생성 된 결과를 보고 합니다. JSON 형식의 TSLint 로그만 보고서에 대해 지원 됩니다. 다른 형식을 선택한 경우에는 TSLint 빌드 작업을 적절 하 게 업데이트 하세요.
| Tslintor | 선택 목록 | AllTools = true 또는 TSLint = true | True | Error | 오류, WarningAbove | 보고할 결과의 수준입니다.
| ToolLogsNotFoundAction | 선택 목록 | always | True | 표준 | 오류, 없음, 표준, 경고 | 도구를 실행 하지 않은 경우 선택 된 도구 (또는 모든 도구를 선택 하는 경우 도구)에 대 한 로그를 찾을 수 없는 경우 수행할 동작입니다.<br/><br/>**옵션:**<br/>**없음:** VSTS 변수 **system.object** 를 **true**로 설정 하 여 액세스할 수 있는 자세한 정보 출력 스트림에 메시지가 기록 됩니다.<br/>**Standard:** (기본값) 도구에 대 한 로그를 찾을 수 없는 표준 출력 메시지를 기록 합니다.<br/>**경고:** 빌드 요약 페이지에 경고로 표시 되는, 도구에 대 한 로그를 찾지 못한 노란색 경고 메시지를 씁니다.<br/>**오류:** 빨간색 오류 메시지를 기록 하 고 빌드를 중단 하는 예외를 throw 합니다. 이 옵션을 사용 하 여 개별 도구를 선택 하 여 실행 되는 도구를 확인 합니다.
| CustomLogsFolder | 문자열 | always | False |  |  | 분석 도구 로그가 있는 기본 폴더 개별 로그 파일은이 경로 아래에 있는 각 도구 다음에 이름이 지정 된 하위 폴더에 있습니다.

## <a name="post-analysis-task"></a>사후 분석 작업

| **InputType**      | **형식**     | **해당**            | **필수** | **기본값**             | **옵션 (선택 목록)**                                   | **설명**                                                                                                                                                                                                                                                                                                                            |
|------------|---------------|-----------------------|----------|---------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AllTools | boolean | always | True | false |  | Microsoft 보안 코드 분석 빌드 작업에서 문제가 발견 되 면 빌드를 중단 합니다.
| BinSkim | boolean | AllTools = false | True | false |  | 선택한 중단 옵션에 따라 BinSkim 문제가 발견 되 면 빌드를 중단 합니다.
| 불균형 | 선택 목록 | AllTools = true 또는 BinSkim = true | True | Error | 오류, WarningAbove | 빌드를 중단할 문제 수준입니다.
| CredScan | boolean | AllTools = false | True | false |  | 자격 증명 스캐너 문제가 발견 되 면 빌드를 중단 합니다.
| Rosl이상 분석기 | boolean | AllTools = false | True | false |  | Roslyn 분석기 문제가 발견 되 면 빌드를 중단 합니다.
| RoslynAnalyzersBreakOn | 선택 목록 | AllTools = true 또는 Rosl를 분석기 = true | True | Error | 오류, WarningAbove | 빌드를 중단할 문제 수준입니다.
| TSLint | boolean | AllTools = false | True | false |  | TSLint 문제가 발견 되 면 빌드를 중단 합니다. JSON 형식의 TSLint 로그만 사후 분석에 대해 지원 됩니다. 다른 형식을 선택한 경우에는 TSLint 빌드 작업을 적절 하 게 업데이트 하세요.
| Tslintor | 선택 목록 | AllTools = true 또는 TSLint = true | True | Error | 오류, WarningAbove | 빌드를 중단할 문제 수준입니다.
| VstsConsole | boolean | always | False | true |  | 파이프라인 콘솔에 결과를 씁니다.
| ToolLogsNotFoundAction | 선택 목록 | always | True | 표준 | 오류, 없음, 표준, 경고 | 도구를 실행 하지 않은 경우 선택 된 도구 (또는 모든 도구를 선택 하는 경우 도구)에 대 한 로그를 찾을 수 없는 경우 수행할 동작입니다.<br/><br/>**옵션:**<br/>**없음:** VSTS 변수 **system.object** 를 **true**로 설정 하 여 액세스할 수 있는 자세한 정보 출력 스트림에 메시지가 기록 됩니다.<br/>**Standard:** (기본값) 도구에 대 한 로그를 찾을 수 없는 표준 출력 메시지를 기록 합니다.<br/>**경고:** 빌드 요약 페이지에 경고로 표시 되는, 도구에 대 한 로그를 찾지 못한 노란색 경고 메시지를 씁니다.<br/>**오류:** 빨간색 오류 메시지를 기록 하 고 빌드를 중단 하는 예외를 throw 합니다. 이 옵션을 사용 하 여 개별 도구를 선택 하 여 실행 되는 도구를 확인 합니다.

## <a name="next-steps"></a>다음 단계

보안 코드 분석 확장 및 제공 된 도구에 대 한 추가 질문이 있는 경우 [FAQ 페이지](security-code-analysis-faq.md)를 확인 하세요.