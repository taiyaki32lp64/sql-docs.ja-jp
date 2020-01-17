---
title: sp_revoke_proxy_from_subsystem (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8901c46c5654b6c633e03d62e8eaec2a3e903e02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022270"
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サブシステムに対するアクセス権をプロキシから取り消します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] id` アクセスを取り消すプロキシのプロキシ識別番号。 *Proxy_id*は**int**、既定値は NULL です。 いずれか*proxy_id*または*proxy_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @proxy_name = ] 'proxy_name'` アクセスを取り消すプロキシの名前。 *Proxy_name*は**sysname**、既定値は NULL です。 いずれか*proxy_id*または*proxy_name*指定する必要がありますが、両方を指定することはできません。  
  
`[ @subsystem_id = ] id` アクセスを取り消す対象となるサブシステムの id 番号。 *Subsystem_id*は**int**、既定値は NULL です。 いずれか*subsystem_id*または*subsystem_name*指定する必要がありますが、両方を指定することはできません。 次の表では、各サブシステムの値を示します。  
  
|値|説明|  
|-----------|-----------------|  
|**2**|ActiveX スクリプト<br /><br /> **\*\* 重要な \*\*** ActiveX スクリプティング サブシステムはから削除する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の将来のバージョンのエージェント[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。|  
|**3**|オペレーティング システム (CmdExec)|  
|**4**|レプリケーション スナップショット エージェント|  
|**5**|レプリケーション ログ リーダー エージェント|  
|**6**|レプリケーション ディストリビューション エージェント|  
|**7**|Replication Merge Agent|  
|**8**|Replication Queue Reader Agent|  
|**9**|Analysis Services コマンド|  
|"**10**"|Analysis Services クエリ|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ実行|  
|**12**|PowerShell スクリプト|  
  
`[ @subsystem_name = ] 'subsystem_name'` アクセスを取り消す対象となるサブシステムの名前。 *Subsystem_name*は**sysname**、既定値は NULL です。 いずれか*subsystem_id*または*subsystem_name*指定する必要がありますが、両方を指定することはできません。 次の表では、各サブシステムの値を示します。  
  
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
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ実行|  
|PowerShell|PowerShell スクリプト|  
  
## <a name="remarks"></a>コメント  
 サブシステムへのアクセスを取り消す場合は、プロキシで指定されるプリンシパルのアクセス許可は変更されません。  
  
> [!NOTE]  
>  プロキシを参照するジョブ ステップを確認するを右クリックし、**プロキシ**ノードの下**SQL Server エージェント**microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 をクリックし、**プロパティ**。 **プロキシ アカウントのプロパティ**ダイアログ ボックスで、**参照**このプロキシを参照するすべてのジョブ ステップを表示するページ。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_revoke_proxy_from_subsystem**します。  
  
## <a name="examples"></a>使用例  
 次の例では、プロキシ `Catalog application proxy` が持つ [!INCLUDE[ssIS](../../includes/ssis-md.md)] サブシステムへのアクセス権を取り消します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェント ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server エージェントのセキュリティを実装します。](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
