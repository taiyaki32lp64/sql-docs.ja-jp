---
title: アプライアンスの警告の追跡
description: Analytics Platform System でアプライアンスのアラートを追跡します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399940"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Analytics Platform System でアプライアンスアラートを追跡する
このトピックでは、管理コンソールとシステムビューを使用して、SQL Server PDW アプライアンスのアラートを追跡する方法について説明します。  
  
## <a name="to-track-appliance-alerts"></a>アプライアンスのアラートを追跡するには  
SQL Server PDW は、注意が必要なハードウェアおよびソフトウェアの問題に関するアラートを作成します。 各アラートには、問題のタイトルと説明が含まれています。  
  
SQL Server PDW は、 [sys. dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV で警告をログに記録します。 システムでは、1万のアラートの上限が保持され、上限を超えた場合に最も古いアラートが最初に削除されます。  
  
### <a name="view-alerts-by-using-the-admin-console"></a>管理コンソールを使用してアラートを表示する  
PDW 領域の [**アラート**] タブとアプライアンスのファブリックリージョンがあります。 フェールオーバーが発生した後、フェールオーバーイベントはページ上のアラートの数に含まれます。 PDW リージョン用のページとアプライアンスのファブリックリージョン用のページがあります。 各正常性ページにはタブがあります。アラートの詳細を確認するには、[**正常性**] ページの [**アラート**] タブをクリックし、アラートをクリックします。  
  
![PDW 管理コンソールの警告](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
[**アラート**] ページで、次のようにします。  
  
-   アラートの履歴を表示するには、[**アラート履歴の確認**] リンクをクリックします。  
  
-   警告コンポーネントとその現在のプロパティ値を表示するには、[アラート] 行をクリックします。  
  
-   アラートを発生させたノードの詳細を表示するには、ノード名をクリックします。  
  
### <a name="view-alerts-by-using-the-system-views"></a>システムビューを使用したアラートの表示  
システムビューを使用して警告を表示するには、 [dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)クエリを実行します。 この DMV には、修正されていないアラートが表示されます。 アラートとエラーのトリアージに関するヘルプを表示するには、 [dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV を使用します。  
  
次の例は、現在のアラートを表示するための一般的なクエリです。  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[アプライアンス監視 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
