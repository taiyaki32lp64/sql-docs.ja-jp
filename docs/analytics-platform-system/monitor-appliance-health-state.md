---
title: アプライアンスの正常性の監視
description: 管理コンソールを使用して Analytics Platform System アプライアンスの状態を監視する方法、または並列データウェアハウスの動的管理ビューに直接クエリを実行する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400994"
---
# <a name="monitor-appliance-health-state"></a>アプライアンスの正常性状態の監視
この記事では、管理コンソールを使用して Analytics Platform System アプライアンスの状態を監視する方法、または並列データウェアハウスの動的管理ビューに直接クエリを実行する方法について説明します。 
  
## <a name="to-monitor-the-appliance-state"></a>アプライアンスの状態を監視するには  
システム管理者は、管理コンソールまたは SQL Server PDW 動的管理ビュー (Dmv) を使用して、ノード、コンポーネント、およびソフトウェアの完全階層を取得できます。 次の図は、SQL Server PDW 監視するコンポーネントの概要を示しています。  
  
![監視の概要](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>管理コンソールを使用してコンポーネントのステータスを監視する  
管理コンソールを使用してコンポーネントのステータスを取得するには:  
  
1.  [アプライアンスの**状態**] タブをクリックします。  
  
2.  [アプライアンスの状態] ページで、特定のノードをクリックすると、ノードの詳細が表示されます。  
  
    ![PDW 管理コンソールの状態](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>システムビューを使用したコンポーネントのステータスの監視  
システムビューを使用してコンポーネントのステータスを取得するには、 [dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)を使用します。 たとえば、次のクエリでは、すべてのコンポーネントの状態が取得されます。  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
Status プロパティに返される値は次のとおりです。  
  
-   [OK]  
  
-   ほど  
  
-   Critical  
  
-   Unknown の中から 1 つ以上を指定します  
  
-   サポートされていません  
  
-   アクセス不可  
  
-   回復不能  
  
すべてのコンポーネントのすべてのプロパティを表示するに`WHERE  p.property_name = 'Status'`は、句を削除します。  
  
**[Update_time]** 列には、コンポーネントが SQL Server PDW 正常性エージェントによって最後にポーリングされた時刻が表示されます。  
  
> [!CAUTION]  
> コンポーネントが5分以上ポーリングされていない場合は、問題を調査してください。ソフトウェアのハートビートの問題を示すアラートが表示される場合があります。  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[アプライアンス監視 &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
