---
title: sp_addlogreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a50b989afef382a8315c29ea5257ad9b103e124c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769222"
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  データベースにログ リーダー エージェントを追加します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_login = ] 'job_login'`エージェントを実行する[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログインを指定します。 *job_login*は**nvarchar (257)** ,、既定の値は NULL です。 この Windows アカウントは、ディストリビューターへのエージェント接続に常に使用されます。  
  
> [!NOTE]
>  以外[!INCLUDE[msCoName](../../includes/msconame-md.md)] [ &#40;&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)のパブリッシャーの場合は、sp_adddistpublisher で指定されたログインと同じである必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
`[ @job_password = ] 'job_password'`エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password*は**sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを最大限に高めるには、ログイン名とパスワードを実行時に指定する必要があります。  
  
`[ @job_name = ] 'job_name'`既存のエージェントジョブの名前を指定します。 *job_name* は **sysname** 既定値は NULL です。 このパラメーターは、新しく作成されたジョブ (既定値) ではなく、既存のジョブを使用してエージェントを起動する場合にのみ指定します。  
  
`[ @publisher_security_mode = ] publisher_security_mode`パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode*は**smallint**,、既定値は**1**です。 **0 は認証を**、1は Windows 認証を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーには、値**0**を指定する必要があります。  
  
`[ @publisher_login = ] 'publisher_login'`パブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname** 、既定値は NULL です。 *publisher_security_mode*が**0**の場合は、 *publisher_login*を指定する必要があります。 *Publisher_login*が NULL で*publisher_security_mode*が**1**の場合、 *Job_login*に指定されている Windows アカウントがパブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'`パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname** 、既定値は NULL です。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを最大限に高めるには、ログイン名とパスワードを実行時に指定する必要があります。  
  
`[ @publisher = ] 'publisher'`以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーの場合はこのパラメーターを指定しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_addlogreader_agent**は、トランザクションレプリケーションで使用します。  
  
 データベースを使用するパブリケーションを作成する前に、このバージョンのへの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]レプリケーションが有効になっているデータベースをアップグレードした場合は、sp_addlogreader_agent を実行してログリーダーエージェントを追加する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addlogreader_agent**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>関連項目  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
