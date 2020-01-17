---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4a701a56ba5a71037317f6c404fa394a466febba
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729882"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] データベースの記憶域スペースで使用されている結果セットのキャッシュが表示されます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Remarks

`DBCC SHOWRESULTCACHESPACEUSED` コマンドは、パラメーターがなく、このコマンドを実行したデータベースで使用されるスペースが返されます。

## <a name="permissions"></a>アクセス許可

VIEW SERVER STATE 権限が必要です。
  
## <a name="result-sets"></a>結果セット  
  
|[列]|データ型|[説明]|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|データベースに使用されている合計領域 (KB 単位)。 この数値は、キャッシュされた結果セットの増加に応じて変化します。|  
|data_space|BIGINT|データに使用されている領域 (KB 単位)。|  
|index_space|BIGINT|インデックスに使用されている領域 (KB 単位)。|  
|unused_space|BIGINT|予約済み領域の一部で使用されていない領域 (KB 単位)。|  


## <a name="see-also"></a>参照

[結果セットのキャッシュを使用したパフォーマンス チューニング](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET のオプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE  &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)