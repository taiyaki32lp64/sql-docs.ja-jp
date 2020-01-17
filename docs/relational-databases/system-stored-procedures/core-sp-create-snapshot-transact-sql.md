---
title: core.sp_create_snapshot を呼び出します (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_snapshot
- sp_create_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- management data warehouse, data collector stored procedures
- data collector [SQL Server], stored procedures
- core.sp_create_snapshot stored procedure
- sp_create_snapshot
ms.assetid: ff297bda-0ee2-4fda-91c8-7000377775e3
author: stevestein
ms.author: sstein
ms.openlocfilehash: ef2bce1ff84172d01b1304a416f84865f1cb36bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078220"
---
# <a name="corespcreatesnapshot-transact-sql"></a>core.sp_create_snapshot を呼び出します (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  管理データ ウェアハウスの core.snapshots ビューに行を挿入します。 このプロシージャは、アップロード パッケージでは、管理データ ウェアハウスにデータをアップロードが開始されるたびに呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_create_snapshot [ @collection_set_uid = ] 'collection_set_uid'  
    , [ @collector_type_uid = ] 'collector_type_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @log_id = ] log_id  
    , [ @snapshot_id = ] snapshot_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_uid =] '*collection_set_uid*'  
 コレクション セットの GUID を指定します。 *collection_set_uid*は**uniqueidentifier**で既定値はありません。 GUID を取得するには、msdb データベースの dbo.syscollector_collection_sets ビューにクエリを実行します。  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 コレクター型の GUID です。 *collector_type_uid*は**uniqueidentifier**で既定値はありません。 GUID を取得するには、msdb データベースの dbo.syscollector_collector_types ビューにクエリを実行します。  
  
 [ @machine_name=] '*machine_name*'  
 コレクション セットが存在するサーバーの名前を指定します。 *コンピューター名*は**sysname**既定値はありません。  
  
 [ @named_instance=] '*named_instance*'  
 コレクション セットのインスタンスの名前。 *named_instance*は**sysname**既定値はありません。  
  
 [ @log_id = ] *log_id*  
 コレクションにマップする一意識別子では、イベント ログをデータを収集するサーバーを設定します。 *log_id*は**bigint**で既定値はありません。 値を取得する*log_id*、msdb データベースの dbo.syscollector_execution_log ビューにクエリを実行します。  
  
 [ @snapshot_id = ] *snapshot_id*  
 Core.snapshots ビューに挿入する行の一意の識別子。 *snapshot_id*は**int**出力として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 アップロード パッケージが管理データ ウェアハウスへのデータのアップロードを開始するごとに、データ コレクターの実行時コンポーネントが core.sp_create_snapshot を呼び出します。  
  
 このプロシージャでは、次の条件がチェックされます。  
  
-   collection_set_uid が、core.source_info_internal テーブルの既存のエントリと一致していること。  
  
-   collector_type_uid が、core.supported_collector_types ビューの既存のエントリと一致していること。  
  
 これらの条件のいずれかが失敗した場合、プロシージャは失敗し、エラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **mdw_writer** (EXECUTE 権限) を持つ固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、ディスク使用量コレクション セットのスナップショットを作成し、それを管理データ ウェアハウスに追加して、スナップショット識別子を返します。 例では、既定のインスタンスが使用されます。  
  
```  
USE <management_data_warehouse>;  
DECLARE @snapshot_id int;  
EXEC core.sp_create_snapshot   
    @collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
    @collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @machine_name = '<computername>',  
    @named_instance = 'MSSQLSERVER',  
    @log_id = 11, -- ID of the log for the collection set  
    @snapshot_id = @snapshot_id OUTPUT;  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理データ ウェアハウス](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
