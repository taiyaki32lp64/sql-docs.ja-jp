---
title: sp_help_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 904a694d73613bb1c40c671b18ca33e5d9b5d0e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085285"
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つまたは複数のプロキシに関する情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] id` に関する情報を表示するプロキシのプロキシ識別番号。 *Proxy_id*は**int**、既定値は NULL です。 いずれか、 *id*または*proxy_name*指定することがあります。  
  
`[ @proxy_name = ] 'proxy_name'` に関する情報を表示するプロキシの名前。 *Proxy_name*は**sysname**、既定値は NULL です。 いずれか、 *id*または*proxy_name*指定することがあります。  
  
`[ @subsystem_name = ] 'subsystem_name'` プロキシを一覧表示するサブシステムの名前。 *Subsystem_name*は**sysname**、既定値は NULL です。 ときに*subsystem_name*が指定されている*名前*も指定する必要があります。  
  
 次の表では、各サブシステムの値を示します。  
  
|[値]|説明|  
|-----------|-----------------|  
|ActiveScripting|ActiveX スクリプト|  
|CmdExec|オペレーティング システム (CmdExec)|  
|スナップショット|レプリケーション スナップショット エージェント|  
|LogReader|レプリケーション ログ リーダー エージェント|  
|Distribution|レプリケーション ディストリビューション エージェント|  
|Merge|Replication Merge Agent|  
|QueueReader|Replication Queue Reader Agent|  
|ANALYSISQUERY|Analysis Services コマンド|  
|ANALYSISCOMMAND|Analysis Services クエリ|  
|Dts|SSIS パッケージ実行|  
|PowerShell|PowerShell スクリプト|  
  
`[ @name = ] 'name'` 名前、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログイン プロキシを一覧表示します。 名前は**nvarchar (256)** 、既定値は NULL です。 ときに*名前*が指定されている*subsystem_name*も指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシ識別番号。|  
|**name**|**sysname**|プロキシの名前。|  
|**credential_identity**|**sysname**|Microsoft Windows ドメインの名前と、プロキシに関連付けられている資格情報のユーザー名。|  
|**enabled**|**tinyint**|プロキシが有効かどうか { **0** = 無効、 **1** = 有効}|  
|**description**|**nvarchar(1024)**|このプロキシの説明です。|  
|**user_sid**|**varbinary(85)**|プロキシに関する Windows ユーザーの Windows セキュリティ ID|  
|**credential_id**|**int**|このプロキシに関連付けられている資格情報の識別子。|  
|**credential_identity_exists**|**int**|credential_identity が存在するかどうか {0 = 1 が存在しない = が存在する}|  
  
## <a name="remarks"></a>コメント  
 パラメーターが指定されていないときに**sp_help_proxy**インスタンス内のすべてのプロキシ情報を一覧表示します。  
  
 プロキシ ログインできるサブシステムの使用を確認するのには、指定*名前*と*subsystem_name*します。 これらの引数が指定された場合、 **sp_help_proxy**がアクセスとを使用できます、指定したサブシステムのログインが指定されているプロキシを一覧表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 それ以外のユーザーには、 **msdb** データベースの **SQLAgentOperatorRole** 固定サーバー ロールを与える必要があります。  
  
 詳細については**SQLAgentOperatorRole**を参照してください[SQL Server エージェント固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)します。  
  
> [!NOTE]  
>  **Credential_identity**と**user_sid**でのみ列が返されます場合の結果セットのメンバー **sysadmin**このストアド プロシージャを実行します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-information-for-all-proxies"></a>A. すべてのプロキシに関する情報を一覧表示する  
 次の例では、インスタンス内のすべてのプロキシに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. 特定のプロキシに関する情報を表示  
 次の例では、という名前のプロキシ情報を一覧表示`Catalog application proxy`します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
