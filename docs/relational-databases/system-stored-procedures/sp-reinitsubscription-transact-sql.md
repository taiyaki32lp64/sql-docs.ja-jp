---
title: sp_reinitsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: stevestein
ms.author: sstein
ms.openlocfilehash: eaeeaa5009cb119b40dcde9b8f9baa170d8f7bef
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762529"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サブスクリプションに再初期化のマークを付けます。 このストアド プロシージャは、プッシュ サブスクリプションのパブリッシャー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*は**sysname**,、既定値は all です。  
  
`[ @article = ] 'article'`アーティクルの名前を指定します。 *アーティクル*は**sysname**で、既定値は all です。 即時更新パブリケーションの場合、*アーティクル*は**all**である必要があります。それ以外の場合は、ストアドプロシージャによってパブリケーションがスキップされ、エラーが報告されます。  
  
`[ @subscriber = ] 'subscriber'`サブスクライバーの名前を指定します。 *サブスクライバー*は**sysname**,、既定値はありません。  
  
`[ @destination_db = ] 'destination_db'`転送先データベースの名前を指定します。 *destination_db*は**sysname**,、既定値は all です。  
  
`[ @for_schema_change = ] 'for_schema_change'`パブリケーションデータベースでのスキーマ変更の結果、再初期化が行われるかどうかを示します。 *for_schema_change*は**ビット**,、既定値は0です。 **0**の場合、即時更新を許可するパブリケーションのアクティブなサブスクリプションは、そのアーティクルの一部ではなく、パブリケーション全体が再初期化される限り、再アクティブ化されます。 これは、スキーマ変更の結果として再初期化が開始されることを意味します。 **1**の場合、スナップショットエージェントが実行されるまで、アクティブなサブスクリプションは再アクティブ化されません。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーを指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャーはパブリッシャー*に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は使用できません。  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure`ディストリビューターが存在しないかオフラインになっている場合でも、再初期化を許可します。 *ignore_distributor_failure*は**ビット**,、既定値は0です。 **0**の場合、ディストリビューターが存在しないかオフラインになっていると、再初期化は失敗します。  
  
`[ @invalidate_snapshot = ] invalidate_snapshot`既存のパブリケーションスナップショットを無効にします。 *invalidate_snapshot*は**ビット**,、既定値は0です。 **1**の場合、パブリケーションに対して新しいスナップショットが生成されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_reinitsubscription**は、トランザクションレプリケーションで使用します。  
  
 **sp_reinitsubscription**は、ピアツーピアトランザクションレプリケーションではサポートされていません。  
  
 初期スナップショットが自動的に適用され、パブリケーションで更新可能なサブスクリプションが許可されていないサブスクリプションでは、このストアドプロシージャの実行後にスナップショットエージェントを実行して、スキーマおよび一括コピープログラムファイルを準備する必要があります。ディストリビューションエージェントは、サブスクリプションを再同期できます。  
  
 初期スナップショットが自動的に適用され、パブリケーションで更新可能なサブスクリプションが許可される場合のサブスクリプションについては、ディストリビューション エージェントでサブスクリプションを再同期化するときに、スナップショット エージェントによって以前に作成された最新のスキーマおよび一括コピー プログラム ファイルが使用されます。 ディストリビューションエージェントがビジーでない場合、ディストリビューションエージェントは、ユーザーが**sp_reinitsubscription**を実行した直後にサブスクリプションを再同期します。それ以外の場合は、メッセージの間隔 (コマンドプロンプトパラメーターディストリビューションエージェントで指定) の後に同期が実行されることがあります。**MessageInterval**)。  
  
 **sp_reinitsubscription**は、初期スナップショットが手動で適用されるサブスクリプションには影響しません。  
  
 パブリケーションに対して匿名サブスクリプションを再同期するには、**すべて**または NULL を*サブスクライバー*として渡します。  
  
 トランザクション レプリケーションでは、アーティクル レベルでのサブスクリプションの再初期化がサポートされます。 アーティクルに再初期化のマークが付けられると、次の同期化の際に、アーティクルのスナップショットがサブスクライバーで再適用されます。 ただし、同じサブスクライバーにサブスクライブされる従属アーティクルがある場合は、特定の状況でパブリケーション内の従属アーティクルも自動的に再初期化されない限り、アーティクルへのスナップショットの再適用は失敗する可能性があります。  
  
-   アーティクルの事前作成コマンドが ' drop ' の場合、そのアーティクルのベースオブジェクトに対するスキーマバインドビューおよびスキーマバインドストアドプロシージャのアーティクルにも再初期化のマークが付けられます。  
  
-   アーティクルのスキーマ オプションに、主キーに関する宣言済みの参照整合性のスクリプト作成が含まれている場合は、再初期化されるアーティクルのベース テーブルに対して、外部キー リレーションシップが設定されているベース テーブルを持つアーティクルにも、再初期化のマークが付けられます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_reinitsubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、またはサブスクリプションの作成者だけです。  
  
## <a name="see-also"></a>関連項目  
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [サブスクリプションの再初期化](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
