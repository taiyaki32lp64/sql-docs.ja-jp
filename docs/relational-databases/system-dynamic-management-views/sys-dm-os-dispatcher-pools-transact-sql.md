---
title: sys.dm_os_dispatcher_pools (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: cf8e1700f51f808811a1f5a61f86777547c9cb65
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265852"
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セッション ディスパッチャー プールに関する情報を返します。 ディスパッチャー プールは、バック グラウンド処理を実行するシステム コンポーネントによって使用されるスレッド プールです。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_dispatcher_pools**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|ディスパッチャー プールのアドレス。 dispatcher_pool_address は一意です。 NULL 値は許可されません。|  
|type|**nvarchar (256)**|ディスパッチャー プールの種類。 NULL 値は許可されません。 ディスパッチャー プールの 2 種類があります。<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 完全な一覧については、DMV のクエリ|  
|NAME|**nvarchar (256)**|ディスパッチャー プールの名前。 NULL 値は許可されません。|  
|dispatcher_count|**int**|アクティブなディスパッチャー スレッドの数。 NULL 値は許可されません。|  
|dispatcher_ideal_count|**int**|ディスパッチャー プールを使用して拡張できるディスパッチャー スレッドの数。 NULL 値は許可されません。|  
|dispatcher_timeout_ms|**int**|ディスパッチャーが終了する前に新しい作業を待機するミリ秒単位の時間。 NULL 値は許可されません。|  
|dispatcher_waiting_count|**int**|アイドル状態のディスパッチャー スレッドの数。 NULL 値は許可されません。|  
|queue_length|**int**|ディスパッチャー プールによって処理されるを待機している作業項目の数。 NULL 値は許可されません。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="see-also"></a>関連項目  
  
  


