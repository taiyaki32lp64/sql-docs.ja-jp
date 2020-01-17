---
title: すべてのイベントのフィールドを取得 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0838367ad699c1278bb6ec42f28161ba76c6fd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064789"
---
# <a name="get-the-fields-for-all-events"></a>すべてのイベントのフィールドを取得する
  この作業には、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディターを使用した次の手順の実行も含まれます。  
  
 この手順でステートメントの実行が完了すると、クエリ エディターの **[結果]** タブに次の列が表示されます。  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 バケット ターゲットを使用するイベント セッションを設定する場合は、上記の情報を使用できます。 詳細については、「 [SQL Server 拡張イベント ターゲット](../../2014/database-engine/sql-server-extended-events-targets.md)」を参照してください。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 拡張イベント セッションを作成する前に、イベントに関連したフィールドについての情報を取得すると役立つことがあります。  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>クエリ エディターを使用してすべてのイベントのフィールドを取得するには  
  
-   クエリ エディターで、次のステートメントを実行します。  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>参照  
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
