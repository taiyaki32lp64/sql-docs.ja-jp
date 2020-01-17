---
title: sp_changeqreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: b636eb929d74aec7b0f3555ce511372f6592c5b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099137"
---
# <a name="spchangeqreaderagent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  キュー リーダー エージェントのセキュリティのプロパティを変更します。 このストアド プロシージャは、ディストリビューターのディストリビューション データベースで、またはパブリケーション データベースに対して、パブリッシャー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>引数  
`[ @job_login = ] 'job_login'` 用のログイン、[!INCLUDE[msCoName](../../includes/msconame-md.md)]エージェントを実行する Windows アカウントします。 *job_login*は**nvarchar (257)** 、既定値は NULL です。  
  
`[ @job_password = ] 'job_password'` エージェントを実行する Windows アカウントのパスワードです。 *job_password*は**sysname**、既定値は NULL です。  
  
`[ @frompublisher = ] frompublisher` プロシージャがパブリッシャーで実行されているかどうかです。 *frompublisher*は bit で、既定値は、 **0**します。 値**1**プロシージャがパブリッシャーのパブリケーション データベースから実行されていることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changeqreader_agent**はトランザクション レプリケーションで使用します。  
  
 **sp_changeqreader_agent**キュー リーダー エージェントを実行する Windows アカウントを変更するために使用します。 既存の Windows ログインのパスワードを変更したり、新しい Windows ログインとパスワードを指定できます。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_changeqreader_agent**します。  
  
## <a name="see-also"></a>関連項目  
 [レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
