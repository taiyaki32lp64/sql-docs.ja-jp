---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ac6d3ac9128c8f27a898f4b903f74d1e9ab9bb1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116502"
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] データベースに含まれるテーブルの各パーティションについて、サイズと行数を表示します。
  
![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "記事リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>引数  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 表示される 1 部、2 部、または 3 部構成のテーブル名。  2 部または 3 部構成のテーブル名は、二重引用符 ("") で囲む必要があります。 1 部構成のテーブル名を囲む引用符を使用することは省略できます。  
  
## <a name="permissions"></a>アクセス許可
**VIEW SERVER STATE** アクセス許可が必要です。
  
## <a name="result-sets"></a>結果セット  
このセットは、DBCC PDW_SHOWPARTITIONSTATS コマンドの結果です。
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|partition_number|INT|パーティション番号。|  
|used_page_count|BIGINT|データの使用ページ数。|  
|reserved_page_count|BIGINT|パーティションのために予約されたページ数。|  
|row_count|BIGINT|パーティション内の行数。|  
|pdw_node_id|INT|データのノードを計算します。|  
|distribution_id|INT|データの配布識別子。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. DBCC PDW_SHOWPARTITIONSTATS の基本的な構文の例  
次の例では、[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] データベースの FactInternetSales テーブルについて、パーティションごとに使用されている領域と行数を表示しています。
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>参照
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
 
