---
title: sys.dm_os_sys_memory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_sys_memory
- sys.dm_os_sys_memory_TSQL
- sys.dm_os_sys_memory
- dm_os_sys_memory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_memory dynamic management view
ms.assetid: 1ca58814-1caa-44c1-b307-ff0bdcbbef62
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ca8b0f6e700e97c5cbc33964cc450ad54ea1a7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899711"
---
# <a name="sysdmossysmemory-transact-sql"></a>sys.dm_os_sys_memory (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  オペレーティング システムからメモリ情報を返します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって制限し、オペレーティング システム レベルおよび基になるハードウェアの物理的な制限で外部メモリ状況に応答します。 システム全体の状態を調査することは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメモリ使用量を評価するうえで重要な要素です。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_sys_memory**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**total_physical_memory_kb**|**bigint**|キロバイト (KB) で、オペレーティング システムで使用できる物理メモリの合計サイズ。|  
|**available_physical_memory_kb**|**bigint**|(KB 単位) を使用できる物理メモリのサイズ。|  
|**total_page_file_kb**|**bigint**|オペレーティング システムによって報告されたコミット制限のサイズ (KB 単位)。|  
|**available_page_file_kb**|**bigint**|使用されていない、サポート技術情報でページファイルの合計サイズ。|  
|**system_cache_kb**|**bigint**|システム キャッシュ メモリの合計サイズ (KB 単位)。|  
|**kernel_paged_pool_kb**|**bigint**|ページ カーネル プールの合計サイズ (KB 単位)。|  
|**kernel_nonpaged_pool_kb**|**bigint**|(KB 単位)、非ページ カーネル プールの合計サイズ。|  
|**system_high_memory_signal_state**|**bit**|システムの高メモリ リソース通知の状態。 この値が 1 の場合、Windows によって高メモリ シグナルが設定されていることを意味します。 詳細については、次を参照してください。 [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) 、MSDN ライブラリ。|  
|**system_low_memory_signal_state**|**bit**|システムの低いメモリ リソース通知の状態。 値 1 では、Windows によって低いメモリ シグナルが設定されていることを示します。 詳細については、次を参照してください。 [CreateMemoryResourceNotification](https://go.microsoft.com/fwlink/?LinkId=82427) 、MSDN ライブラリ。|  
|**system_memory_state_desc**|**nvarchar (256)**|メモリの状態の説明です。 次の表を参照してください。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
|条件|値|  
|---------------|-----------|  
|system_high_memory_signal_state = 1<br /><br /> 、<br /><br /> system_low_memory_signal_state = 0|使用可能な物理メモリが十分に存在します。|  
|system_high_memory_signal_state = 0<br /><br /> 、<br /><br /> system_low_memory_signal_state = 1|使用可能な物理メモリが不足しています。|  
|system_high_memory_signal_state = 0<br /><br /> 、<br /><br /> system_low_memory_signal_state = 0|物理メモリの使用量が安定しています。|  
|system_high_memory_signal_state = 1<br /><br /> 、<br /><br /> system_low_memory_signal_state = 1|物理メモリの状態が遷移します。<br /><br /> 高シグナルと低シグナルが同時にオンになることはありません。 ただし、オペレーティング システム レベルで変更を迅速には、両方の値をできるように、ユーザー モード アプリケーションに表示される可能性があります。 両方のシグナルがオンのように見えるとき、その状態は遷移中の状態と解釈されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


