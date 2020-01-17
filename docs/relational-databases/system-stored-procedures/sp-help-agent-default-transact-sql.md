---
title: sp_help_agent_default (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: c0797b8fe4a2ba496b28f0c347eb5349e77e91e0
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762760"
---
# <a name="sphelpagentdefault-transact-sql"></a>sp_help_agent_default (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  パラメーターとして渡されたエージェント タイプについて、既定の構成の ID を取得します。 このストアド プロシージャは、任意のデータベース上のディストリビューター側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>引数  
`[ @profile_id = ] _profile_idOUTPUT`エージェントの種類の既定の構成の ID を設定します。 *profile_id*は**int**,、既定値はありません。*profile_id*は出力パラメーターでもあり、エージェントの種類の既定の構成の id を返します。  
  
`[ @agent_type = ] 'agent_type'`エージェントの種類を示します。 *agent_type*は**int**,、既定値はありませんが、これらの値のいずれかを指定することができます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|スナップショットエージェント。|  
|**2**|ログ リーダー エージェント|  
|**3**|ディストリビューションエージェント。|  
|**4**|マージエージェント。|  
|**9**|キュー リーダー エージェント (Queue Reader Agent)|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_help_agent_default**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_help_agent_default**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**replmonitor**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
