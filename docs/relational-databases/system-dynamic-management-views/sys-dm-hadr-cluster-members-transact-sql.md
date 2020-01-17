---
title: sys.dm_hadr_cluster_members (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b28b708aabfdf3ec4e569aab6d8a95e2330b370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900763"
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  かどうか、ホストする WSFC ノードのローカル インスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を有効になっている[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]に WSFC クォーラムがある、各クォーラムとそれぞれの状態を構成するメンバーの行を返します。 これには、クラスター内のすべてのノードの含まれています (によって CLUSTER_ENUM_NODE 型で返されます、 **Clusterenum**関数) と、ディスク監視やファイル共有監視、存在する場合。 特定のメンバーに対して返される行には、そのメンバーの状態に関する情報が含まれています。 たとえば、1 つのノードがダウンしている場合のマジョリティ ノードのクォーラムを 5 つのノード クラスター **sys.dm_hadr_cluster_members**が有効になっているサーバー インスタンスに照会[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]クォーラムを持つノード上に存在します。**sys.dm_hadr_cluster_members** "node_down"停止したノードの状態を反映します。  
  
 WSFC ノードにクォーラムが存在しない場合、行は返されません。  
  
 次の質問に回答するのにには、この動的管理ビューを使用します。  
  
-   ノードの内容は、WSFC クラスターで実行されているか。  
  
-   マジョリティ ノードのクォーラムが失われるまでに、WSFC クラスターがあと何回の障害に耐えられるか。  

 > [!TIP]
 > 以降で[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、この動的管理ビューは、Always On フェールオーバー クラスター インスタンスだけでなく Always On 可用性グループをサポートしています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|メンバー名。コンピューター名、ドライブ文字、ファイル共有パスのいずれかになります。|  
|**member_type**|**tinyint**|メンバーの種類。次のいずれかになります。<br /><br /> 0 = WSFC ノード<br /><br /> 1 = ディスク監視<br /><br /> 2 = ファイル共有監視<br /><br /> 3 = クラウド ミラーリング監視サーバー|  
|**member_type_desc**|**nvarchar (50)**|説明**member_type**、1 つの。<br /><br /> クラスタ<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|いずれかのメンバーの状態:<br /><br /> 0 = オフライン<br /><br /> 1 = オンライン|  
|**member_state_desc**|**nvarchar(60)**|説明**member_state**、1 つの。<br /><br /> UP<br /><br /> ダウン|  
|**number_of_quorum_votes**|**tinyint**|このクォーラム メンバーが保有するクォーラムの投票数。 マジョリティなし。0 にディスクのみクォーラムでは、この値が既定値です。 その他のクォーラムの種類の場合、この値は既定で 1 になります。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
