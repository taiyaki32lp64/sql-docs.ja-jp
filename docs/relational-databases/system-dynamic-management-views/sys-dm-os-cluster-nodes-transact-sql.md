---
title: sys.dm_os_cluster_nodes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
author: stevestein
ms.author: sstein
ms.openlocfilehash: 44c42bfebdd1a5b4e74a4a95243fb0c0606e9908
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900253"
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  フェールオーバー クラスター インスタンスの構成にノードごとに 1 つの行を返します。 現在のインスタンスがフェールオーバー クラスター インスタンスの場合は、このフェールオーバー クラスター インスタンス (「仮想サーバー」以前) が定義されているノードの一覧を返します。 現在のサーバー インスタンスがフェールオーバー クラスター インスタンスではない場合は、空の行セットを返します。  
  
> **注:** これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_cluster_nodes**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**NodeName**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (仮想サーバー) 構成内のノードの名前。|  
|status|**int**|内のノードの状態、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]フェールオーバー クラスター インスタンス。0、1、2、3、-1。 詳細については、次を参照してください。 [GetClusterNodeState 関数](https://go.microsoft.com/fwlink/?LinkId=204794)します。|  
|status_description|**nvarchar(20)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター ノードの状態の説明。<br /><br /> 0 = up<br /><br /> 1 = down<br /><br /> 2 = 一時停止<br /><br /> 3 = joining<br /><br /> -1 = unknown|  
|is_current_owner|bit|1 は、このノードが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター リソースの現在の所有者であることを意味します。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="remarks"></a>コメント  
 フェールオーバー クラスタリングが有効な場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (仮想サーバー) 構成の一部として指定されているフェールオーバー クラスター内のどのノードでも実行できます。  
  
> **注:** このビューには、将来のリリースで非推奨の予定 fn_virtualservernodes 関数が置き換えられます。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、sys. dm_os_cluster_nodes を使用して、クラスター化されたサーバー インスタンスの割り当てノードを返します。  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1|  
|node2|0|up|0|  
|Node3|1|ダウン (down)|0|  
  
## <a name="see-also"></a>参照  
 [sys.dm_os_cluster_properties &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [sys.fn_virtualservernodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



