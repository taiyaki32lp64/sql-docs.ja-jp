---
title: sp_syscollector_update_collection_item (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
author: stevestein
ms.author: sstein
ms.openlocfilehash: 791c20214ff3eda4b5bb1f2bd3214b25ea972d74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010564"
---
# <a name="spsyscollectorupdatecollectionitem-transact-sql"></a>sp_syscollector_update_collection_item (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー定義のコレクション アイテムのプロパティまたは名前の変更に使用されます。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_item_id = ] *collection_item_id*  
 コレクション アイテムを識別する一意の識別子です。 *collection_item_id*は**int**既定値は NULL です。 *collection_item_id*場合、値が必要*名前*は NULL です。  
  
 [ @name = ] '*name*'  
 コレクション アイテムの名前です。 *名前*は**sysname**既定値は NULL です。 *名前*場合、値が必要*collection_item_id*は NULL です。  
  
 [ @new_name = ] '*new_name*'  
 コレクション アイテムの新しい名前を指定します。 *新しい名前*は**sysname**、使用する場合は空の文字列にすることはできません。  
  
 *新しい名前*で一意である必要があります。 現在のコレクション アイテムの名前の一覧については、syscollector_collection_items システム ビューにクエリを実行します。  
  
 [ @frequency = ] *frequency*  
 このコレクション アイテムによってデータを収集する頻度を秒単位で指定します。 *頻度*は**int**、既定値は 5 で指定できる最小値。  
  
 [ @parameters =] '*パラメーター*'  
 コレクション アイテムの入力パラメーターを指定します。 *パラメーター*は**xml**既定値は NULL です。 *パラメーター*スキーマはコレクター型のパラメーター スキーマと一致する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 コレクション セットが非キャッシュ モードに設定されている場合、このモードではコレクション セットに指定されたスケジュールでデータ収集とアップロードが行われるため、頻度を変更しても無視されます。 コレクション セットの状態を表示するには、次のクエリを実行します。 `<collection_item_id>` は、更新するコレクション アイテムの ID に置き換えてください。  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin または dc_operator 固定データベース ロールのメンバーシップが必要です。 dc_operator ロールのメンバーがこのストアド プロシージャで更新できるのは、その権限で変更できるプロパティに限られます。 次のプロパティについては、dc_admin のみ変更できます。  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>使用例  
 次の例で定義されている例で作成したコレクション項目に基づいています[sp_syscollector_create_collection_item &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)します。  
  
### <a name="a-changing-the-collection-frequency"></a>A. 収集頻度を変更する  
 次の例では、指定したコレクション アイテムの収集頻度を変更します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. コレクション アイテムの名前を変更します。  
 次の例では、コレクション アイテムの名前を変更します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. コレクション アイテムのパラメーターを変更する  
 次の例では、コレクション アイテムに関連付けられているパラメーターを変更します。 `<Value>` 属性内で定義されているステートメントを変更し、`UseSystemDatabases` 属性を false に設定します。 このアイテムの現在のパラメーターを表示するには、syscollector_collection_items システム ビューの parameters 列にクエリを実行します。 値を変更する必要があります`@collection_item_id`します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
