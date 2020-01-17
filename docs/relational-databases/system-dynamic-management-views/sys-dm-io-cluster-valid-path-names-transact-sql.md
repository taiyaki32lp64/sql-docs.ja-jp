---
title: sys.dm_io_cluster_valid_path_names (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs:
- TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
author: stevestein
ms.author: sstein
ms.openlocfilehash: ff2348efe62929bdfbe03b4c92b5d411f57c2b99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900357"
---
# <a name="sysdmioclustervalidpathnames-transact-sql"></a>sys.dm_io_cluster_valid_path_names (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  SQL Server フェールオーバー クラスター インスタンスに対応するクラスター化ボリュームを含む、すべての有効な共有ディスクに関する情報を返します。 インスタンスがクラスター化されていない場合は、空の行セットが返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**path_name**|**Nvarchar(512)**|ボリューム マウント ポイント パスまたはドライブ パス データベースとログ ファイルのルート ディレクトリとして使用できます。 NULL 値は許可されません。|  
|**cluster_owner_node**|**Nvarchar(64)**|ドライブの現在の所有者。 クラスターの共有ボリューム (CSV) の所有者は、メタデータ サーバーをホストしているノードです。 NULL 値は許可されません。|  
|**is_cluster_shared_volume**|**Bit**|このパスを含むドライブがクラスター化ボリュームの場合は 1 を返します。それ以外の場合は 0 を返します。|  
  
## <a name="remarks"></a>コメント  
 SQL Server フェールオーバー クラスター インスタンス (FCI) では、データとログ ファイルの記憶域は FCI のすべてのノード間の共有記憶域を使用する必要があります。 このビューで表示されるディスクは、インスタンスに関連付けられたクラスター リソース グループにあり、データまたはログ ファイルの記憶域に使用できるディスクのみ。  
  
> [!NOTE]  
>  このビューに置き換わります[sys.dm_io_cluster_shared_drives &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)将来のリリースでします。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、sys.dm_io_cluster_valid_path_names を使用して、クラスター サーバー インスタンスの共有デバイスを特定します。  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

