---
title: sys.dm_io_cluster_shared_drives (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_shared_drives_TSQL
- sys.dm_io_cluster_shared_drives
- dm_io_cluster_shared_drives_TSQL
- dm_io_cluster_shared_drives
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_cluster_shared_drives dynamic management view
ms.assetid: c8fcced8-c780-49dc-99bd-6beb3ca532c4
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6633988bf660de8225b201266a4f2ef7ebea55e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900386"
---
# <a name="sysdmioclustershareddrives-transact-sql"></a>sys.dm_io_cluster_shared_drives (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  このビューは、現在のサーバー インスタンスがクラスター化されたサーバーの場合、各共有ドライブのドライブ名を返します。 現在のサーバー インスタンスがクラスター化されたインスタンスではない場合は、空の行セットを返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_io_cluster_shared_drives**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DriveName**|**nchar(2)**|クラスター共有ディスク アレイに参加している個々 のディスクを表すドライブ (ドライブ文字) の名前。 列値が許容されません。|  
|**pdw_node_id**|**int**|**適用対象**: ssPDW<br /><br /> この配布であるノードの識別子。|  
  
## <a name="remarks"></a>コメント  
 クラスタ リングが有効になっているときに、フェールオーバー クラスター インスタンスには、データが必要ですし、インスタンスの後にアクセスできるように共有ディスク上にログ ファイルが別のノードにフェールオーバーします。 このビューの各行は、クラスター化された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで使用される 1 つの共有ディスクを表します。 データを格納したり、ログ ファイルのこのインスタンスをこのビューで表示されているディスクのみを使用できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このビューで表示されるディスクは、インスタンスに関連付けられているクラスター リソース グループ内にあるものです。  
  
> [!NOTE]  
>  このビューは、将来のリリースで非推奨とされます。 使用することをお勧めします。 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)代わりにします。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、sys.dm_io_cluster_shared_drives を使用して、クラスター サーバー インスタンスの共有デバイスを特定します。  
  
```  
SELECT * FROM sys.dm_io_cluster_shared_drives;  
```  
  
 これは、結果セットです。  
  
 DriveName  
  
 --------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_io_cluster_valid_path_names &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.fn_servershareddrives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)   
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
