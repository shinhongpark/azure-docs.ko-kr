---
title: SQL-Azure Monitor 로그 쿼리 참고 자료 | Microsoft Docs
description: Azure Monitor에서 로그 쿼리를 작성하는 데 SQL에 익숙한 사용자를 위한 도움말입니다.
ms.subservice: logs
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 08/21/2018
ms.openlocfilehash: e9f937323f4e14b5c8c3f30c94bf9d2daef0baea
ms.sourcegitcommit: e15c0bc8c63ab3b696e9e32999ef0abc694c7c41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97606694"
---
# <a name="sql-to-azure-monitor-log-query-cheat-sheet"></a>SQL-Azure Monitor 로그 쿼리 참고 자료 

아래 표는 SQL에 익숙한 사용자가 Azure Monitor에서 로그 쿼리를 작성하기 위한 Kusto 쿼리 언어를 알아보는 데 도움이 됩니다. 일반적인 시나리오를 해결 하기 위한 T-sql 명령과 Azure Monitor 로그 쿼리에서 해당 하는 항목을 살펴봅니다.

## <a name="sql-to-azure-monitor"></a>SQL-Azure Monitor

Description |SQL 쿼리 | Azure Monitor 로그 쿼리
----------------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------
테이블에서 모든 데이터 선택 |`SELECT * FROM dependencies` |<code>dependencies</code>
테이블에서 특정 열 선택 |`SELECT name, resultCode FROM dependencies` |<code>dependencies <br>&#124; project name, resultCode</code>
테이블에서 100개의 레코드 선택 |`SELECT TOP 100 * FROM dependencies` |<code>dependencies <br>&#124; take 100</code>
Null 평가 |`SELECT * FROM dependencies WHERE resultCode IS NOT NULL` |<code>dependencies <br>&#124; where isnotnull(resultCode)</code>
문자열 비교: 같음 |`SELECT * FROM dependencies WHERE name = "abcde"` |<code>dependencies <br>&#124; where name == "abcde"</code>
문자열 비교: 하위 문자열 |`SELECT * FROM dependencies WHERE name like "%bcd%"` |<code>dependencies <br>&#124; where name contains "bcd"</code>
문자열 비교: 와일드 카드 |`SELECT * FROM dependencies WHERE name like "abc%"` |<code>dependencies <br>&#124; where name startswith "abc"</code>
날짜 비교: 최근 1일 |`SELECT * FROM dependencies WHERE timestamp > getdate()-1` |<code>dependencies <br>&#124; where timestamp > ago(1d)</code>
날짜 비교: 날짜 범위 |`SELECT * FROM dependencies WHERE timestamp BETWEEN '2016-10-01' AND '2016-11-01'` |<code>dependencies <br>&#124; where timestamp between (datetime(2016-10-01) .. datetime(2016-10-01))</code>
부울 비교 |`SELECT * FROM dependencies WHERE !(success)` |<code>dependencies <br>&#124; where success == "False" </code>
정렬 |`SELECT name, timestamp FROM dependencies ORDER BY timestamp asc` |<code>dependencies <br>&#124; order by timestamp asc </code>
Distinct |`SELECT DISTINCT name, type  FROM dependencies` |<code>dependencies <br>&#124; summarize by name, type </code>
그룹화, 집계 |`SELECT name, AVG(duration) FROM dependencies GROUP BY name` |<code>dependencies <br>&#124; summarize avg(duration) by name </code>
열 별칭, 확장 |`SELECT operation_Name as Name, AVG(duration) as AvgD FROM dependencies GROUP BY name` |<code>dependencies <br>&#124; summarize AvgD=avg(duration) by operation_Name <br>&#124; project Name=operation_Name, AvgD</code>
측정값 별 상위 n 개 레코드 |`SELECT TOP 100 name, COUNT(*) as Count FROM dependencies GROUP BY name ORDER BY Count asc` |<code>dependencies <br>&#124; summarize Count=count() by name <br>&#124; top 100 by Count asc</code>
Union |`SELECT * FROM dependencies UNION SELECT * FROM exceptions` |<code>union dependencies, exceptions</code>
통합: 조건 사용 |`SELECT * FROM dependencies WHERE value > 4 UNION SELECT * FROM exceptions WHERE value < 5` |<code>dependencies <br>&#124; where value > 4 <br>&#124; union (exceptions <br>&#124; where value < 5)</code>
Join |`SELECT * FROM dependencies JOIN exceptions ON dependencies.operation_Id = exceptions.operation_Id`|<code>dependencies <br>&#124; join (exceptions) on operation_Id == operation_Id</code>


## <a name="next-steps"></a>다음 단계

- [Azure Monitor에서 로그 쿼리 작성](get-started-queries.md)에 대 한 단원을 참조 하세요.
