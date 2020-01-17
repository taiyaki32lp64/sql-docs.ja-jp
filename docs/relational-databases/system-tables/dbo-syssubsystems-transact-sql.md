---
title: dbo.syssubsystems (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3f06182f06e92ff581dd02c072b63fc10962921a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069085"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用可能なすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのプロキシ サブシステムに関する情報を格納します。 **Syssubsystems**でテーブルが格納されている、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|サブシステムの ID。|  
|**subsystem**|**nvarchar(40)**|サブシステムの名前。|  
|**description_id**|**int**|メッセージ内の行の ID、 **sys.messages**カタログ サブシステムの説明を含むビュー。|  
|**subsystem_dll**|**nvarchar (255)**|サブシステム DLL の場所です。|  
|**agent_exe**|**nvarchar (255)**|サブシステムを使用する実行可能ファイルの完全パスです。|  
|**start_entry_point**|**nvarchar(30)**|サブシステムが初期化されるときに呼び出される関数。|  
|**event_entry_point**|**nvarchar(30)**|サブシステム ステップが実行されるときに呼び出される関数。|  
|**stop_entry_point**|**nvarchar(30)**|サブシステムが実行を終了するときに呼び出される関数。|  
|**max_worker_threads**|**int**|サブシステムの同時ステップの最大数。|  
  
## <a name="remarks"></a>コメント  
 メンバーのみ、 **sysadmin**固定サーバー ロールがこのテーブルにアクセスできます。  
  
## <a name="see-also"></a>関連項目  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
