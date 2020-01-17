---
title: sys.availability_group_listeners (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listeners_TSQL
- sys.availability_group_listeners
- sys.availability_group_listeners_TSQL
- availability_group_listeners
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_group_listeners catalog view
- Availability Groups [SQL Server], listeners
ms.assetid: b5e7d1fb-3ffb-4767-8135-604c575016b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b363e410f35eb7880933520dd1dbf47f258b651e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041061"
---
# <a name="sysavailabilitygrouplisteners-transact-sql"></a>sys.availability_group_listeners (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  各 AlwaysOn 可用性グループについて、可用性グループにネットワーク名が関連付けられていないことを示すゼロ行を返すか、Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の可用性グループ リスナーの構成ごとに 1 行のデータを返します。 このビューには、クラスターから収集したリアルタイムの構成が表示されます。  
  
> [!NOTE]  
>  このカタログ ビューでは、WSFC クラスターで定義された IP 構成の詳細は表示されません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|可用性グループ ID (**group_id**) から[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)します。|  
|**listener_id**|**nvarchar(36)**|クラスター リソース ID の GUID|  
|**dns_name**|**nvarchar(63)**|可用性グループ リスナーの構成されたネットワーク名 (ホスト名)。|  
|**port**|**int**|可用性グループ リスナーに対して構成された TCP ポート番号。<br /><br /> NULL = リスナーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部で構成され、そのポート番号が可用性グループに追加されていません。 ポート、pleaseuse の MODIFY LISTENER オプションを追加する、 [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。|  
|**is_conformant**|**bit**|この IP 構成がかどうかに準拠するのいずれかです。<br /><br /> 1 = リスナーは準拠。 唯一の"OR"リレーションは、そのインターネット プロトコル (IP) アドレスの間に存在します。 *準拠する*はすべてによって作成された IP 構成、 [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。 また場合の外部で作成された IP 構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]などで、WSFC フェールオーバー クラスター マネージャーを使用して、変更することができます、ALTER AVAILABILITY GROUP tsql ステートメントでは、準拠と見なされる IP 構成。<br /><br /> 0 = リスナーは準拠していません。 通常、IP アドレスを使用して構成できませんでしたがこれを示します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コマンドし、代わりに、WSFC クラスターで直接定義されました。|  
|**ip_configuration_string_from_cluster**|**nvarchar(max)**|このリスナーの存在する場合は、クラスターの IP 構成文字列を実行します。 NULL = リスナーには仮想 IP アドレスがありません。 以下に例を示します。<br /><br /> IPv4 アドレス: `65.55.39.10`<br /><br /> IPv6 アドレス: `2001::4898:23:1002:20f:1fff:feff:b3a3`|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
