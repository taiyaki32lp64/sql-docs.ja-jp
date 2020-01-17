---
title: sys.dm_filestream_file_io_handles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_filestream_file_io_handles
- sys.dm_filestream_file_io_handles
- dm_filestream_file_io_handles_TSQL
- sys.dm_filestream_file_io_handles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_handle catalog view
ms.assetid: e59632f4-3292-419f-9217-ca375749f1a5
author: stevestein
ms.author: sstein
ms.openlocfilehash: a96bcedaa3922ebb0691ac949f9eb15ed28336b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103301"
---
# <a name="sysdmfilestreamfileiohandles-transact-sql"></a>sys.dm_filestream_file_io_handles (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Namespace 所有者 (NSO) が知っているファイル ハンドルが表示されます。 クライアントを使用して取得した Filestream ハンドル**OpenSqlFilestream**がこのビューで表示されます。  
  
|[列]|種類|説明|  
|------------|----------|-----------------|  
|**handle_context_address**|**varbinary(8)**|クライアントのハンドルに関連付けられた内部 NSO 構造体のアドレスを示します。 NULL 値が許可されます。|  
|**creation_request_id**|**int**|このハンドルを作成するために使用した REQ_PRE_CREATE I/O 要求からのフィールドを示しています。 NULL 値は許可されません。|  
|**creation_irp_id**|**int**|このハンドルを作成するために使用した REQ_PRE_CREATE I/O 要求からのフィールドを示しています。 値が許容されません。|  
|**handle_id**|**int**|ドライバーによって割り当てられるこのハンドルの一意の ID を示しています。 NULL 値は許可されません。|  
|**creation_client_thread_id**|**varbinary(8)**|このハンドルを作成するために使用した REQ_PRE_CREATE I/O 要求からのフィールドを示しています。 NULL 値が許可されます。|  
|**creation_client_process_id**|**varbinary(8)**|このハンドルを作成するために使用した REQ_PRE_CREATE I/O 要求からのフィールドを示しています。 NULL 値が許可されます。|  
|**filestream_transaction_id**|**varbinary (128)**|特定のハンドルに関連付けられているトランザクションの ID を示します。 これは、によって返される値、 **get_filestream_transaction_context**関数。 このフィールドへの参加を使用して、 **sys.dm_filestream_file_io_requests**ビュー。 NULL 値が許可されます。|  
|**access_type**|**nvarchar(60)**|NULL 値は許可されません。|  
|**logical_path**|**nvarchar (256)**|このハンドルによって開かれたファイルの論理パス名を示します。 これは、によって返されるパス名と同じ、**します。パス名**メソッドの**varbinary**(**max**) filestream です。 NULL 値が許可されます。|  
|**physical_path**|**nvarchar (256)**|ファイルの実際の NTFS パス名を示します。 これは同じパス名がによって返される、**します。PhysicalPathName**のメソッド、 **varbinary**(**max**) filestream です。 トレース フラグ 5556 で有効です。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [Filestream および FileTable 動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
