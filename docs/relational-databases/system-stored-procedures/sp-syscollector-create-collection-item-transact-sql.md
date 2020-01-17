---
title: sp_syscollector_create_collection_item (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7ba3753a18d8e79848b0674e4738f2d2b811143e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032668"
---
# <a name="spsyscollectorcreatecollectionitem-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー定義のコレクション セットにコレクション アイテムを作成します。 コレクション アイテムは、データを収集して、データを収集する頻度を定義します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_id = ] *collection_set_id*  
 コレクション セットの一意なローカル識別子を指定します。 *collection_set_id*は**int**します。  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 この項目に使用するコレクター型を識別する GUID が*collector_type_uid*は**uniqueidentifier**で既定値はありません. コレクター型の一覧については、syscollector_collector_types システム ビューにクエリを実行します。  
  
 [ @name = ] '*name*'  
 コレクション アイテムの名前です。 *名前*は**sysname**空の文字列または NULL にすることはできません。  
  
 *名前*で一意である必要があります。 現在のコレクション アイテムの名前の一覧については、syscollector_collection_items システム ビューにクエリを実行します。  
  
 [ @frequency = ] *frequency*  
 このコレクション アイテムによってデータを収集する頻度を秒単位で指定に使用されます。 *頻度*は**int**、既定値は 5 です。 指定できる最小値は、5 秒です。  
  
 コレクション セットが非キャッシュ モードに設定されている場合は、このモードでは、データ収集とアップロードが、コレクション セットの指定されたスケジュールで行われるため、頻度が無視されます。 コレクション セットのコレクション モードを表示するには、クエリ、 [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)システム ビュー。  
  
 [ @parameters =] '*パラメーター*'  
 コレクター型の入力パラメーターを指定します。 *パラメーター*は**xml**既定値は NULL です。 *パラメーター*スキーマはコレクター型のパラメーター スキーマと一致する必要があります。  
  
 [ @collection_item_id = ] *collection_item_id*  
 コレクション セット アイテムを識別する一意な識別子を指定します。 *collection_item_id*は**int** OUTPUT を持ちます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syscollector_create_collection_item は、msdb システム データベースのコンテキストで実行する必要があります。  
  
 コレクション アイテムが追加するコレクション セットは、コレクション アイテムを作成する前に停止する必要があります。 コレクション アイテムは、システム コレクション セットに追加できません。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、コレクション アイテムがコレクション型に基づく`Generic T-SQL Query Collector Type`名前付きセット、コレクションに追加します`Simple collection set test 2`します。 指定したコレクションを作成する設定、例 B を実行[sp_syscollector_create_collection_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)します。  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item は&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [sp_syscollector_create_collection_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
