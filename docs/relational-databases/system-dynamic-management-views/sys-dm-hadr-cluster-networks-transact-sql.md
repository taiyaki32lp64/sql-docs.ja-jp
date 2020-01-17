---
title: sys.dm_hadr_cluster_networks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_cluster_networks
- sys.dm_hadr_cluster_networks_TSQL
- sys.dm_hadr_cluster_networks
- dm_hadr_cluster_networks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_networks dynamic management view
ms.assetid: ece32b15-d63f-4f93-92b7-e2930333e97a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0b2475a3881cb73d9dd82ee7fc311e7288aa4738
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67900648"
---
# <a name="sysdmhadrclusternetworks-transact-sql"></a>sys.dm_hadr_cluster_networks (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  可用性グループのサブネット構成に参加している WSFC クラスター メンバーごとに 1 行のデータを返します。 この動的管理ビューを使用して、可用性レプリカごとに構成されているネットワーク仮想 IP を検証できます。  
  
 主キー: **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > 以降で[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、この動的管理ビューは、Always On フェールオーバー クラスター インスタンスだけでなく Always On 可用性グループをサポートしています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|WSFC クラスター内のノードのコンピューター名。|  
|**network_subnet_ip**|**nvarchar(48)**|コンピューターが属するサブネットのネットワーク IP アドレス。 IPv4 または IPv6 アドレスを指定できます。|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|IP アドレスが属するサブネットを指定するネットワーク サブネット マスクです。 **network_subnet_ipv4_mask**の WITH DHCP 句で DHCP < network_subnet_option > オプションを指定する、 [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md)または[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。<br /><br /> NULL = IPv6 サブネット。|  
||||  
|**network_subnet_prefix_length**|**int**|コンピューターが属するサブネットを指定するネットワーク IP プレフィックス長。|  
|**is_public**|**bit**|かどうか、ネットワークは、プライベートまたはパブリックのいずれかの WSFC クラスターには。<br /><br /> 0 = プライベート<br /><br /> 1 = パブリック|  
|**is_ipv4**|**bit**|サブネットの種類。次のいずれかになります。<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [フェールオーバー クラスタリングと Always On 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
