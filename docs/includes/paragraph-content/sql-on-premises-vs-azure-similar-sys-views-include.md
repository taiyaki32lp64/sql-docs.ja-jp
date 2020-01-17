---
ms.openlocfilehash: 6fd7bb2b8be38becc87c4dc8cb353594459a8dd6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68220159"
---

<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

オンプレミスの SQL Server 向けに作成された一部の Transact-SQL コード例は、クラウドの Azure SQL Database サービスで実行する場合は少し変更する必要があります。 このようなコード例の 1 つのカテゴリには、2 つのデータベース システム間で名前のプレフィックスがわずかに異なるシステム ビューが含まれています。

- **server\_** &nbsp; - &nbsp; _オンプレミスのプレフィックス_
- **database\_** &nbsp; - &nbsp; _クラウド内の Azure SQL DB サービスのプレフィックス_

説明のために、次の表に、システム ビューの 2 つのサブセットの比較リストを示します。 簡潔にするために、サブセットは、文字列 `_event` も含むビュー名に限定されています。 2 つの異なるデータベース システムに由来するため、サブセットの名前のプレフィックスは異なります。

| オンプレミス 2017 に由来する名前 | クラウド サービスに由来する名前 |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

上記の表の 2 つのリストは、2019 年 6 月時点のものです。 この表の内容は保守対象ではない可能性があり、古くなっている可能性があります。 正確なリストを表示するには、次の T-SQL SELECT ステートメントを実行します。 SELECT を 2 回、データベース システムごとに 1 回ずつ実行します。

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
