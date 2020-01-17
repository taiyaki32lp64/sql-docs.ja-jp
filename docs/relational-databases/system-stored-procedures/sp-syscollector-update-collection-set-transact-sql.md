---
title: sp_syscollector_update_collection_set は (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a351eaa746654d26d7f51536a41fc2677a2f67e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68010551"
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set は (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ユーザー定義のコレクション セットのプロパティを変更するために使用またはユーザー定義のコレクションの名前を変更するには設定します。  
  
> [!WARNING]  
>  プロキシとして構成されている Windows アカウントが非対話型または対話型のユーザーではまだログインしていない場合、プロファイル ディレクトリは存在しませんし、ステージング ディレクトリの作成は失敗します。 したがって、ドメイン コントローラーでプロキシ アカウントを使用している場合は、プロファイル ディレクトリが確実に作成されているようにするため、少なくとも 1 回は使用されている対話型アカウントを指定する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @collection_set_id = ] collection_set_id` コレクション セットの一意なローカル識別子です。 *collection_set_id*は**int**場合、値が必要と*名前*は NULL です。  
  
`[ @name = ] 'name'` コレクション セットの名前です。 *名前*は**sysname**場合、値が必要と*collection_set_id*は NULL です。  
  
`[ @new_name = ] 'new_name'` コレクション セットの新しい名前です。 *新しい名前*は**sysname**、使用する場合は空の文字列にすることはできません。 *新しい名前*で一意である必要があります。 現在のコレクション セットの名前の一覧については、syscollector_collection_sets システム ビューにクエリを実行します。  
  
`[ @target = ] 'target'` 将来使用するために予約されています。  
  
`[ @collection_mode = ] collection_mode` 使用するデータ コレクションの型です。 *collection_mode*は**smallint**値は次のいずれかを指定できます。  
  
 0 - キャッシュ モード。 データの収集とアップロードは個別のスケジュールです。 継続的なコレクションのキャッシュ モードを指定します。  
  
 1-非キャッシュ モード。 データの収集とアップロードは、同じスケジュールでは。 アドホック コレクションまたはスナップショット コレクションの非キャッシュ モードを指定します。  
  
 非キャッシュ モードからキャッシュ モード (0) に変更を場合、する必要がありますいずれかも指定*schedule_uid*または*schedule_name*します。  
  
`[ @days_until_expiration = ] days_until_expiration` 管理データ ウェアハウスに収集されたデータが保存されている日の数です。 *days_until_expiration*は**smallint**します。 *days_until_expiration* 0 または正の整数にする必要があります。  
  
`[ @proxy_id = ] proxy_id` 一意の識別子には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント プロキシ アカウント。 *proxy_id*は**int**します。  
  
`[ @proxy_name = ] 'proxy_name'` プロキシの名前です。 *proxy_name*は**sysname** null 値は。  
  
`[ @schedule_uid = ] 'schedule_uid'` スケジュールを参照する GUID。 *schedule_uid*は**uniqueidentifier**します。  
  
 取得する*schedule_uid*、sysschedules システム テーブルをクエリします。  
  
 ときに*collection_mode*を 0 に設定されている*schedule_uid*または*schedule_name*指定する必要があります。 ときに*collection_mode*を 1 に設定されている*schedule_uid*または*schedule_name*指定されている場合は無視されます。  
  
`[ @schedule_name = ] 'schedule_name'` スケジュールの名前です。 *schedule_name*は**sysname** null 値は。 指定した場合*schedule_uid* NULL にする必要があります。 取得する*schedule_name*、sysschedules システム テーブルをクエリします。  
  
`[ @logging_level = ] logging_level` ログ記録レベルです。 *logging_level*は**smallint**次の値のいずれかの。  
  
 0 - ログの実行情報と[!INCLUDE[ssIS](../../includes/ssis-md.md)]イベントを追跡します。  
  
-   開始/停止のコレクション セット  
  
-   パッケージの開始/停止  
  
-   エラー情報  
  
 1-レベル 0 のログ記録と。  
  
-   実行の統計  
  
-   コレクションの進行状況を継続的に実行  
  
-   警告イベント [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2-1 レベルのログ記録とから詳細なイベント情報[!INCLUDE[ssIS](../../includes/ssis-md.md)]します。  
  
 既定値*logging_level*は 1 です。  
  
`[ @description = ] 'description'` コレクション セットの説明です。 *説明*は**nvarchar (4000)** します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syscollector_update_collection_set は、msdb システム データベースのコンテキストで実行する必要があります。  
  
 いずれか*collection_set_id*または*名前*する必要があります値を持つ、どちらも NULL をすることはできません。 これらの値を取得するには、syscollector_collection_sets システム ビューにクエリを実行します。  
  
 のみ更新できますコレクション セットが実行されている場合*schedule_uid*と*説明*します。 コレクション セットを停止するには使用[sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin または dc_operator 固定データベース ロールのメンバーシップが必要です。 dc_operator ロールのメンバーがこのストアド プロシージャで更新できるのは、その権限で変更できるプロパティに限られます。 次のプロパティについては、dc_admin のみ変更できます。  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>使用例  
  
### <a name="a-renaming-a-collection-set"></a>A. コレクション セットの名前を変更する  
 次の例では、ユーザー定義のコレクション セットを変更します。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. コレクション モードを非キャッシュからキャッシュに変更する  
 次の例では、コレクション モードを非キャッシュ モードからキャッシュ モードに変更します。 この変更は、スケジュール ID またはスケジュール名を指定することが必要です。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. パラメーターを設定するその他のコレクションを変更します。  
 次の例の更新プログラム、コレクション セットのさまざまなプロパティという名前の"Simple collection set test 2" です。  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysschedules &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
