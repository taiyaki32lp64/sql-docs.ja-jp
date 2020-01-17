---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8c5d7ac822546d8334f1a174684f35733d9571b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116489"
---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースの特定のテーブルまたはすべてのテーブルの行数、予約済みのディスク領域、使用済みのディスク領域を表示します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>引数  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 表示される 1 部、2 部、または 3 部構成のテーブル名。 2 部または 3 部構成のテーブル名は、二重引用符 ("") で囲む必要があります。 1 部構成のテーブル名を囲む引用符を使用することは省略できます。 テーブル名が指定されていない場合は、現在のデータベースの情報が表示されます。  
  
## <a name="permissions"></a>アクセス許可  
VIEW SERVER STATE 権限が必要です。
  
## <a name="result-sets"></a>結果セット  
これは、すべてのテーブルの結果セットです。
  
|[列]|データ型|[説明]|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|データベースに使用されている合計領域 (KB 単位)。|  
|data_space|BIGINT|データに使用されている領域 (KB 単位)。|  
|index_space|BIGINT|インデックスに使用されている領域 (KB 単位)。|  
|unused_space|BIGINT|予約済み領域の一部で使用されていない領域 (KB 単位)。|  
|pdw_node_id|INT|データに使用されているコンピューティング ノード。|  
  
これは、1 つのテーブルの結果セットです。
  
|[列]|データ型|[説明]|範囲|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|行の数。||  
|reserved_space|BIGINT|オブジェクトに予約されている合計領域 (KB 単位)。||  
|data_space|BIGINT|データに使用されている領域 (KB 単位)。||  
|index_space|BIGINT|インデックスに使用されている領域 (KB 単位)。||  
|unused_space|BIGINT|予約済み領域の一部で使用されていない領域 (KB 単位)。||  
|pdw_node_id|INT|領域の使用状況の報告に使用されるコンピューティング ノード。||  
|distribution_id|INT|領域の使用状況の報告に使用されるディストリビューション。|レプリケートされたテーブルの場合、値は -1 です。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. DBCC PDW_SHOWSPACEUSED の基本的な構文  
次の例では、[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] データベースの FactInternetSales テーブルの行数、予約済みのディスク領域、使用済みのディスク領域を表示する複数の方法を示します。
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. 現在のデータベース内のすべてのテーブルで使用されているディスク領域を表示する  
 次の例では、[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] のすべてのユーザー テーブルとシステム テーブルで使用される予約済みのディスク領域を示します。  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>参照
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
