---
title: RESULT_SET_CACHING の設定 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: aea7470bd5b4d046dd5346e633fb5302ea8e7b9c
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962360"
---
# <a name="set-result-set-caching-transact-sql"></a>結果セット キャッシュの設定 (Transact-SQL) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

現在のクライアント セッションの結果セットのキャッシュ動作を制御します。  

適用対象: Azure SQL Data Warehouse  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

result_set_caching の設定を構成するユーザー データベースに接続した状態で、このコマンドを実行します。

**ON**   
現在のクライアント セッションの結果セットのキャッシュを有効にします。  結果セットのキャッシュがデータベース レベルで OFF にされていた場合、これをセッションで ON にすることはできません。

**OFF**   
現在のクライアント セッションの結果セットのキャッシュを無効にします。

## <a name="examples"></a>使用例

クエリの request_id を指定して [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) 内の result_cache_hit 列をクエリし、このクエリの実行時に、結果のキャッシュ ヒットおよびキャッシュ ミスのいずれが使用されたかを確認します。

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>アクセス許可

public ロールのメンバーシップが必要です

## <a name="see-also"></a>参照
[結果セットのキャッシュを使用したパフォーマンス チューニング](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)</br>
[DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)