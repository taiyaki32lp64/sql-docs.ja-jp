---
title: 登録パッケージの拡張イベント ターゲットの表示 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae927a281db54697bbda49e28a58ea4c6e60326a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088727"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>登録パッケージの拡張イベント ターゲットの表示
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 拡張イベント セッションを作成する前に、提供されている拡張イベント ターゲットを確認すると役立つことがあります。 この作業では、以降に示した手順を実行するために [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用します。  
  
 この手順でステートメントの実行を完了すると、クエリ エディターの **[結果]** タブに次の 2 つの列が表示されます。  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>クエリ エディターを使用して登録パッケージの拡張イベント ターゲットを表示するには  
  
-   クエリ エディターで、次のステートメントを実行します。  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>参照  
 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
