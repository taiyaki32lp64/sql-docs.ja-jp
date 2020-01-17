---
title: sys.dm_filestream_file_io_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4fb51b33655756d9c3c65dfcb5de3bae380ee9a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951034"
---
# <a name="sysdmfilestreamfileiorequests-transact-sql"></a>sys.dm_filestream_file_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定の時点で Namespace 所有者 (NSO) によってを処理中の I/O 要求の一覧を表示します。  
  
|[列]|種類|説明|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary(8)**|ドライバーからの I/O 要求を含む NSO メモリ ブロックの内部アドレスを示します。 NULL 値は許可されません。|  
|**current_spid**|**smallint**|現在の SQL Server の接続のシステム プロセス id (SPID) を示しています。 NULL 値は許可されません。|  
|**request_type**|**nvarchar(60)**|I/O 要求パケット (IRP) の種類を示します。 要求の種類は REQ_PRE_CREATE、REQ_POST_CREATE、REQ_RESOLVE_VOLUME、REQ_GET_VOLUME_INFO、REQ_GET_LOGICAL_NAME、REQ_GET_PHYSICAL_NAME、REQ_PRE_CLEANUP、REQ_POST_CLEANUP、REQ_CLOSE、REQ_FSCTL、REQ_QUERY_INFO、REQ_SET_INFO、REQ_ENUM_DIRECTORY、REQ_QUERY_SECURITY、および req_set_security があります。 値が許容されません。|  
|**request_state**|**nvarchar(60)**|NSO の I/O 要求の状態を示します。 REQ_STATE_RECEIVED、REQ_STATE_INITIALIZED、REQ_STATE_ENQUEUED、REQ_STATE_PROCESSING、REQ_STATE_FORMATTING_RESPONSE、REQ_STATE_SENDING_RESPONSE、REQ_STATE_COMPLETING、および REQ_STATE_COMPLETED のいずれかの値になります。 NULL 値は許可されません。|  
|**request_id**|**int**|この要求に、ドライバーによって割り当てられた一意の要求 ID を示します。 NULL 値は許可されません。|  
|**irp_id**|**int**|一意の IRP ID を示しています。 これは、特定の IRP に関連するすべての I/O 要求を識別する場合に役立ちます。 NULL 値は許可されません。|  
|**handle_id**|**int**|名前空間のハンドル ID が示されます これは NSO 固有の識別子で、インスタンス内で一意です。 NULL 値は許可されません。|  
|**client_thread_id**|**varbinary(8)**|要求を発信したクライアント アプリケーションのスレッドの ID を示します。<br /><br /> **\*\* 警告\* \*** これは、クライアント アプリケーションが SQL Server と同じコンピューターで実行されている場合にのみ意味を持ちます。 クライアント アプリケーションがリモートで実行されているときに、 **client_thread_id**リモート クライアントの代理として動作するいくつかのシステム プロセスのスレッド ID を示します。<br /><br /> NULL 値が許可されます。|  
|**client_process_id**|**varbinary(8)**|クライアント アプリケーションは、SQL Server と同じコンピューターで実行する場合は、クライアント アプリケーションのプロセス ID を示します。 リモート クライアントの場合は、クライアント アプリケーションの代わりに動作しているシステム プロセス ID を示します。 NULL 値が許可されます。|  
|**handle_context_address**|**varbinary(8)**|クライアントのハンドルに関連付けられた内部 NSO 構造体のアドレスを示します。 NULL 値が許可されます。|  
|**filestream_transaction_id**|**varbinary (128)**|特定のハンドルとこのハンドルに関連付けられたすべての要求に関連付けられているトランザクションの ID を示します。 によって返される値は、 **get_filestream_transaction_context**関数。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [Filestream および FileTable 動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
