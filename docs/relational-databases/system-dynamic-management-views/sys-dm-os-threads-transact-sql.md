---
title: dm_os_threads (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8eeeaaf59934d6c3307641b6c93f110ab5738f
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982537"
---
# <a name="sysdm_os_threads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オペレーティング システム スレッドの一覧を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_threads**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|スレッドのメモリ アドレス (主キー)。|  
|started_by_sqlservr|**bit**|スレッドの開始元。<br /><br /> 1 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってスレッドが開始されました。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の拡張ストアド プロシージャなど、スレッドを開始した他のコンポーネント。|  
|os_thread_id|**int**|オペレーティング システムによって割り当てられたスレッドの ID。|  
|ステータス|**int**|内部状態フラグ。|  
|instruction_address|**varbinary(8)**|現在実行されている命令のアドレス。|  
|creation_time|**datetime**|スレッドが作成された日時。|  
|kernel_time|**bigint**|スレッドで使用されたカーネル時間。|  
|usermode_time|**bigint**|スレッドで使用されたユーザー時間。|  
|stack_base_address|**varbinary(8)**|スレッドにおける最上位のスタック アドレスのメモリ アドレス。|  
|stack_end_address|**varbinary(8)**|スレッドにおける最下位のスタック アドレスのメモリ アドレス。|  
|stack_bytes_committed|**int**|スタックでコミットされたバイト数。|  
|stack_bytes_used|**int**|スレッドでアクティブに使用されているバイト数。|  
|affinity|**bigint**|このスレッドが実行されている CPU マスク。 これは、 **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY**ステートメントで構成された値によって異なります。 ソフト アフィニティの場合は、スケジューラと異なることがあります。|  
|[Priority]|**int**|スレッドの優先度値。|  
|ロケール|**int**|スレッド用にキャッシュされているロケール LCID。|  
|トークン|**varbinary(8)**|スレッド用にキャッシュされている権限借用トークン ハンドル。|  
|is_impersonating|**int**|スレッドで Win32 権限借用が使用されているかどうかを示します。<br /><br /> 1 = スレッドではプロセスの既定値と異なるセキュリティ資格情報が使用されています。 これは、プロセスを作成したエンティティとは異なるエンティティの権限をスレッドで借用していることを示します。|  
|is_waiting_on_loader_lock|**int**|スレッドでローダー ロックを待機中かどうかを示す、オペレーティング システムの状態。|  
|fiber_data|**varbinary(8)**|スレッドで実行されている現在の Win32 ファイバー。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が簡易プーリング用に構成されている場合にのみ該当します。|  
|thread_handle|**varbinary(8)**|内部使用のみです。|  
|event_handle|**varbinary(8)**|内部使用のみです。|  
|scheduler_address|**varbinary(8)**|スレッドに関連付けられているスケジューラのメモリ アドレス。 詳細については、「 [sys &#40;. dm_os_schedulers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)」を参照してください。|  
|worker_address|**varbinary(8)**|スレッドにバインドしているワーカーのメモリ アドレス。 詳細については、「 [sys &#40;. dm_os_workers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)」を参照してください。|  
|fiber_context_address|**varbinary(8)**|内部ファイバー コンテキスト アドレス。 これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が簡易プーリング用に構成されている場合にのみ該当します。|  
|self_address|**varbinary(8)**|内部一貫性ポインター。|  
|processor_group|**smallint**|**適用対象**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 以降。<br /><br /> プロセッサ グループ ID。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="notes-on-linux-version"></a>Linux のバージョンに関する注意事項

Linux での SQL エンジンの動作によって、この情報の一部が Linux 診断データと一致しません。 たとえば、`os_thread_id` が `ps`、`top`、procfs (/proc/`pid`) などのツールの結果と一致しません。  これは、プラットフォームアブストラクションレイヤー (SQLPAL)、SQL Server コンポーネントとオペレーティングシステムの間のレイヤーです。

## <a name="examples"></a>使用例  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、起動時にスレッドが開始され、これらのスレッドとワーカーが関連付けられますが、 拡張ストアド プロシージャなどの外部コンポーネントでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスでスレッドを開始できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれらのスレッドを制御できません。 dm_os_threads は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス内のリソースを消費する悪意のあるスレッドに関する情報を提供できます。  
  
 次のクエリを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって開始されなかったスレッドを実行しているワーカーと、実行に使用された時間を特定できます。  
  
> [!NOTE]
>  次のクエリでは、簡略化のため `*` ステートメントでアスタリスク (`SELECT`) を使用していますが、 特にカタログ ビュー、動的管理ビュー、およびシステム テーブル値関数では、アスタリスク (*) を使用しないようにしてください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のアップグレードおよびリリースでは、列を追加し、これらのビューおよび関数に列の順序を変更することができます。 このような変更により、特定の順序および列数を必要とするアプリケーションが機能しなくなる場合があります。  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>参照  
  [dm_os_workers &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


