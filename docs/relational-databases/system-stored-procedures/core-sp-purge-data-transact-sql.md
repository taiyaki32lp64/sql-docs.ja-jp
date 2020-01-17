---
title: core.sp_purge_data (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
author: stevestein
ms.author: sstein
ms.openlocfilehash: 72737a9b623e7979617784c1ef49c3f6d09aaea8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942491"
---
# <a name="coresppurgedata-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  保有ポリシーに基づいて、管理データ ウェアハウスからデータを削除します。 このプロシージャは、指定されたインスタンスに関連付けられている管理データ ウェアハウスに対して、mdw_purge_data [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブによって毎日実行されます。 このストアド プロシージャを使用すると、管理データ ウェアハウスからデータのオンデマンドで削除を実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>引数  
 [@retention_days =] *retention_days*  
 管理データ ウェアハウスのテーブルにデータを保持する日数。 古いタイムスタンプを持つデータ*retention_days*が削除されます。 *retention_days*は**smallint**、既定値は NULL です。 指定した場合、値は正である必要があります。 NULL の場合は、core.snapshots ビューの valid_through 列の値によって、削除対象の行が判断されます。  
  
 [@instance_name =] '*instance_name*'  
 コレクション セットのインスタンスの名前。 *instance_name*は**sysname**、既定値は NULL です。  
  
 *instance_name*インスタンスの完全修飾名は、コンピューター名と形式でインスタンス名で構成される必要があります*computername*\\*instancename*します。 NULL の場合は、ローカル サーバーの既定のインスタンスが使用されます。  
  
 [@collection_set_uid =] '*collection_set_uid*'  
 コレクション セットの GUID を指定します。 *collection_set_uid*は**uniqueidentifier**、既定値は NULL です。 NULL の場合は、すべてのコレクション セットから条件を満たす行が削除されます。 この値を取得するには、syscollector_collection_sets カタログ ビューに対してクエリを実行します。  
  
 [@duration =]*期間*  
 パージ操作を実行する分の最大数。 *期間*は**smallint**、既定値は NULL です。 指定する場合、値はゼロまたは正の整数にする必要があります。 NULL の場合は、条件を満たすすべての行が削除されるか操作が手動で停止されるまで、操作は実行されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 このプロシージャでは、保有期間に基づいて削除対象となる core.snapshots ビューの行が選択されます。 削除対象のすべての行が core.snapshots_internal テーブルから削除されます。 前の行を削除すると、管理データ ウェアハウスのテーブルのすべての連鎖削除アクションがトリガーされます。 これは、収集されたデータを格納するすべてのテーブルに対して定義されている ON DELETE CASCADE 句を使って実行されます。  
  
 各スナップショットとその関連データは、明示的なトランザクションで削除されてからコミットされます。 そのため、パージ操作を手動で停止すると、または指定された値のかどうか@durationを超えると、のみ コミットされていないデータが残ります。 このデータは、ジョブの次回の実行時に削除できます。  
  
 管理データ ウェアハウス データベースのコンテキストでプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **mdw_admin** (EXECUTE 権限) を持つ固定データベース ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-running-sppurgedata-with-no-parameters"></a>A. パラメーターなしで sp_purge_data を実行します。  
 次の例では、パラメーターを指定せずに core.sp_purge_data を実行します。 そのため、すべてのパラメーターに既定値の NULL が使用され、それに関連付けられている動作が実行されます。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. 保有期間と実行時間の値を指定する  
 次の例では、7 日より前である、管理データ ウェアハウスからデータを削除します。 さらに、@durationパラメーターが指定されるため、操作を 5 分以内に実行されます。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. インスタンスの名前とコレクション セットの指定  
 次の例は、設定の指定されたインスタンスで指定したコレクションの管理データ ウェアハウスからデータを削除します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 @retention_daysが指定されていない、core.snapshots ビューの valid_through 列の値は削除対象のコレクション セットの行を特定するために使用します。  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
