---
title: sp_addpullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7f65d868f7560f1e413b8c28308afac495233102
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769081"
---
# <a name="sp_addpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  スナップショット パブリケーションまたはトランザクション パブリケーションにプル サブスクリプションを追加します。 このストアド プロシージャは、プル サブスクリプションが作成されるデータベース上のサブスクライバー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db*は**sysname**,、既定値は NULL です。 *publisher_db*は、Oracle パブリッシャーでは無視されます。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @independent_agent = ] 'independent_agent'`このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうかを指定します。 *independent_agent*は**nvarchar (5)** ,、既定値は TRUE です。 **True**の場合、このパブリケーションにはスタンドアロンのディストリビューションエージェントがあります。 **False**の場合、パブリッシャーデータベース/サブスクライバーデータベースのペアごとに1つのディストリビューションエージェントが存在します。 *independent_agent*はパブリケーションのプロパティであり、ここではパブリッシャー側と同じ値である必要があります。  
  
`[ @subscription_type = ] 'subscription_type'`サブスクリプションの種類を示します。 *subscription_type*は**nvarchar (9)** ,、既定値は**anonymous**です。 パブリッシャーでサブスクリプションを登録せずにサブスクリプションを作成する場合を除き、 *subscription_type*には**pull**の値を指定する必要があります。 この場合、**匿名**の値を指定する必要があります。 これは、サブスクリプションの構成時にパブリッシャーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続を確立できない場合に必要です。  
  
`[ @description = ] 'description'`パブリケーションの説明を示します。 *説明*は**nvarchar (100)** ,、既定値は NULL です。  
  
`[ @update_mode = ] 'update_mode'`更新の種類を示します。 *update_mode*は**nvarchar (30)** ,、値は次のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**読み取り**専用標準|サブスクリプションは読み取り専用です。 サブスクライバーでの変更は、パブリッシャーに送り返されません。 サブスクライバーで更新が行われない場合は、を使用する必要があります。|  
|**synctran**|即時更新サブスクリプションのサポートを有効にします。|  
|**キューに登録されたトランザクション**|サブスクリプションのキュー更新を有効にします。 サブスクライバーでデータ変更を行い、キューに格納して、パブリッシャーに反映することができます。|  
|**用**|キュー更新をフェールオーバーとするサブスクリプションの即時更新を有効にします。 サブスクライバーでデータを変更し、それを直ちにパブリッシャーに配信することができます。 パブリッシャーとサブスクライバーが接続されていない場合は、サブスクライバーとパブリッシャーが接続されるまで、サブスクライバーで加えられたデータの変更をキューに格納することができます。|  
|**キューに置かれたフェールオーバー**|即時更新モードへの変更が可能なキュー更新サブスクリプションとしてサブスクリプションを有効にします。 サブスクライバーでデータを変更し、サブスクライバーとパブリッシャーの間に接続が確立されるまで、キューに格納することができます。 連続接続が確立されると、更新モードを即時更新に変更できます。 *Oracle パブリッシャーではサポートされていません*。|  
  
`[ @immediate_sync = ] immediate_sync`スナップショットエージェントを実行するたびに同期ファイルを作成または再作成するかどうかを指定します。 *immediate_sync*は**ビット**既定値は1で、 **sp_addpublication**の*immediate_sync*と同じ値に設定する必要があります。*immediate_sync*はパブリケーションのプロパティであり、ここではパブリッシャー側と同じ値である必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addpullsubscription**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
> [!IMPORTANT]  
>  キュー更新サブスクリプションの場合、サブスクライバーへの接続には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用し、各サブスクライバーへの接続にはそれぞれ異なるアカウントを指定してください。 キュー更新をサポートするプル サブスクリプションを作成する場合は、レプリケーションによって、常に Windows 認証を使用するように接続が設定されます (プル サブスクリプションでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するために必要な、サブスクライバー側のメタデータにレプリケーションからアクセスすることはできません)。 この場合、サブスクリプションの構成後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するように接続を変更するには、[sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) を実行する必要があります。  
  
 [ &#40;MSreplication_subscriptions transact-sql&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)テーブルがサブスクライバーに存在しない場合は、 **sp_addpullsubscription**によって作成されます。 また、 [MSreplication_subscriptions &#40;transact-sql&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)テーブルに行を追加します。 プルサブスクリプションの場合は、最初にパブリッシャーで[sp_addsubscription &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)を呼び出す必要があります。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addpullsubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [トランザクションパブリケーションに対する更新可能なサブスクリプションの作成](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)[パブリケーションをサブスクライブする](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
