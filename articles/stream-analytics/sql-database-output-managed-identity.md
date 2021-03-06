---
title: 관리 되는 id를 사용 하 여 Azure SQL Database 또는 Azure Synapse Analytics에 액세스-Azure Stream Analytics
description: 이 문서에서는 관리 되는 id를 사용 하 여 Azure SQL Database 또는 Azure Synapse Analytics 출력에 Azure Stream Analytics 작업을 인증 하는 방법을 설명 합니다.
author: enkrumah
ms.author: ebnkruma
ms.service: stream-analytics
ms.topic: how-to
ms.date: 11/30/2020
ms.openlocfilehash: 7d624f2dd2c0c9b4c7e99d5628a1d47e4303da7f
ms.sourcegitcommit: 6628bce68a5a99f451417a115be4b21d49878bb2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2021
ms.locfileid: "98555596"
---
# <a name="use-managed-identities-to-access-azure-sql-database-or-azure-synapse-analytics-from-an-azure-stream-analytics-job-preview"></a>관리 되는 id를 사용 하 여 Azure Stream Analytics 작업에서 Azure SQL Database 또는 Azure Synapse Analytics에 액세스 (미리 보기)

Azure Stream Analytics Azure SQL Database 및 Azure Synapse Analytics 출력 싱크에 대해 [관리 id 인증](../active-directory/managed-identities-azure-resources/overview.md) 을 지원 합니다. 관리 ID를 사용하면 암호를 변경할 때 재인증해야 하거나 90일마다 사용자 토큰이 만료되는 등의 사용자 기반 인증 방법의 제한이 사라집니다. 수동으로 인증할 필요가 없어지면 Stream Analytics 배포를 완전히 자동화할 수 있습니다.

관리 ID는 지정된 Stream Analytics 작업을 나타내는 Azure Active Directory에 등록된 관리형 애플리케이션입니다. 관리형 애플리케이션은 대상 리소스에 인증하는 데 사용됩니다. 이 문서에서는 Azure Portal를 통해 Stream Analytics 작업의 Azure SQL Database 또는 Azure Synapse Analytics 출력에 대해 관리 되는 Id를 사용 하도록 설정 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

#### <a name="azure-sql-database"></a>[Azure SQL Database](#tab/azure-sql)

이 기능을 사용 하려면 다음이 필요 합니다.

- Azure Stream Analytics 작업

- Azure SQL Database 리소스

#### <a name="azure-synapse-analytics"></a>[Azure Synapse Analytics](#tab/azure-synapse)

이 기능을 사용 하려면 다음이 필요 합니다.

- Azure Stream Analytics 작업

- Azure Synapse Analytics SQL 풀.

- [Stream Analytics 작업으로 구성](azure-synapse-analytics-output.md)된 Azure Storage 계정

---

## <a name="create-a-managed-identity"></a>관리 ID 만들기

먼저 Azure Stream Analytics 작업의 관리 ID를 만듭니다.

1. [Azure Portal](https://portal.azure.com)에서 Stream Analytics 작업을 엽니다.

1. 왼쪽 탐색 메뉴의 **구성** 아래에서 **관리 ID** 를 선택합니다. 그런 다음, **시스템 할당 관리 ID 사용** 옆에 있는 확인란을 선택하고 **저장** 을 선택합니다.

   ![시스템 할당 관리 ID 선택](./media/sql-db-output-managed-identity/system-assigned-managed-identity.png)

   Azure Active Directory에서 Stream Analytics 작업의 ID에 대한 서비스 주체가 생성됩니다. 새로 생성된 ID의 수명 주기는 Azure에서 관리합니다. Stream Analytics 작업을 삭제하면 연결된 ID(즉, 서비스 주체)는 Azure에서 자동으로 삭제합니다.

1. 구성을 저장하면 서비스 주체의 OID(개체 ID)가 아래와 같이 보안 주체 ID로 나열됩니다. 

   ![보안 주체 ID로 표시되는 개체 ID](./media/sql-db-output-managed-identity/principal-id.png)

   서비스 주체에는 Stream Analytics 작업과 동일한 이름이 사용됩니다. 예를 들어 작업 이름이 *MyASAJob* 이면 서비스 주체 이름도 *MyASAJob* 이 됩니다.

## <a name="select-an-active-directory-admin"></a>Active Directory 관리자 선택

관리 ID를 만든 후에는 Active Directory 관리자를 선택합니다.

1. Azure SQL Database 또는 Azure Synapse Analytics 리소스로 이동 하 고 데이터베이스가 있는 SQL Server를 선택 합니다. 리소스 개요 페이지의 *서버 이름* 옆에서 SQL Server 이름을 찾을 수 있습니다.

1. **설정** 에서 **Active Directory 관리자** 를 선택합니다. 그런 다음, **관리자 설정** 을 선택합니다.

   ![Active Directory 관리자 페이지](./media/sql-db-output-managed-identity/active-directory-admin-page.png)

1. Active Directory 관리자 페이지에서 SQL Server의 관리자가 될 사용자 또는 그룹을 검색하고 **선택** 을 클릭합니다.

   ![Active Directory 관리자 추가](./media/sql-db-output-managed-identity/add-admin.png)

   Active Directory 관리 페이지에 해당 Active Directory에 모든 멤버와 그룹이 표시됩니다. 회색으로 표시 된 사용자 또는 그룹은 Azure Active Directory 관리자로 지원 되지 않으므로 선택할 수 없습니다.  ****    [SQL Database 또는 Azure Synapse 인증에 대 한 Azure Active Directory 인증 사용](../azure-sql/database/authentication-aad-overview.md#azure-ad-features-and-limitations)의 Azure Active Directory 기능 및 제한 사항 섹션에서 지원 되는 관리자 목록을 참조 하세요. Azure RBAC (역할 기반 액세스 제어)는 포털에만 적용 되 고 SQL Server로 전파 되지 않습니다. 또한 선택한 사용자 또는 그룹은 다음 섹션에서 **포함된 데이터베이스 사용자** 를 만들 수 있는 사용자입니다.

1. **Active Directory 관리자** 페이지에서 **저장** 을 선택합니다. 관리자를 변경하는 프로세스는 몇 분 정도 걸립니다.

   Azure Active Directory 관리자를 설정 하면 새 관리자 이름 (사용자 또는 그룹)이 가상 주 데이터베이스에 SQL Server 인증 사용자로 표시 되지 않습니다. 표시 되는 경우 Azure Active Directory 관리자 설치 프로그램은 실패 하 고 관리자 (이름)가 이미 있음을 나타내는 만들기를 롤백합니다. SQL Server 인증 사용자는 Azure Active Directory의 일부가 아니므로 Azure Active Directory 인증을 사용 하 여 서버에 연결 하는 데 필요한 작업은 실패 합니다. 

## <a name="create-a-contained-database-user"></a>포함된 데이터베이스 사용자 만들기

다음으로 Azure Active Directory id에 매핑되는 azure SQL 또는 Azure Synapse 데이터베이스에 포함 된 데이터베이스 사용자를 만듭니다. 포함 된 데이터베이스 사용자에 게는 주 데이터베이스에 대 한 로그인이 없지만 데이터베이스와 연결 된 디렉터리의 id에 매핑됩니다. Azure Active Directory ID는 개별 사용자 계정 또는 그룹일 수 있습니다. 이 경우 Stream Analytics 작업에 대한 포함된 데이터베이스 사용자를 만들어야 합니다. 

1. SQL Server Management Studio를 사용 하 여 Azure SQL 또는 Azure Synapse 데이터베이스에 연결 합니다. **사용자 이름** 은 **ALTER ANY USER** 권한이 있는 Azure Active Directory 사용자입니다. SQL Server에서 설정하는 관리자를 예로 들 수 있습니다. **Azure Active Directory - MFA가 지원되는 유니버설** 인증을 사용합니다. 

   ![SQL Server에 연결](./media/sql-db-output-managed-identity/connect-sql-server.png)

   서버 이름 `<SQL Server name>.database.windows.net`은 지역에 따라 달라질 수 있습니다. 예를 들어 중국 지역은 `<SQL Server name>.database.chinacloudapi.cn`을 사용해야 합니다.
 
   **데이터베이스에 연결 > 연결 속성 > 옵션** 으로 이동 하 여 특정 azure SQL 또는 azure Synapse 데이터베이스를 지정할 수 있습니다.  

   ![SQL Server 연결 속성](./media/sql-db-output-managed-identity/sql-server-connection-properties.png)

1. 처음으로 연결하면 다음 창이 표시될 수 있습니다.

   ![새 방화벽 규칙 창](./media/sql-db-output-managed-identity/new-firewall-rule.png)

   1. 창의 내용이 맞으면 Azure Portal에서 SQL 서버 리소스로 이동합니다. **보안** 섹션에서 **방화벽 및 가상 네트워크** 페이지를 엽니다. 
   1. 원하는 규칙 이름을 사용하여 새 규칙을 추가합니다.
   1. **새 방화벽 규칙** 창의 *시작* IP 주소를 *시작 IP* 로 사용합니다.
   1. **새 방화벽 규칙** 창의 *끝* IP 주소를 *끝 IP* 로 사용합니다. 
   1. **저장** 을 선택하고 SQL Server Management Studio에서 다시 연결을 시도합니다. 

1. 연결 되 면 포함 된 데이터베이스 사용자를 만듭니다. 다음 SQL 명령은 Stream Analytics 작업과 동일한 이름을 사용하는 포함된 데이터베이스 사용자를 만듭니다. *ASA_JOB_NAME* 을 대괄호를 묶어야 합니다. 다음 T-SQL 구문을 사용하여 쿼리를 실행합니다. 

   ```sql
   CREATE USER [ASA_JOB_NAME] FROM EXTERNAL PROVIDER; 
   ```

1. Microsoft Azure Active Directory에서 Stream Analytics 작업이 SQL Database에 액세스했는지 확인하려면 데이터베이스와 통신할 Azure Active Directory 권한을 부여해야 합니다. 이렇게 하려면 Azure Portal의 "방화벽 및 가상 네트워크" 페이지로 이동 하 고 "Azure 서비스 및 리소스에서이 서버에 액세스할 수 있도록 허용"을 사용 하도록 설정 합니다. 

   ![방화벽 및 가상 네트워크](./media/sql-db-output-managed-identity/allow-access.png)

## <a name="grant-stream-analytics-job-permissions"></a>Stream Analytics 작업 권한 부여

#### <a name="azure-sql-database"></a>[Azure SQL Database](#tab/azure-sql)

이전 섹션에 설명 된 것 처럼 포함 된 데이터베이스 사용자를 만들고 포털에서 Azure 서비스에 대 한 액세스 권한을 부여 하면 Stream Analytics 작업에 관리 id를 통해 Azure SQL database 리소스에 **연결할** 수 있는 권한이 관리 되는 id로 포함 됩니다. 나중에 Stream Analytics 워크플로에서 필요하므로 Stream Analytics 작업에 대한 SELECT 및 INSERT 권한을 부여하는 것이 좋습니다. **SELECT** 권한을 통해 작업은 Azure SQL database의 테이블에 대 한 연결을 테스트할 수 있습니다. 입력 및 Azure SQL database 출력을 구성한 후에는 **INSERT** 권한을 사용 하 여 종단 간 Stream Analytics 쿼리를 테스트할 수 있습니다.

#### <a name="azure-synapse-analytics"></a>[Azure Synapse Analytics](#tab/azure-synapse)

이전 섹션에 설명 된 것 처럼 포함 된 데이터베이스 사용자를 만들고 포털에서 Azure 서비스에 대 한 액세스 권한을 부여 하면 Stream Analytics 작업에 관리 id를 통해 Azure Synapse 데이터베이스 리소스에 **연결할** 수 있는 권한이 관리 되는 id로 포함 됩니다. Stream Analytics 작업에 대 한 선택, 삽입 및 관리 데이터베이스 대량 작업을 추가 하는 것이 좋습니다 .이 작업은 나중에 Stream Analytics 워크플로에서 필요 하기 때문입니다. **SELECT** 권한을 사용 하면 작업에서 Azure Synapse 데이터베이스의 테이블에 대 한 연결을 테스트할 수 있습니다. **데이터베이스 대량 작업** **삽입** 및 관리 권한을 통해 입력 및 Azure Synapse 데이터베이스 출력을 구성한 후에는 종단 간 Stream Analytics 쿼리를 테스트할 수 있습니다.

데이터베이스 대량 작업 관리 권한을 부여 하려면 Stream Analytics 작업에 대 한 [데이터베이스 사용 권한을 포함](/sql/t-sql/statements/grant-database-permissions-transact-sql?view=azure-sqldw-latest&preserve-view=true#remarks) 하는 **컨트롤** 로 레이블이 지정 된 모든 사용 권한을 부여 해야 합니다. Stream Analytics 작업에서 COPY 문을 수행 하기 때문에이 권한이 필요 합니다. 여기에는 [데이터베이스 대량 작업 및 삽입](/sql/t-sql/statements/copy-into-transact-sql)이 필요 합니다.

---

SQL Server Management Studio를 사용하여 Stream Analytics 작업에 이러한 권한을 부여할 수 있습니다. 자세한 내용은 GRANT(Transact-SQL) 참조를 확인하세요.

데이터베이스의 특정 테이블 또는 개체에만 권한을 부여하려면 다음 T-SQL 구문을 사용하고 쿼리를 실행합니다. 

#### <a name="azure-sql-database"></a>[Azure SQL Database](#tab/azure-sql)

```sql
GRANT SELECT, INSERT ON OBJECT::TABLE_NAME TO ASA_JOB_NAME;
```

#### <a name="azure-synapse-analytics"></a>[Azure Synapse Analytics](#tab/azure-synapse)

```sql
GRANT [PERMISSION NAME] OBJECT::TABLE_NAME TO ASA_JOB_NAME;
```

---

또는 SQL Server Management Studio에서 Azure SQL 또는 Azure Synapse 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **속성 > 사용 권한** 을 선택할 수 있습니다. 권한 메뉴에서 이전에 추가한 Stream Analytics 작업을 볼 수 있으며, 필요에 따라 수동으로 권한을 부여하거나 거부할 수 있습니다.

## <a name="create-an-azure-sql-database-or-azure-synapse-output"></a>Azure SQL Database 또는 Azure Synapse 출력 만들기

#### <a name="azure-sql-database"></a>[Azure SQL Database](#tab/azure-sql)

관리 id를 구성 했으므로 이제 Stream Analytics 작업에 Azure SQL Database 또는 Azure Synapse 출력을 추가할 준비가 되었습니다.

적절한 출력 스키마를 사용하여 SQL Database에 테이블을 만들었는지 확인합니다. 이 테이블의 이름은 Stream Analytics 작업에 SQL Database 출력을 추가할 때 작성해야 하는 필수 속성 중 하나입니다. 또한 연결을 테스트하고 Stream Analytics 쿼리를 실행하기 위한 **SELECT** 및 **INSERT** 권한이 작업에 있는지 확인합니다. 아직 수행하지 않은 경우 [Stream Analytics 작업 권한 부여](#grant-stream-analytics-job-permissions) 섹션을 참조하세요. 

1. Stream Analytics 작업으로 돌아가서 **작업 토폴로지** 에서 **출력** 페이지로 이동합니다. 

1. **추가 > SQL Database** 를 선택합니다. SQL Database 출력 싱크의 출력 속성 창에서 인증 모드 드롭다운을 클릭하고 **관리 ID** 를 선택합니다.

1. 나머지 속성을 입력합니다. SQL Database 출력을 만드는 방법에 대한 자세한 내용은 [Stream Analytics를 사용하여 SQL Database 출력 만들기](sql-database-output.md)를 참조하세요. 작업을 마쳤으면 **저장** 을 선택합니다.

#### <a name="azure-synapse-analytics"></a>[Azure Synapse Analytics](#tab/azure-synapse)

이제 관리 되는 id 및 저장소 계정이 구성 되었으므로 Stream Analytics 작업에 Azure SQL Database 또는 Azure Synapse 출력을 추가할 준비가 되었습니다.

적절 한 출력 스키마를 사용 하 여 Azure Synapse 데이터베이스에 테이블을 만들었는지 확인 합니다. 이 테이블의 이름은 Stream Analytics 작업에 Azure Synapse 출력을 추가할 때 채워야 하는 필수 속성 중 하나입니다. 또한 연결을 테스트하고 Stream Analytics 쿼리를 실행하기 위한 **SELECT** 및 **INSERT** 권한이 작업에 있는지 확인합니다. 아직 수행하지 않은 경우 [Stream Analytics 작업 권한 부여](#grant-stream-analytics-job-permissions) 섹션을 참조하세요.

1. Stream Analytics 작업으로 돌아가서 **작업 토폴로지** 에서 **출력** 페이지로 이동합니다.

1. **추가 > Azure Synapse Analytics** 를 선택 합니다. SQL Database 출력 싱크의 출력 속성 창에서 인증 모드 드롭다운을 클릭하고 **관리 ID** 를 선택합니다.

1. 나머지 속성을 입력합니다. Azure Synapse output을 만드는 방법에 대 한 자세한 내용은 [Azure Stream Analytics의 Azure Synapse Analytics 출력](azure-synapse-analytics-output.md)을 참조 하세요. 작업을 마쳤으면 **저장** 을 선택합니다.

---

## <a name="remove-managed-identity"></a>관리 Id 제거

Stream Analytics 작업에 대해 생성 된 관리 Id는 작업이 삭제 된 경우에만 삭제 됩니다. 작업을 삭제 하지 않고 관리 되는 Id를 삭제할 수 있는 방법은 없습니다. 관리 Id를 더 이상 사용 하지 않으려는 경우에는 출력에 대 한 인증 방법을 변경할 수 있습니다. 관리 id는 작업이 삭제 될 때까지 계속 존재 하며 관리 되는 Id 인증을 다시 사용 하도록 결정 한 경우에 사용 됩니다.

## <a name="next-steps"></a>다음 단계

* [Azure Stream Analytics의 출력 이해](stream-analytics-define-outputs.md)
* [Azure SQL Database에 Azure Stream Analytics 출력](stream-analytics-sql-output-perf.md)
* [Azure Stream Analytics의 Azure Synapse Analytics 출력](azure-synapse-analytics-output.md)
