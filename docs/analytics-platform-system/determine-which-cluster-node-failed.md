---
title: 失敗したクラスターノードを特定する
description: この記事では、クラスターのフェールオーバーが発生し、クラスターのフェールオーバーアラートが発生した後に失敗した Analytics Platform System (APS) ノードの名前を確認する方法について説明します。 クラスターのフェールオーバーのトラブルシューティングの一環として、Microsoft に連絡して問題の解決に役立てるために、失敗したノードの名前を特定する必要があります。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401207"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>分析プラットフォームシステムで失敗したクラスターノードを特定する
このトピックでは、クラスターのフェールオーバーが発生し、クラスターのフェールオーバーアラートが発生した後に失敗した Analytics Platform System (APS) ノードの名前を確認する方法について説明します。 クラスターのフェールオーバーのトラブルシューティングの一環として、Microsoft に連絡して問題の解決に役立てるために、失敗したノードの名前を特定する必要があります。  
  
## <a name="Background"></a>基本  
SQL Server PDW の高可用性を実現するために、制御ノードとコンピューティングノードは、Windows フェールオーバークラスターのアクティブまたはパッシブコンポーネントとして構成されています。 アクティブなサーバーが重要なシステム要求に応答できない場合、パッシブサーバーはフェールオーバーし、失敗したサーバーの機能を実行します。  
  
クラスターのフェールオーバー後、ノードの状態に関するレポートを SQL Server PDW と、パッシブサーバーの状態が [フェールオーバー] になります。 ただし、障害が発生したサーバーがまだオンラインになっている場合は、どのサーバーまたはノードで障害が発生したかはっきりしません。 クラスターの障害のトラブルシューティングを行うには、フェールオーバーしたノードの名前を確認する必要があります。  
  
## <a name="AdminConsoleSolution"></a>管理コンソールソリューション  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>失敗したノードの名前を検索するには  
  
1.  管理コンソールを開きます。 管理コンソールの詳細については、「[管理コンソール &#40;Analytics Platform System&#41;を使用したアプライアンスの監視](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。 フェールオーバーが発生した後、フェールオーバーイベントは [**正常性**] ページのアラートの数に含まれます。 PDW リージョンおよびアプライアンスのファブリックリージョンの**正常性**ページがあります。 各正常性ページには [**アラート**] タブがあります。アラートの詳細を確認するには、[正常性] ページの [アラート] タブをクリックし、アラートをクリックします。  
  
## <a name="SystemView"></a>システムビューソリューション  
次の SQL ステートメントは、 [dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)システムビューを使用して、失敗したサーバーの名前を検索する方法を示しています。  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
