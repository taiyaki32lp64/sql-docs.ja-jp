---
title: sp_helplogreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
author: stevestein
ms.author: sstein
ms.openlocfilehash: b6ecac979077dd83d6549b408c8c9e4d2bd4402f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122440"
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  パブリケーション データベースに対してログ リーダー エージェント ジョブのプロパティを返します。 このストアド プロシージャは、パブリッシャー側でパブリケーション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値は NULL です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|エージェントの ID。|  
|**name**|**nvarchar(100)**|エージェントの名前。|  
|**publisher_security_mode**|**smallint**|次のいずれかの値と、パブリッシャーに接続するときに、エージェントで使用されるセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証<br /><br /> **1** = Windows 認証。|  
|**publisher_login**|**sysname**|パブリッシャーに接続するときに使用されるログイン。|  
|**publisher_password**|**nvarchar(524)**|セキュリティ上の理由から、値の **\* \* \* \* \* \* \* \* \* \*** は常に返されます。|  
|**job_id**|**uniqueidentifier**|エージェント ジョブの一意の ID。|  
|**job_login**|**nvarchar(512)**|形式で返される、ログ リーダー エージェントを実行する Windows アカウントは、*ドメイン*\\*username*します。|  
|**job_password**|**sysname**|セキュリティ上の理由から、値の **\* \* \* \* \* \* \* \* \* \*** は常に返されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helplogreader_agent**はトランザクション レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールのメンバー、または発行元、 **db_owner**パブリケーション データベースの固定データベース ロールが実行できる**sp_helplogreader_agent**.  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
