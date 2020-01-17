---
title: sp_syscollector_create_collection_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
author: stevestein
ms.author: sstein
ms.openlocfilehash: e859ed97afdc3dfbb4e39a93b8691d044ceca37d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032640"
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新しいコレクション セットを作成します。 このストアド プロシージャを使用して、データ収集の設定、カスタム コレクションを作成することができます。  
  
> [!WARNING]  
>  プロキシとして構成されている Windows アカウントが非対話型または対話型のユーザーではまだログインしていない場合、プロファイル ディレクトリは存在しませんし、ステージング ディレクトリの作成は失敗します。 したがって、ドメイン コントローラーでプロキシ アカウントを使用している場合は、プロファイル ディレクトリが確実に作成されているようにするため、少なくとも 1 回は使用されている対話型アカウントを指定する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` コレクション セットの名前です。 *名前*は**sysname**空の文字列または NULL にすることはできません。  
  
 *名前*で一意である必要があります。 現在のコレクション セットの名前の一覧については、syscollector_collection_sets システム ビューにクエリを実行します。  
  
`[ @target = ] 'target'` 将来使用するために予約されています。 *名前*は**nvarchar (128)** 既定値は NULL です。  
  
`[ @collection_mode = ] collection_mode` データが収集および保存の方法を指定します。 *collection_mode*は**smallint**値は次のいずれかを指定できます。  
  
 0 - キャッシュ モード。 データの収集とアップロードは個別のスケジュールです。 継続的なコレクションのキャッシュ モードを指定します。  
  
 1-非キャッシュ モード。 データの収集とアップロードは、同じスケジュールでは。 アドホック コレクションまたはスナップショット コレクションの非キャッシュ モードを指定します。  
  
 既定値*collection_mode*は 0 です。 ときに*collection_mode*は 0 です。 *schedule_uid*または*schedule_name*指定する必要があります。  
  
`[ @days_until_expiration = ] days_until_expiration` 管理データ ウェアハウスに収集されたデータが保存されている日の数です。 *days_until_expiration*は**smallint**で、既定値は 730 (2 年)。 *days_until_expiration* 0 または正の整数にする必要があります。  
  
`[ @proxy_id = ] proxy_id` 一意の識別子には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント プロキシ アカウント。 *proxy_id*は**int**既定値は NULL です。 指定した場合*proxy_name* NULL にする必要があります。 取得する*proxy_id*、sysproxies システム テーブルをクエリします。 Dc_admin 固定データベース ロールは、プロキシにアクセスする権限が必要です。 詳細については、次を参照してください。 [SQL Server エージェント プロキシの作成](../../ssms/agent/create-a-sql-server-agent-proxy.md)です。  
  
`[ @proxy_name = ] 'proxy_name'` プロキシ アカウントの名前です。 *proxy_name*は**sysname**既定値は NULL です。 指定した場合*proxy_id* NULL にする必要があります。 取得する*proxy_name*、sysproxies システム テーブルをクエリします。  
  
`[ @schedule_uid = ] 'schedule_uid'` スケジュールを参照する GUID。 *schedule_uid*は**uniqueidentifier**既定値は NULL です。 指定した場合*schedule_name* NULL にする必要があります。 取得する*schedule_uid*、sysschedules システム テーブルをクエリします。  
  
 ときに*collection_mode*を 0 に設定されている*schedule_uid*または*schedule_name*指定する必要があります。 ときに*collection_mode*を 1 に設定されている*schedule_uid*または*schedule_name*指定されている場合は無視されます。  
  
`[ @schedule_name = ] 'schedule_name'` スケジュールの名前です。 *schedule_name*は**sysname**既定値は NULL です。 指定した場合*schedule_uid* NULL にする必要があります。 取得する*schedule_name*、sysschedules システム テーブルをクエリします。  
  
`[ @logging_level = ] logging_level` ログ記録レベルです。 *logging_level*は**smallint**次の値のいずれかの。  
  
 0 - ログの実行情報と[!INCLUDE[ssIS](../../includes/ssis-md.md)]イベントを追跡します。  
  
-   開始/停止のコレクション セット  
  
-   パッケージの開始/停止  
  
-   エラー情報  
  
 1 - レベル 0 の情報に加えて、以下の情報をログに記録します。  
  
-   実行の統計  
  
-   コレクションの進行状況を継続的に実行  
  
-   警告イベント [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2-1 レベルのログ記録とから詳細なイベント情報 [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 既定値*logging_level*は 1 です。  
  
`[ @description = ] 'description'` コレクション セットの説明です。 *説明*は**nvarchar (4000)** 既定値は NULL です。  
  
`[ @collection_set_id = ] collection_set_id` コレクション セットの一意なローカル識別子です。 *collection_set_id*は**int**出力を含む必要があります。  
  
`[ @collection_set_uid = ] 'collection_set_uid'` コレクション セットの GUID です。 *collection_set_uid*は**uniqueidentifier**出力で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syscollector_create_collection_set は、msdb システム データベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. 既定値を使用して設定コレクションを作成します。  
 次の例では、必須パラメーターのみを指定してコレクション セットを作成します。 `@collection_mode` 必須ではありませんが (キャッシュ済み)、既定のコレクション モードは、スケジュール ID またはスケジュール名のいずれかを指定する必要があります。  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>B. 指定した値を使用して設定コレクションを作成します。  
 次の例では、多くのパラメーターの値を指定してコレクション セットを作成します。  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [ジェネリック T-SQL Query コレクター型を使用するカスタム コレクション セットの作成 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
