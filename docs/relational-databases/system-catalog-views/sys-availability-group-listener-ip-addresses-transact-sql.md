---
title: sys.availability_group_listener_ip_addresses (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- availability_group_listener_ip_addresses
- sys.availability_group_listener_ip_addresses
- availability_group_listener_ip_addresses_TSQL
- sys.availability_group_listener_ip_addresses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.availability_group_listener_ip_addresses catalog view
ms.assetid: e515fa6b-1354-4110-9b70-ab2e6164c992
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9c66e12ec326ba5021de0829b0d7cc479f858c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997587"
---
# <a name="sysavailabilitygrouplisteneripaddresses-transact-sql"></a>sys.availability_group_listener_ip_addresses (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Windows Server フェールオーバー クラスタリング (WSFC) クラスター内の任意の AlwaysOn 可用性グループ リスナーに関連付けられている IP アドレスごとに 1 行のデータを返します。  
  
 主キー: **listener_id** + **ip_address** + **ip_sub_mask**  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**listener_id**|**nvarchar(36)**|Windows Server フェールオーバー クラスタ リング (WSFC) クラスターからのリソース GUID。|  
|**ip_address**|**nvarchar(48)**|可用性グループ リスナーの構成された仮想 IP アドレス。 1 つの IPv4 または IPv6 アドレスを返します。|  
|**ip_subnet_mask**|**nvarchar(15)**|可用性グループ リスナーに対して構成されている IPv4 アドレスの構成された IP サブネット マスク (存在する場合)。<br /><br /> NULL = IPv6 サブネット|  
|**is_dhcp**|**bit**|かどうかのいずれか、DHCP によって IP アドレスが構成されています。<br /><br /> 0 = IP アドレスは DHCP によって構成されていません。<br /><br /> 1 = IP アドレスが DHCP によって構成されています。|  
|**network_subnet_ip**|**nvarchar(48)**|IP アドレスが属するサブネットを指定するネットワークのサブネット IP アドレス。|  
|**network_subnet_prefix_length**|**int**|IP アドレスが属するサブネットのネットワーク サブネット プレフィックス長。|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|IP アドレスが属するサブネットのネットワークのサブネット マスクです。 **network_subnet_ipv4_mask**の WITH DHCP 句で DHCP < network_subnet_option > オプションを指定する、 [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md)または[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント。<br /><br /> NULL = IPv6 サブネット|  
|**state**|**tinyint**|WSFC のクラスターからの IP リソースのオンラインまたはオフライン状態。次のいずれかになります。<br /><br /> 1 = オンラインです。 IP リソースはオンラインです。<br /><br /> 0 = オフライン。 IP リソースはオフラインです。<br /><br /> 2 = オンライン待ち。 IP リソースはオフラインになってがオンラインになっています。<br /><br /> 3 = 失敗します。 IP リソースはでしたが、失敗しましたオンラインされています。|  
|**state_desc**|**nvarchar(60)**|説明**状態**、1 つの。<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> ONLINE_PENDING<br /><br /> FAILED|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
