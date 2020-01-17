---
title: sp_enum_sqlagent_subsystems (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 963cbcea93091eb48b8c73214ee3bc509f118e67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124673"
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  一覧表示、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サブシステムです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>引数  
 なし  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|サブシステムの名前。|  
|**description**|**nvarchar(512)**|サブシステムの説明。|  
|**subsystem_dll**|**nvarchar(510)**|サブシステムを格納している DLL モジュール|  
|**agent_exe**|**nvarchar(510)**|サブシステムによって使用される実行可能モジュール。|  
|**start_entry_point**|**nvarchar(30)**|SQL Server エージェントがジョブ ステップの実行中に呼び出すプロシージャです。|  
|**event_entry_point**|**nvarchar(30)**|SQL Server エージェントがジョブ ステップの実行中に呼び出すプロシージャです。|  
|**stop_entry_point**|**nvarchar(30)**|SQL Server エージェントがジョブ ステップの実行中に呼び出すプロシージャです。|  
|**max_worker_threads**|**int**|スレッドの最大数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]このサブシステム用にエージェントが開始されます。|  
|**subsystem_id**|**int**|サブシステムの識別子|  
  
## <a name="remarks"></a>コメント  
 この手順では、インスタンスで使用できるサブシステムが一覧表示します。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 それ以外のユーザーには、 **msdb** データベースの **SQLAgentOperatorRole** 固定サーバー ロールを与える必要があります。  
  
 詳細については**SQLAgentOperatorRole**を参照してください[SQL Server エージェント固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェントのセキュリティを実装します。](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
