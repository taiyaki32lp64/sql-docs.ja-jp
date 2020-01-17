---
title: sys.dm_os_child_instances (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 59a58348f5428f568f40d28b4e83bc6bc040647c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900233"
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  親サーバー インスタンスから作成されたユーザー インスタンスごとに 1 行のデータを返します。  
  
> **重要:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 返される情報**sys.dm_os_child_instances** (heart_beat) ごとのユーザー インスタンスの状態を確認して、ユーザーへの接続を作成するために使用できるパイプ名 (instance_pipe_name) を取得するために使用できますインスタンスを使用して[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]または SQLCmd します。 ユーザー インスタンスがクライアント アプリケーションなどの外部プロセスによって開始された場合のみ、ユーザー インスタンスに接続できます。 SQL 管理ツールではユーザー インスタンスを開始できません。  
  
> **注:** ユーザー インスタンスは、[!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] のみの機能です。  
> 
> **注**これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_child_instances**します。  
  
|[列]|データ型|説明|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar (256)**|このユーザー インスタンスに対応するユーザーの名前です。|  
|owning_principal_sid|nvarchar (256)|このユーザー インスタンスを所有するプリンシパルの SID (セキュリティ識別子) です。 この値は、Windows SID と一致します。|  
|owning_principal_sid_binary|varbinary (85)|このユーザー インスタンスを所有するユーザーの SID のバイナリ バージョンです。|  
|**instance_name**|**nvarchar(128)**|このユーザー インスタンスの名前です。|  
|**instance_pipe_name**|**nvarchar(260)**|ユーザー インスタンスを作成すると、アプリケーションから接続するための名前付きパイプが作成されます。 この名前を接続文字列中で使用することにより、ユーザー インスタンスに接続できます。|  
|**os_process_id**|**Int**|このユーザー インスタンスに対応する、Windows プロセスのプロセス番号です。|  
|**os_process_creation_date**|**DateTime**|このユーザー インスタンス プロセスの前回の開始日付と時刻です。|  
|**heart_beat**|**nvarchar(5)**|このユーザー インスタンスの現在の状態 (ALIVE または DEAD) です。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 動的管理ビューの詳細については、次を参照してください。[動的管理ビューおよび関数&#40;TRANSACT-SQL&#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="see-also"></a>参照  
 [管理者以外のユーザー インスタンス](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



