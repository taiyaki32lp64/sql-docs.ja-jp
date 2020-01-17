---
title: sp_help_downloadlist (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_downloadlist_TSQL
- sp_help_downloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_downloadlist
ms.assetid: 745b265b-86e8-4399-b928-c6969ca1a2c8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40345ed8ad1a10da0088c5c1388c44fa24cad929
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055194"
---
# <a name="sphelpdownloadlist-transact-sql"></a>sp_help_downloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべての行を一覧表示、 **sysdownloadlist**ジョブまたはジョブが指定されていない場合、すべての行がシステム テーブル。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_downloadlist { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }   
     [ , [ @operation = ] 'operation' ]   
     [ , [ @object_type = ] 'object_type' ]   
     [ , [ @object_name = ] 'object_name' ]   
     [ , [ @target_server = ] 'target_server' ]   
     [ , [ @has_error = ] has_error ]   
     [ , [ @status = ] status ]   
     [ , [ @date_posted = ] date_posted ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 情報を返す対象のジョブ識別番号。 *job_id*は**uniqueidentifier**、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name*は**sysname**、既定値は NULL です。  
  
> [!NOTE]  
>  いずれか*job_id*または*job_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @operation = ] 'operation'` 指定したジョブの有効な操作です。 *操作*は**varchar (64)** 、既定値は null の場合、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**欠陥**|マスターからの参加を解除する対象サーバーを要求するサーバー操作**SQLServerAgent**サービス。|  
|**DELETE**|ジョブ全体を削除するジョブ操作。|  
|**INSERT**|ジョブ全体の追加、または既存のジョブの更新を行うジョブ操作。 場合によっては、この操作にはすべてのジョブ ステップとスケジュールが含まれます。|  
|**RE-ENLIST**|ターゲット サーバーで参加情報の再送信を行うためのサーバー操作。この情報にはマルチサーバー ドメインのポーリング間隔やタイム ゾーンも含まれます。 ターゲット サーバーがでも、 **MSXOperator**詳細。|  
|**SET-POLL**|ターゲット サーバーがマルチサーバー ドメインを呼び出す間隔を秒単位で設定するサーバー操作。 指定した場合*値*は必要な間隔の値として解釈されから値を指定できます**10**に**28,800**します。|  
|**開始**|ジョブ実行の開始を要求するジョブ操作。|  
|**STOP**|ジョブ実行の停止を要求するジョブ操作。|  
|**同期時刻**|ターゲット サーバーでシステム クロックとマルチサーバー ドメインとの同期化を行うためのサーバー操作。 これは非常に時間のかかる操作なので、頻繁に実行しないでください。限られた場合にだけ、実行するようにしてください。|  
|**UPDATE**|ジョブだけを更新する操作、 **sysjobs**ジョブ ステップまたはスケジュールではない、ジョブの情報。 によって自動的に呼び出される**sp_update_job**します。|  
  
`[ @object_type = ] 'object_type'` 指定したジョブのオブジェクトの型。 *object_type*は**varchar (64)** 、既定値は NULL です。 *object_type*ジョブまたはサーバーのいずれかにすることができます。 有効なの詳細については*object_type*値を参照してください[sp_add_category &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)します。  
  
`[ @object_name = ] 'object_name'` オブジェクトの名前。 *object_name*は**sysname**、既定値は NULL です。 場合*object_type*ジョブ、 *object_name*ジョブの名前します。 場合*object_type*サーバー、 *object_name*サーバーの名前を指定します。  
  
`[ @target_server = ] 'target_server'` 対象サーバーの名前。 *target_server*は**nvarchar (128)** 、既定値は NULL です。  
  
`[ @has_error = ] has_error` ジョブがエラーを肯定するかどうか。 *has_error*は**tinyint**の既定値は NULL には、エラーを肯定しないことを示します。 **1**すべてのエラーを肯定することを示します。  
  
`[ @status = ] status` ジョブの状態です。 *ステータス*は**tinyint**既定値は NULL です。  
  
`[ @date_posted = ] date_posted` 日付と時刻に作成されたどのすべてのエントリ、または指定した日付と時刻は、結果に含める必要が次のように設定します。 *date_posted*は**datetime**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|命令の一意な整数識別番号。|  
|**source_server**|**nvarchar(30)**|命令を実行したサーバーのコンピューター名。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]バージョン 7.0 では、これは、常にマスター (MSX) サーバーのコンピューター名。|  
|**operation_code**|**nvarchar (4000)**|命令の操作コード。|  
|**object_name**|**sysname**|命令対象のオブジェクト。|  
|**object_id**|**uniqueidentifier**|命令によって影響を受けるオブジェクトの識別番号 (**job_id**ジョブ オブジェクト、またはサーバー オブジェクトの場合は 0x00) に固有のデータ値、または、 **operation_code**します。|  
|**target_server**|**nvarchar(30)**|命令をダウンロードするターゲット サーバー。|  
|**error_message**|**nvarchar(1024)**|この命令の処理中に問題が発生した場合の、ターゲット サーバーからのエラー メッセージ (存在する場合)。<br /><br /> 注:すべてのエラー メッセージ ブロックは、ターゲット サーバーによってさらにダウンロードします。|  
|**date_posted**|**datetime**|命令をテーブルに記録した日付。|  
|**date_downloaded**|**datetime**|ターゲット サーバーが命令をダウンロードした日付。|  
|**status**|**tinyint**|ジョブのステータス。<br /><br /> **0** = 未ダウンロード<br /><br /> **1** = 正常にダウンロードします。|  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
 次の例では、`sysdownloadlist` 内の `NightlyBackups` ジョブに関する行を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_downloadlist  
    @job_name = N'NightlyBackups',  
    @operation = N'UPDATE',   
    @object_type = N'JOB',   
    @object_name = N'NightlyBackups',  
    @target_server = N'SEATTLE2',   
    @has_error = 1,   
    @status = NULL,   
    @date_posted = NULL ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
