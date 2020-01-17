---
title: sp_MSchange_merge_agent_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 84c517fe891052ff6e12ee6e92a2d16d912a140b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905193"
---
# <a name="sp_mschange_merge_agent_properties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  実行されるマージ エージェント ジョブのプロパティを変更、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]またはそれ以降のバージョンのディストリビューター。 このストアド プロシージャがパブリッシャーのインスタンス上の実行時にプロパティを変更する使用[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]します。 このストアド プロシージャは、ディストリビューター側でディストリビューション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *publisher* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーション データベースの名前です。 *publisher_db* は **sysname** 、既定値はありません。  
  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *publication* は **sysname** 、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前です。 *subscriber*は**sysname**、既定値はありません。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプション データベースの名前です。 *subscriber_db*は**sysname**、既定値はありません。  
  
`[ @property = ] 'property'` 変更するパブリケーションのプロパティです。 *プロパティ*は**sysname**、既定値はありません。  
  
`[ @value = ] 'value'` 新しいプロパティ値です。 *value*は**nvarchar (524)** 、既定値は NULL です。  
  
 次の表では、これらのプロパティの値を変更できるマージ エージェント ジョブと制約事項のプロパティについて説明します。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**description**||サブスクリプションの簡単な説明。|  
|**merge_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**merge_job_password**||エージェント ジョブを実行する Windows アカウントのパスワード。|  
|**publisher_login**||サブスクリプションの同期で、パブリッシャーに接続するときに使用するログイン。|  
|**publisher_password**||パブリッシャーのパスワード。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Windows 認証。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。|  
|**subscriber_login**||サブスクリプションを同期するサブスクライバーに接続するときに使用するログイン。|  
|**subscriber_password**||サブスクライバーのパスワード。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Windows 認証。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。|  
  
> [!NOTE]  
>  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_MSchange_merge_agent_properties**はマージ レプリケーションで使用します。  
  
 インスタンスで、パブリッシャーを実行するときに[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降のバージョンを使用する必要がありますまたは[sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)ディストリビューターで実行されているプッシュ サブスクリプションを同期するマージ エージェント ジョブのプロパティを変更します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin** 、ディストリビューター側の固定サーバー ロールが実行できる**sp_MSchange_merge_agent_properties**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_addmergepushsubscription_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
