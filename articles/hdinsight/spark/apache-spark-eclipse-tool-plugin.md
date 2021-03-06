---
title: 'Azure Toolkit for Eclipse: HDInsight Spark 용 Scala apps 만들기'
description: Azure Toolkit for Eclipse의 HDInsight Tools를 사용하여 Scala로 작성된 Spark 애플리케이션을 개발한 후에 Eclipse IDE에서 직접 HDInsight Spark 클러스터로 제출합니다.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: how-to
ms.custom: hdinsightactive
ms.date: 12/13/2019
ms.openlocfilehash: 33cbb9b5ac754969a6a9038db227123bae3a0ea7
ms.sourcegitcommit: 28c93f364c51774e8fbde9afb5aa62f1299e649e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/30/2020
ms.locfileid: "97822406"
---
# <a name="use-azure-toolkit-for-eclipse-to-create-apache-spark-applications-for-an-hdinsight-cluster"></a>Azure Toolkit for Eclipse를 사용하여 HDInsight 클러스터용 Apache Spark 애플리케이션 만들기

Azure Toolkit for [Eclipse](https://www.eclipse.org/)의 HDInsight Tools를 사용하여 [Scala](https://www.scala-lang.org/)로 작성된 [Apache Spark](https://spark.apache.org/) 애플리케이션을 개발하여 Eclipse IDE에서 직접 Azure HDInsight Spark 클러스터에 제출합니다. 다음과 같은 방법으로 HDInsight Tools 플러그 인을 사용할 수 있습니다.

* HDInsight Spark 클러스터에서 Scala Spark 애플리케이션을 개발 및 제출하려면
* Azure HDInsight Spark 클러스터 리소스에 액세스하려면
* Scala Spark 애플리케이션을 로컬로 개발 및 실행하려면

## <a name="prerequisites"></a>필수 구성 요소

* HDInsight의 Apache Spark 클러스터. 자세한 내용은 [Azure HDInsight에서 Apache Spark 클러스터 만들기](apache-spark-jupyter-spark-sql.md)를 참조하세요.

* [JDK (Java Developer Kit) 버전 8](/azure/developer/java/fundamentals/java-jdk-long-term-support)입니다.

* [ECLIPSE IDE](https://www.eclipse.org/downloads/). 이 문서에서는 Java 개발자를 위한 Eclipse IDE를 사용 합니다.

## <a name="install-required-plug-ins"></a>필요한 플러그 인 설치

### <a name="install-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트 설치

설치 지침은 [Eclipse용 Azure 도구 키트 설치](/azure/developer/java/toolkit-for-eclipse/installation)를 참조하세요.

### <a name="install-the-scala-plug-in"></a>Scala 플러그 인 설치

Eclipse를 열면 HDInsight Tools는 Scala 플러그 인을 설치했는지 여부를 자동으로 검색합니다. **확인** 을 선택하여 계속 진행한 다음 Eclipse Marketplace에서 해당 플러그 인을 설치하는 지침을 따릅니다. 설치가 완료 되 면 IDE를 다시 시작 합니다.

![Scala 플러그 인 자동 설치](./media/apache-spark-eclipse-tool-plugin/auto-installation-scala1.png)

### <a name="confirm-plug-ins"></a>플러그 인 확인

1. **도움말**  >  **Eclipse Marketplace** 로 이동 합니다.

1. **설치됨** 탭을 선택합니다.

1. 최소한 다음이 표시 되어야 합니다.
    * Azure Toolkit for Eclipse \<version> .
    * Scala IDE \<version> .

## <a name="sign-in-to-your-azure-subscription"></a>Azure 구독에 로그인합니다.

1. Eclipse IDE를 시작 합니다.

1. **창**  >   **보기**  >   다른  >  창으로 이동 ... **로그인**...

1. **보기 표시** 대화 상자에서 **azure**  >  **azure 탐색기** 로 이동 하 고 **열기** 를 선택 합니다.

   ![Eclipse 표시 Apache Spark 보기](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer1.png)

1. **Azure 탐색기** 에서 **azure** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **로그인** 을 선택 합니다.

1. **Azure 로그인** 대화 상자에서 인증 방법을 선택 하 고 **로그인** 을 선택 하 고 로그인 프로세스를 완료 합니다.

   ![Apache Spark Eclipse Azure Sign](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer2.png)

1. 로그인 한 후에는 **구독** 대화 상자에 자격 증명과 연결 된 모든 Azure 구독이 나열 됩니다. **선택** 을 클릭 하 여 대화 상자를 닫습니다.

   ![구독 선택 대화 상자](./media/apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)

1. **Azure 탐색기** 에서 **azure**  >   **hdinsight** 로 이동 하 여 구독에서 HDInsight Spark 클러스터를 확인 합니다.

   ![Azure Explorer3의 HDInsight Spark 클러스터](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer3.png)

1. 클러스터 이름 노드를 더 확장하여 클러스터와 연결된 리소스(예: 스토리지 계정)를 표시할 수 있습니다.

   ![클러스터 이름을 확장하여 리소스 표시](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer4.png)

## <a name="link-a-cluster"></a>클러스터 연결

Ambari 관리 사용자 이름을 사용하여 일반 클러스터를 연결할 수 있습니다. 마찬가지로, 도메인에 가입된 HDInsight 클러스터의 경우, `user1@contoso.com`과 같이 도메인 및 사용자 이름을 사용하여 연결할 수 있습니다.

1. **Azure 탐색기** 에서 **HDInsight** 를 마우스 오른쪽 단추로 클릭 하 고 **클러스터 연결** 을 선택 합니다.

   ![Azure 탐색기 링크 클러스터 메뉴](./media/apache-spark-eclipse-tool-plugin/link-a-cluster-context-menu.png)

1. **클러스터 이름**, **사용자 이름** 및 **암호** 를 입력 하 고 **확인** 을 선택 합니다. 선택적으로 스토리지 계정, 스토리지 키를 입력한 다음, Storage Explorer의 스토리지 컨테이너를 선택하여 왼쪽 트리 뷰에서 작업합니다.

   ![새 HDInsight 클러스터 연결 대화 상자](./media/apache-spark-eclipse-tool-plugin/link-cluster-dialog1.png)

   > [!NOTE]  
   > 클러스터가 Azure 구독 및 연결된 클러스터 모두에 로그인되어 있으면, 연결된 스토리지 키, 사용자 이름 및 암호를 사용합니다.
   > ![Azure Explorer 스토리지 계정](./media/apache-spark-eclipse-tool-plugin/storage-explorer-in-Eclipse.png)
   >
   > 키보드 전용 사용자의 경우 현재 포커스가 **저장소 키** 에 있는 경우 **Ctrl + TAB** 을 사용 하 여 대화 상자의 다음 필드에 포커스를 두어야 합니다.

1. **HDInsight** 에서 연결 된 클러스터를 볼 수 있습니다. 이제 애플리케이션을 연결된 클러스터에 제출할 수 있습니다.

   ![Azure Explorer hdi 연결 된 클러스터](./media/apache-spark-eclipse-tool-plugin/hdinsight-linked-cluster.png)

1. **Azure Explorer** 에서 클러스터 연결을 해제할 수도 있습니다.

   ![Azure Explorer에서 클러스터에 연결 해제](./media/apache-spark-eclipse-tool-plugin/hdi-unlinked-cluster.png)

## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에 Spark Scala 프로젝트 설정

1. Eclipse IDE 작업 영역에서 **파일**  >  **새로 만들기**  >  **프로젝트**...를 선택 합니다.

1. **새 프로젝트** 마법사에서 hdinsight의 hdinsight **프로젝트**  >  **Spark (Scala)** 를 선택 합니다. 그런 후 **다음** 을 선택합니다.

   ![HDInsight의 Spark(Scala) 프로젝트 선택](./media/apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)

1. **새 HDInsight Scala 프로젝트** 대화 상자에서 다음 값을 입력한 후 **다음** 을 선택합니다.
   * 프로젝트의 이름을 입력합니다.
   * **JRE** 영역에서 **JRE 실행 환경 사용** 을 **JavaSE-1.7** 이상으로 설정해야 합니다.
   * **Spark 라이브러리** 영역에서 **Maven을 사용하여 Spark SDK 구성** 옵션을 선택할 수 있습니다.  이 도구는 Spark SDK 및 Scala SDK에 대해 적합한 버전을 통합합니다. 수동으로 **SPARK Sdk 추가** 옵션, 다운로드 및 spark sdk 추가를 수동으로 선택할 수도 있습니다.

   ![새 HDInsight Scala 프로젝트 대화 상자](./media/apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)

1. 다음 대화 상자에서 세부 정보를 검토 한 다음 **마침** 을 선택 합니다.

## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>HDInsight Spark 클러스터에 대한 Scala 애플리케이션 만들기

1. **패키지 탐색기** 에서 앞서 만든 프로젝트를 확장 합니다. **Src** 를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**  >  ...를 **선택 합니다.**

1. **마법사 선택** 대화 상자에서 **Scala 마법사**  >  **Scala 개체** 를 선택 합니다. 그런 후 **다음** 을 선택합니다.

   ![마법사 선택 Scala 개체 만들기](./media/apache-spark-eclipse-tool-plugin/create-scala-project1.png)

1. **새 파일 만들기** 대화 상자에서 개체 이름을 입력한 다음 **마침** 을 선택합니다. 텍스트 편집기가 열립니다.

   ![새 파일 마법사 새 파일 만들기](./media/apache-spark-eclipse-tool-plugin/create-scala-project2.png)

1. 텍스트 편집기에서 현재 내용을 아래 코드로 바꿉니다.

    ```scala
    import org.apache.spark.SparkConf
    import org.apache.spark.SparkContext

    object MyClusterApp{
        def main (arg: Array[String]): Unit = {
        val conf = new SparkConf().setAppName("MyClusterApp")
        val sc = new SparkContext(conf)

        val rdd = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        //find the rows that have only one digit in the seventh column in the CSV
        val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

        rdd1.saveAsTextFile("wasbs:///HVACOut")
        }
    }
    ```

1. HDInsight Spark 클러스터에서 애플리케이션 실행:

   a. 패키지 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭한 다음 **HDInsight에 Spark 애플리케이션 제출** 을 선택합니다.

   b. **Spark 제출** 대화 상자에서 다음 값을 제공한 다음 **제출** 을 선택 합니다.

   * **클러스터 이름** 의 경우 애플리케이션을 실행하려는 HDInsight Spark 클러스터를 선택합니다.
   * Eclipse 프로젝트에서 아티팩트를 선택하거나 하드 디스크에서 아티팩트를 선택합니다. 기본값은 패키지 탐색기에서 마우스 오른쪽 단추로 클릭한 항목에 따라 달라집니다.
   * **기본 클래스 이름** 드롭다운 목록에서 제출 마법사에는 프로젝트의 모든 개체 이름이 표시됩니다. 실행하려는 이름을 선택하거나 입력합니다. 하드 드라이브에서 아티팩트를 선택한 경우 주 클래스 이름을 수동으로 입력해야 합니다. 
   * 이 예제의 응용 프로그램 코드에는 명령줄 인수나 참조 Jar 나 파일이 필요 하지 않으므로 나머지 텍스트 상자를 비워 둘 수 있습니다.

     ![Apache Spark 제출 대화 상자](./media/apache-spark-eclipse-tool-plugin/create-scala-project3.png)

1. **Spark 제출** 탭에 진행 상태가 표시되기 시작합니다. **Spark 제출** 창에서 빨간색 단추를 선택하여 애플리케이션을 중지할 수 있습니다. 구형 아이콘(이미지에 파란색 상자로 표시됨)을 선택하여 특정 애플리케이션을 실행하는 로그를 볼 수도 있습니다.

   ![Apache Spark 제출 창](./media/apache-spark-eclipse-tool-plugin/create-scala-project4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 HDInsight Spark 클러스터 액세스 및 관리

HDInsight Tools를 사용하여 작업 출력에 액세스를 포함한 다양한 작업을 수행할 수 있습니다.

### <a name="access-the-job-view"></a>작업 보기 액세스

1. **Azure 탐색기** 에서 **HDInsight**, Spark 클러스터 이름을 차례로 확장 한 다음 **작업** 을 선택 합니다.

   ![Azure 탐색기 Eclipse 작업 보기 노드](./media/apache-spark-eclipse-tool-plugin/eclipse-job-view-node.png)

1. **작업** 노드를 선택합니다. Java 버전이 **1.8** 보다 낮으면 HDInsight Tools가 자동으로 **E(fx)clipse** 플러그인 설치를 미리 알립니다. **확인** 을 선택하여 계속 진행한 다음 마법사에 따라 Eclipse Marketplace에서  Eclipse를 설치하고 다시 시작합니다.

   ![누락 된 플러그 인 E (fx) clipse 설치](./media/apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

1. **작업** 노드에서 작업 보기를 엽니다. 오른쪽 창의 **Spark 작업 보기** 탭에는 클러스터에서 실행된 모든 애플리케이션이 표시됩니다. 자세한 내용을 보려면 원하는 애플리케이션 이름을 선택합니다.

   ![Apache Eclipse 작업 로그 보기 세부 정보](./media/apache-spark-eclipse-tool-plugin/eclipse-view-job-logs.png)

   다음 작업 중 하나를 수행할 수 있습니다.

   * 작업 그래프로 마우스를 가져갑니다. 실행 중인 작업에 대한 기본 정보가 표시됩니다. 작업 그래프를 선택하면 모든 작업이 생성하는 단계 및 정보가 표시됩니다.

     ![Apache Spark 작업 그래프 단계 정보](./media/apache-spark-eclipse-tool-plugin/Job-graph-stage-info.png)

   * **드라이버 Stderr**, **드라이버 Stdout** 및 **디렉터리 정보** 와 같은 자주 사용되는 로그를 보려면 **로그** 탭을 선택합니다.

     ![Eclipse 작업 로그 정보 Apache Spark](./media/apache-spark-eclipse-tool-plugin/eclipse-job-log-info.png)

   * 창 맨 위에 있는 하이퍼링크를 선택하여 Spark 기록 UI 및 Apache Hadoop YARN UI(애플리케이션 수준)를 엽니다.

### <a name="access-the-storage-container-for-the-cluster"></a>클러스터에 대한 스토리지 컨테이너 액세스

1. Azure 탐색기에서 **HDInsight** 루트 노드를 확장하여 사용할 수 있는 HDInsight Spark 클러스터의 목록을 표시합니다.

1. 클러스터 이름을 확장하여 클러스터에 대한 스토리지 계정 및 기본 스토리지 컨테이너를 표시합니다.

   ![Storage 계정 및 기본 스토리지 컨테이너](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer5.png)

1. 클러스터와 연결된 스토리지 컨테이너 이름을 선택합니다. 오른쪽 창에서 **HVACOut** 폴더를 두 번 클릭합니다. **파트-** 파일 중 하나를 열어 애플리케이션의 출력을 표시합니다.

### <a name="access-the-spark-history-server"></a>Spark 기록 서버 액세스

1. Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **Spark 기록 UI 열기** 를 선택합니다. 메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다. 이러한 항목은 클러스터를 프로비전하는 동안 지정한 것입니다.

1. Spark 기록 서버 대시보드에서 애플리케이션 이름을 사용하여 방금 실행을 마친 애플리케이션을 찾을 수 있습니다. 위의 코드에서 `val conf = new SparkConf().setAppName("MyClusterApp")`을 사용하여 애플리케이션 이름을 설정합니다. 따라서 Spark 애플리케이션의 이름은 **MyClusterApp** 입니다.

### <a name="start-the-apache-ambari-portal"></a>Apache Ambari 포털 시작

1. Azure 탐색기에서 Spark 클러스터 이름을 마우스 오른쪽 단추로 클릭한 다음 **클러스터 관리 포털(Ambari) 열기** 를 선택합니다.

1. 메시지가 표시되면 클러스터에 대한 관리자 자격 증명을 입력합니다. 이러한 항목은 클러스터를 프로비전하는 동안 지정한 것입니다.

### <a name="manage-azure-subscriptions"></a>Azure 구독 관리

기본적으로 Eclipse용 Azure 도구 키트의 HDInsight Tool에는 모든 Azure 구독의 Spark 클러스터가 나열됩니다. 필요한 경우 클러스터에 액세스하려는 구독을 지정할 수 있습니다.

1. Azure 탐색기에서 **Azure** 루트 노드를 마우스 오른쪽 단추로 클릭한 다음 **구독 관리** 를 선택합니다.

1. 대화 상자에서 액세스하지 않으려는 구독의 확인란 선택을 취소하고 **닫기** 를 선택합니다. Azure 구독에서 로그아웃하려는 경우 **로그아웃** 을 선택할 수도 있습니다.

## <a name="run-a-spark-scala-application-locally"></a>로컬로 Spark Scala 애플리케이션 실행

Eclipse용 Azure 도구 키트의 HDInsight Tools를 사용하여 워크스테이션에서 Spark Scala 애플리케이션을 로컬로 실행할 수 있습니다. 일반적으로 이러한 애플리케이션은 스토리지 컨테이너와 같은 클러스터 리소스에 액세스할 필요가 없으므로 로컬로 실행하고 테스트할 수 있습니다.

### <a name="prerequisite"></a>필수 요소

Windows 컴퓨터에서 로컬 Spark Scala 응용 프로그램을 실행 하는 동안 [Spark-2356](https://issues.apache.org/jira/browse/SPARK-2356)에 설명 된 예외를 받을 수 있습니다. 이 예외는 Windows에 **WinUtils.exe** 가 없기 때문에 발생합니다.

이 오류를 해결 하려면 **C:\WinUtils\bin** 와 같은 위치에 [Winutils.exe](https://github.com/steveloughran/winutils) 한 다음 **HADOOP_HOME** 환경 변수를 추가 하 고 변수 값을 **C\WinUtils** 로 설정 해야 합니다.

### <a name="run-a-local-spark-scala-application"></a>로컬 Spark Scala 애플리케이션 실행

1. Eclipse를 시작하고 프로젝트를 만듭니다. **새 프로젝트** 대화 상자에서 다음과 같이 선택하고 **다음** 을 선택합니다.

1. **새 프로젝트** 마법사에서 hdinsight **Project**  >  **Spark on hdinsight 로컬 실행 샘플 (Scala)** 을 선택 합니다. 그런 후 **다음** 을 선택합니다.

   ![새 프로젝트 마법사 대화 상자 선택](./media/apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)

1. 프로젝트 세부 정보를 제공하려면 이전의 [HDInsight Spark 클러스터용 Spark Scala 프로젝트 설정](#set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster) 섹션의 3-6단계를 따릅니다.

1. 템플릿은 컴퓨터에서 로컬로 실행할 수 있는 샘플 코드(**LogQuery**)를 **src** 폴더 아래에 추가합니다.

   ![LogQuery 로컬 scala 응용 프로그램의 위치](./media/apache-spark-eclipse-tool-plugin/local-scala-application.png)

1. **Logquery** 를 마우스 오른쪽 단추로 클릭 하 고 **실행**  >  **1 scala 응용 프로그램** 을 선택 합니다. **콘솔** 탭에 다음과 같은 출력이 표시됩니다.

   ![Spark 애플리케이션 로컬 실행 결과](./media/apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="reader-only-role"></a>독자 전용 역할

사용자가 판독기 전용 역할 권한이 있는 클러스터에 작업을 제출하는 경우, Ambari 자격 증명이 필요합니다.

### <a name="link-cluster-from-context-menu"></a>상황에 맞는 메뉴에서 클러스터 연결

1. 독자 전용 역할 계정으로 로그인합니다.

2. **Azure 탐색기** 에서 **HDInsight** 를 확장하여 구독에 포함된 HDInsight 클러스터를 표시합니다. **"Role:Reader"** 표시가 있는 클러스터에는 판독기 전용 역할 권한만 있습니다.

    ![Azure 탐색기 역할 판독기의 HDInsight Spark 클러스터](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer6.png)

3. 판독기 전용 역할 권한이 있는 클러스터를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **Link this cluster**(이 클러스터 연결)를 선택하여 클러스터를 연결합니다. Ambari 사용자 이름 및 암호를 입력 합니다.

    ![Azure 탐색기 링크의 HDInsight Spark 클러스터](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer7.png)

4. 클러스터가 연결되면 HDInsight가 새로 고쳐집니다.
   클러스터의 단계가 연결됨으로 변경됩니다.
  
    ![Azure 탐색기에서 HDInsight Spark 클러스터 연결](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer8.png)

### <a name="link-cluster-by-expanding-jobs-node"></a>작업 노드를 확장하여 클러스터 연결

1. **작업** 노드를 클릭하면 **Cluster Job Access Denied**(클러스터 작업 액세스 거부됨) 창이 표시됩니다.

2. **Link this cluster**(이 클러스터 연결)를 클릭하여 클러스터를 연결합니다.

    ![Azure Explorer9의 HDInsight Spark 클러스터](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer9.png)

### <a name="link-cluster-from-spark-submission-window"></a>Spark 제출 창에서 클러스터 연결

1. HDInsight 프로젝트를 만듭니다.

2. 패키지를 마우스 오른쪽 단추로 클릭 합니다. 그런 다음 **HDInsight에 Spark 응용 프로그램 제출을** 선택 합니다.

   ![Azure 탐색기에서 HDInsight Spark 클러스터 전송](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer11.png)

3. **클러스터 이름** 에 대 한 읽기 전용 역할 권한이 있는 클러스터를 선택 합니다. 경고 메시지가 표시 됩니다. **이 클러스터에 연결** 을 클릭 하 여 클러스터에 연결할 수 있습니다.

   ![Azure 탐색기에서 HDInsight Spark 클러스터이 링크](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer15.png)

### <a name="view-storage-accounts"></a>스토리지 계정 보기

* 판독기 전용 역할 권한이 있는 클러스터에 대해 **스토리지 계정** 노드를 클릭하면 **Storage Access Denied**(스토리지 계정 거부됨) 창이 표시됩니다.

   ![Azure 탐색기 저장소의 HDInsight Spark 클러스터](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer13.png)

   ![Azure 탐색기에서 HDInsight Spark 클러스터 거부 됨](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer12.png)

* 연결된 클러스터에 대해 **스토리지 계정** 노드를 클릭하면 **Storage Access Denied**(스토리지 계정 거부됨) 창이 표시됩니다.

   ![Azure 탐색기에서 HDInsight Spark 클러스터 denied2](./media/apache-spark-eclipse-tool-plugin/eclipse-view-explorer14.png)

## <a name="known-problems"></a>알려진 문제

**클러스터 링크** 를 사용 하는 경우 저장소의 자격 증명을 제공 하는 것이 좋습니다.

![저장소 자격 증명을 사용 하 여 클러스터 연결 eclipses](./media/apache-spark-eclipse-tool-plugin/link-cluster-with-storage-credential-eclipse.png)

작업을 제출하는 두 가지 모드가 있습니다. 스토리지 자격 증명을 제공하는 경우 작업을 제출하는 데 일괄 처리 모드가 사용됩니다. 그렇지 않으면 대화형 모드가 사용됩니다. 클러스터가 사용 중인 경우 아래 오류가 발생할 수 있습니다.

![클러스터가 사용 중인 경우 Eclipse에 오류가 발생합니다.](./media/apache-spark-eclipse-tool-plugin/eclipse-interactive-cluster-busy-upload.png "클러스터가 사용 중인 경우 Eclipse에 오류가 발생합니다.")

![클러스터 사용량이 yarn 때 eclipse 가져오기 오류](./media/apache-spark-eclipse-tool-plugin/eclipse-interactive-cluster-busy-submit.png "클러스터 사용량이 yarn 때 eclipse 가져오기 오류")

## <a name="see-also"></a>참조

* [개요: Azure HDInsight의 Apache Spark](apache-spark-overview.md)

### <a name="scenarios"></a>시나리오

* [BI와 Apache Spark: BI 도구와 함께 HDInsight의 Spark를 사용하여 대화형 데이터 분석 수행](apache-spark-use-bi-tools.md)
* [Machine Learning과 Apache Spark: HVAC 데이터를 사용하여 건물 온도를 분석하는 데 HDInsight의 Spark 사용](apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning과 Apache Spark: HDInsight의 Spark를 사용하여 식품 검사 결과 예측](apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight의 Apache Spark를 사용한 웹 사이트 로그 분석](apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>애플리케이션 만들기 및 실행

* [Scala를 사용하여 독립 실행형 애플리케이션 만들기](apache-spark-create-standalone-application.md)
* [Apache Livy를 사용하여 Apache Spark 클러스터에서 원격으로 작업 실행](apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>도구 및 확장

* [IntelliJ용 Azure 도구 키트를 사용하여 Spark Scala 애플리케이션 만들기 및 제출](apache-spark-intellij-tool-plugin.md)
* [Azure Toolkit for IntelliJ를 사용하여 VPN을 통해 원격으로 Apache Spark 애플리케이션 디버그](./apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Azure Toolkit for IntelliJ를 사용하여 SSH를 통해 원격으로 Apache Spark 애플리케이션 디버그](./apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [HDInsight에서 Apache Spark 클러스터와 함께 Apache Zeppelin Notebook 사용](apache-spark-zeppelin-notebook.md)
* [HDInsight 용 Apache Spark 클러스터의 Jupyter Notebook에 사용할 수 있는 커널](apache-spark-jupyter-notebook-kernels.md)
* [Jupyter 노트북에서 외부 패키지 사용](apache-spark-jupyter-notebook-use-external-packages.md)
* [컴퓨터에 Jupyter를 설치하고 HDInsight Spark 클러스터에 연결](apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>리소스 관리

* [Azure HDInsight에서 Apache Spark 클러스터에 대한 리소스 관리](apache-spark-resource-manager.md)
* [HDInsight의 Apache Spark 클러스터에서 실행되는 작업 추적 및 디버그](apache-spark-job-debugging.md)