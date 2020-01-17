---
title: sp_MSchange_logreader_agent_properties (T-sql)
description: SQL Server レプリケーショントポロジのログリーダーエージェントのプロパティを変更するために使用される sp_MSchange_logreader_agent_properties ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 37a36218b4e9e93a761c776e76a6596f40a6c0eb
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322289"
---
# <a name="sp_mschange_logreader_agent_properties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以降のバージョンの[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ディストリビューターで実行されるログリーダーエージェントジョブのプロパティを変更します。 このストアドプロシージャは、パブリッシャーがの[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]インスタンスで実行されている場合に、プロパティを変更するために使用します。 このストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*は**sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリケーションデータベースの名前を指定します。 *publisher_db*は**sysname**であり、既定値はありません。  
  
`[ @publisher_security_mode = ] publisher_security_mode`パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode*は**smallint**,、既定値はありません。  
  
 **0**は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。  
  
 **1** Windows 認証を指定します。  
  
`[ @publisher_login = ] 'publisher_login'`パブリッシャーに接続するときに使用するログインを示します。 *publisher_login*は**sysname**であり、既定値はありません。 *publisher_security_mode*が**0**の場合は*publisher_login*を指定する必要があります。 *Publisher_login*が NULL で*publisher_security_mode*が**1**の場合、 *job_login*で指定された Windows アカウントがパブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'`パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password*は**sysname**であり、既定値はありません。  
  
`[ @job_login = ] 'job_login'`エージェントを実行する Windows アカウントのログインを指定します。 *job_login*は**nvarchar (257)**,、既定値はありません。 *これは、以外*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のパブリッシャーに対しては変更できません *。*  
  
`[ @job_password = ] 'job_password'`エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password*は**sysname**であり、既定値はありません。  
  
`[ @publisher_type = ] 'publisher_type'`パブリッシャーがの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスで実行されていない場合のパブリッシャーの種類を指定します。 *publisher_type*は**sysname**で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**MS**|パブリッシャーを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定します。|  
|**ORACLE11I**|標準の Oracle パブリッシャーを指定します。|  
|**ORACLE GATEWAY **|Oracle ゲートウェイ パブリッシャーを指定します。|  
  
 Oracle パブリッシャーと Oracle ゲートウェイパブリッシャーの相違点の詳細については、「 [Oracle パブリッシングの概要](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)」を参照してください。  
  
## <a name="remarks"></a>コメント  
 **sp_MSchange_logreader_agent_properties**は、トランザクションレプリケーションで使用します。  
  
 **Sp_MSchange_logreader_agent_properties**を実行するときは、すべてのパラメーターを指定する必要があります。 [&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)を実行 sp_helplogreader_agent て、ログリーダーエージェントジョブの現在のプロパティを返します。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
 パブリッシャーが以降のバージョンの[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]インスタンスで実行されている場合は、 [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)を使用してログリーダーエージェントのプロパティを変更する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_MSchange_logreader_agent_properties**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addlogreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
