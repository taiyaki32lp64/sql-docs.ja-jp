---
title: sp_autostats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3fdb095ed869ba2e8f060bdba7a3dc9db81a405
ms.sourcegitcommit: 8c1c6232a4f592f6bf81910a49375f7488f069c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70026248"
---
# <a name="sp_autostats-transact-sql"></a>sp_autostats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  インデックス、統計オブジェクト、テーブル、またはインデックス付きビューの自動統計更新オプション (AUTO_UPDATE_STATISTICS) を表示または変更します。  
  
 AUTO_UPDATE_STATISTICS オプションの詳細については、「 [ALTER DATABASE の&#40;SET オプション transact-sql&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)と[STATISTICS](../../relational-databases/statistics/statistics.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_flag' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tblname = ] 'table_or_indexed_view_name'`AUTO_UPDATE_STATISTICS オプションを表示するテーブルまたはインデックス付きビューの名前を指定します。 *table_or_indexed_view_name*は**nvarchar (776)** ,、既定値はありません。  
  
`[ @flagc = ] 'stats_flag'`AUTO_UPDATE_STATISTICS オプションを次のいずれかの値に更新します。  
  
 **ON** = オン  
  
 **OFF** = オフ  
  
 *Stats_flag*が指定されていない場合は、現在の AUTO_UPDATE_STATISTICS 設定を表示します。 *stats_flag*は**varchar (10)** ,、既定値は NULL です。  
  
`[ @indname = ] 'statistics_name'`AUTO_UPDATE_STATISTICS オプションを表示または更新する統計の名前を指定します。 インデックスの統計を表示する場合は、インデックスの名前を使用できます。インデックスの名前は、対応する統計オブジェクトの名前と同じです。  
  
 *statistics_name*は**sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 *Stats_flag*を指定した場合、 **sp_autostats**は、実行されたアクションを報告しますが、結果セットは返しません。  
  
 場合*stats_flag*が指定されていない、 **sp_autostats**は、次の結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Index Name**|**varchar(60)**|インデックスまたは統計の名前。|  
|**AUTOSTATS**|**varchar(3)**|AUTO_UPDATE_STATISTICS オプションの現在の値。|  
|**最終更新日時**|**datetime**|統計の最終更新日。|  
  
 テーブルまたはインデックス付きビューの結果セットには、インデックス用に作成された統計、AUTO_CREATE_STATISTICS オプションで生成された単一列統計、および[CREATE statistics](../../t-sql/statements/create-statistics-transact-sql.md)ステートメントを使用して作成された統計が含まれます。  
  
## <a name="remarks"></a>コメント  
 指定したインデックスが無効な場合、または指定したテーブルに無効なクラスター化インデックスがある場合は、エラー メッセージが表示されます。  
  
 AUTO_UPDATE_STATISTICS はメモリ最適化テーブルでは常に OFF です。  
  
## <a name="permissions"></a>アクセス許可  
 AUTO_UPDATE_STATISTICS オプションを変更するには、 **db_owner**固定データベースロールのメンバーシップ、または*TABLE_NAME*に対する ALTER 権限が必要です。AUTO_UPDATE_STATISTICS オプションを表示するには、 **public**ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>A. テーブルのすべての統計の状態を表示する  
 次の`Product`表に、テーブルのすべての統計の状態を示します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-auto_update_statistics-for-all-statistics-on-a-table"></a>B. テーブルのすべての統計に対して AUTO_UPDATE_STATISTICS を有効にする  
 次の例では、`Product` テーブルのすべての統計の AUTO_UPDATE_STATISTICS オプションを有効にします。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-auto_update_statistics-for-a-specific-index"></a>C. 特定のインデックスの AUTO_UPDATE_STATISTICS を無効にする  
 次の例では、 `AK_Product_Name` `Product`テーブルのインデックスの AUTO_UPDATE_STATISTICS オプションを無効にします。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [統計](../../relational-databases/statistics/statistics.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [ストアドプロシージャ&#40;のデータベースエンジン transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
