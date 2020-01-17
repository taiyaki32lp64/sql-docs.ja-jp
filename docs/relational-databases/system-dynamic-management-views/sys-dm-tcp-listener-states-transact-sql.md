---
title: sys.dm_tcp_listener_states (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 396d2e1c2d0387e716123ce6f87ea5cef4ecbbe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090644"
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  各 TCP リスナーの動的状態情報を含む行を返します。  
  
> [!NOTE]
> 可用性グループ リスナーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのリスナーと同じポートでリッスンしている場合があります。 この場合、リスナーは個別に一覧表示、Service Broker リスナーの場合と同様です。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|リスナーの内部 id。 NULL 値は許可されません。<br /><br /> 主キー。|  
|**ip_address**|**nvarchar(48)**|オンラインであり、現在リッスンしているリスナーの IP アドレス。 IPv4 と IPv6 のどちらかを使用できます。 リスナーが両方の種類のアドレスを所有とは別に、一覧表示されます。 IPv4 のワイルドカードは、「0.0.0.0」として表示されます。 IPv6 のワイルドカードとして表示されます"::"です。<br /><br /> NULL 値は許可されません。|  
|**is_ipv4**|**bit**|IP アドレスの種類<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|リスナーがリッスンするポート番号。 NULL 値は許可されません。|  
|**type**|**tinyint**|リスナーの種類。次のいずれかになります。<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = データベース ミラーリング<br /><br /> NULL 値は許可されません。|  
|**type_desc**|**nvarchar(20)**|説明、**型**、1 つの。<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> NULL 値は許可されません。|  
|**state**|**tinyint**|可用性グループのリスナーの状態。次のいずれかになります。<br /><br /> 1 = オンラインです。 リスナーが要求のリスニングおよび処理中です。<br /><br /> 2 = 再起動の保留中。 リスナーはオフラインであり、再起動が保留されています。<br /><br /> 場合は、可用性グループ リスナーは、サーバー インスタンスと同じポートをリッスンしている、これら 2 つのリスナー常に同じ状態になっています。<br /><br /> NULL 値は許可されません。<br /><br /> 注:この列の値は、TSD_listener オブジェクトから取得します。 列は、状態を照会することはできません、TDS_listener がオフラインのときのため、オフラインの状態をサポートしません。|  
|**state_desc**|**nvarchar(16)**|説明**状態**、1 つの。<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> NULL 値は許可されません。|  
|**start_time**|**datetime**|リスナーが開始された日時を示すタイムスタンプ。 NULL 値は許可されません。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server のシステム カタログよく寄せられる質問のクエリを実行します。](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [AlwaysOn 可用性グループのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Always On 可用性グループの動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
