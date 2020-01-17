---
title: sp_addsynctriggers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2b9bdabcc11c900ae0a1cbe71280b64efb6ccdaf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096211"
---
# <a name="spaddsynctriggers-transact-sql"></a>sp_addsynctriggers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新可能なサブスクリプション (イミディ エイト、キュー、およびフェールオーバーとしてキュー更新を使用する即時更新) のすべての種類で使用するサブスクライバーでトリガーを作成します。 このストアド プロシージャは、サブスクライバーのサブスクリプション データベースで実行されます。  
  
> [!IMPORTANT]  
>  [Sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)の代わりにプロシージャを使用する必要があります**sp_addsynctrigger**します。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)を含むスクリプトを生成、 **sp_addsynctrigger**呼び出し。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>引数  
`[ @sub_table = ] 'sub_table'` サブスクライバー テーブルの名前です。 *sub_table*は**sysname**、既定値はありません。  
  
`[ @sub_table_owner = ] 'sub_table_owner'` サブスクライバー テーブルの所有者の名前です。 *sub_table_owner*は**sysname**、既定値はありません。  
  
`[ @publisher = ] 'publisher'` パブリッシャー サーバーの名前です。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャー データベースの名前です。 *publisher_db* は **sysname** 、既定値はありません。 NULL の場合は、現在のデータベースが使用されます。  
  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値はありません。  
  
`[ @ins_proc = ] 'ins_proc'` パブリッシャー側での同期トランザクション挿入をサポートするストアド プロシージャの名前です。 *ins_proc*は**sysname**、既定値はありません。  
  
`[ @upd_proc = ] 'upd_proc'` パブリッシャーでの同期トランザクション更新をサポートするストアド プロシージャの名前です。 *ins_proc*は**sysname**、既定値はありません。  
  
`[ @del_proc = ] 'del_proc'` パブリッシャー側での同期トランザクション削除をサポートするストアド プロシージャの名前です。 *ins_proc*は**sysname**、既定値はありません。  
  
`[ @cftproc = ] 'cftproc'` キュー更新を許可するパブリケーションによって使用される自動生成されたプロシージャの名前です。 *cftproc*は**sysname**、既定値はありません。 即時更新を許可するパブリケーションの場合は、この値は NULL です。 このパラメーターは、キュー更新 (キュー更新、およびフェールオーバーとしてキュー更新を使用する即時更新) が許可されているパブリケーションに適用されます。  
  
`[ @proc_owner = ] 'proc_owner'` すべてのパブリッシャーのパブリケーション (キューに置かれたおよび即時) を更新するための自動生成されたストアド プロシージャが作成されたユーザー アカウントを指定します。 *proc_owner*は**sysname**既定値はありません。  
  
`[ @identity_col = ] 'identity_col'` パブリッシャー側で id 列の名前です。 *identity_col*は**sysname**、既定値は NULL です。  
  
`[ @ts_col = ] 'timestamp_col'` 名前を指定します、**タイムスタンプ**パブリッシャーの列。 *timestamp_col*は**sysname**、既定値は NULL です。  
  
`[ @filter_clause = ] 'filter_clause'` 制限は、水平方向のフィルターを定義する (、) where 句。 制限句を入力するときに、キーワードを省略する場所。 *filter_clause*は**nvarchar (4000)** 、既定値は NULL です。  
  
`[ @primary_key_bitmap = ] 'primary_key_bitmap'` テーブルの主キー列のビット マップです。 *primary_key_bitmap*は**varbinary (4000)** 、既定値はありません。  
  
`[ @identity_support = ] identity_support` 有効にし、キュー更新を使用するときに自動 id 範囲処理を無効にします。 *identity_support*は、**ビット**、既定値は**0**します。 **0** id がないことを意味の範囲のサポート、 **1**自動 id 範囲処理を有効にします。  
  
`[ @independent_agent = ] independent_agent` このパブリケーションの 1 つのディストリビューション エージェント (独立エージェント) またはパブリケーション データベースとサブスクリプション データベースのペア (共有エージェント) ごとに 1 つのディストリビューション エージェントがあるかどうかを示します。 この値には、パブリッシャーで定義されているパブリケーションの independent_agent プロパティの値が反映されます。 *independent_agent*は bit で、既定値は**0**します。 場合**0**エージェントが共有エージェント。 場合**1**エージェントが独立したエージェント。  
  
`[ @distributor = ] 'distributor'` ディストリビューターの名前です。 *ディストリビューター*は**sysname**、既定値はありません。  
  
`[ @pubversion = ] pubversion` パブリッシャーのバージョンを示します。 *pubversion*は**int**、既定値は 1 です。 **1**パブリッシャーのバージョンであることを意味[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 以前です。**2**パブリッシャーであることを意味[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]Service Pack 3 (SP3) 以降。 *pubversion*に明示的に設定する必要があります**2**とパブリッシャーのバージョンが[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]SP3 以降。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addsynctriggers**サブスクリプションの初期化の一部として、ディストリビューション エージェントによって使用されます。 このストアド プロシージャでは、ユーザーが頻繁に実行されませんが、ユーザーが手動で同期なしサブスクリプションを設定する必要がある場合に便利です。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_addsynctriggers**します。  
  
## <a name="see-also"></a>関連項目  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
