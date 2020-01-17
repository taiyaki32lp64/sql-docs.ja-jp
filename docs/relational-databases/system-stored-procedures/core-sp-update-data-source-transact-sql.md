---
title: core.sp_update_data_source を呼び出します (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
author: stevestein
ms.author: sstein
ms.openlocfilehash: a840c749222cc7c01fa1b1ff5a27489e0e9d322a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942465"
---
# <a name="corespupdatedatasource-transact-sql"></a>core.sp_update_data_source を呼び出します (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  管理データ ウェアハウスの core.source_info_internal テーブルで既存行の更新または新規行の挿入を行います。 この手順は、アップロード パッケージが管理データ ウェアハウスへのデータのアップロードを起動するたびに、データ コレクターの実行時コンポーネントによって呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_uid =] '*collection_set_uid*'  
 コレクション セットの GUID を指定します。 *collection_set_uid*は**uniqueidentifier**既定値はありません。 GUID を取得するには、msdb データベースの dbo.syscollector_collection_sets ビューにクエリを実行します。  
  
 [ @machine_name =] '*machine_name*'  
 コレクション セットが存在するサーバーの名前を指定します。 *コンピューター名*は**sysname**で既定値はありません。  
  
 [ @named_instance =] '*named_instance*'  
 コレクション セットのインスタンスの名前。 *named_instance*は**sysname**既定値はありません。  
  
> [!NOTE]  
>  *named_instance*インスタンスの完全修飾名は、コンピューター名と形式でインスタンス名で構成される必要があります*computername*\\*instancename*します。  
  
 [ @days_until_expiration = ] *days_until_expiration*  
 スナップショット データ保持期間の日数を指定します。 *days_until_expiration*は**smallint**します。  
  
 [ @source_id =] *source_id*  
 更新プログラムのソースの一意の識別子。 *source_id*は**int**出力として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 アップロード パッケージが管理データ ウェアハウスへのデータのアップロードを開始するたびに、データ コレクターの実行時コンポーネントが core.sp_update_data_source を呼び出します。 前回のアップロード時以降に次のいずれかの変更が行われている場合は、core.source_info_internal テーブルが更新されます。  
  
-   新しいコレクション セットが追加されました。  
  
-   days_until_expiration の値が変更された。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **mdw_writer** (EXECUTE 権限) を持つ固定データベース ロール。  
  
## <a name="examples"></a>使用例  
 次の例では、データ ソースを更新する (この場合、ディスク使用量コレクション セット)、有効期限までの日数の数を設定し、ソースの識別子を返します。 例では、既定のインスタンスが使用されます。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理データ ウェアハウス](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
