---
title: 登録パッケージのイベントの表示 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing events
- extended events [SQL Server], viewing events
ms.assetid: 9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1156a7272edc8ad1ecfb8e173f81bc678800c855
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089629"
---
# <a name="view-the-events-for-registered-packages"></a>登録パッケージのイベントの表示
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 拡張イベント セッションを作成する前に、登録パッケージで提供されているイベントを確認すると役立つことがあります。 詳細については、「 [SQL Server 拡張イベント パッケージ](../relational-databases/extended-events/sql-server-extended-events-packages.md)」を参照してください。  
  
 この作業には、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用した次の手順の実行も含まれます。  
  
 この手順でステートメントの実行が完了すると、クエリ エディターの **[結果]** タブに次の列が表示されます。  
  
-   name: パッケージの名前です。  
  
-   event: イベント名。  
  
-   keyword: 内部数値マッピング テーブルから派生されたキーワードです。  
  
-   channel: イベントの対象ユーザーです。  
  
-   description: イベントの説明です。  
  
## <a name="to-view-the-events-for-registered-packages-using-query-editor"></a>クエリ エディターを使用して登録パッケージのイベントを表示するには  
  
-   クエリ エディターで、次のステートメントを実行します。  
  
    ```  
    USE msdb  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
    (  
    SELECT event_package=o.package_guid, o.description,   
    event=c.object_name, channel=v.map_value  
    FROM sys.dm_xe_objects o  
    LEFT JOIN sys.dm_xe_object_columns c ON o.name=c.object_name  
    INNER JOIN sys.dm_xe_map_values v ON c.type_name=v.name   
    AND c.column_value=cast(v.map_key AS nvarchar)  
    WHERE object_type='event' AND (c.name='CHANNEL' or c.name IS NULL)  
  
    ) c LEFT JOIN   
    (  
    SELECT event_package=c.object_package_guid, event=c.object_name,   
    keyword=v.map_value  
    FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
    ON c.type_name=v.name AND c.column_value=v.map_key   
    AND c.type_package_guid=v.object_package_guid  
    INNER JOIN sys.dm_xe_objects o ON o.name=c.object_name   
    AND o.package_guid=c.object_package_guid  
    WHERE object_type='event' AND c.name='KEYWORD'   
    ) k  
    ON  
    k.event_package=c.event_package AND (k.event=c.event or k.event IS NULL)  
    INNER JOIN sys.dm_xe_packages p ON p.guid=c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
## <a name="see-also"></a>参照  
 [SQL Server 拡張イベント パッケージ](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
