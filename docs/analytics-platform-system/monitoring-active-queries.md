---
title: アクティブなクエリの監視
description: 管理コンソールと並列データウェアハウスシステムビューを使用して、Analytics Platform System のアクティブなクエリを監視します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400910"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>アクティブなクエリの監視-並列データウェアハウス
この記事では、管理コンソールと SQL Server PDW システムビューを使用して、アクティブなクエリを監視する方法について説明します。 これらのツールの詳細については、「管理コンソールと[システムビュー](tsql-system-views.md) [を使用したアプライアンスの監視](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
アクティブなクエリの監視に使用する方法に関係なく、ログインには、[管理コンソールを使用するためのアクセス許可の付与](grant-permissions.md#grant-permissions-to-use-the-admin-console)に関するページに記載されているアクセス許可が必要です。  
  
## <a name="PermsAdminConsole"></a>アクティブなクエリの監視  
管理コンソールと SQL Server PDW システムビューの両方を使用して、アクティブなクエリを監視できます。 次の手順に従ってください。  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>管理コンソールを使用してアクティブなクエリを監視するには  
  
1.  管理コンソールにログオンします。 手順については[、「管理コンソールを使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。  
  
2.  上部のメニューで、[**クエリ**] をクリックします。 クエリを送信したログイン、クエリの開始時刻と終了時刻、クエリの現在の状態など、アプライアンスに関する最新のクエリに関する基本的な情報を含むテーブルが表示されます。  
  
3.  クエリコマンドを表示するには、その行の左側の列にあるクエリ ID の上にマウスポインターを置きます。  
  
    特定のクエリの詳細情報を表示するには、クエリ ID をクリックします。 クエリ実行の各ステップの状態情報と共に、完全なクエリとクエリプランを含む情報が表示されます。 エラーが返された場合は、エラーの詳細情報も確認できます。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>システムビューを使用してアクティブなクエリを監視するには  
クエリの監視に使用されるプライマリシステムビューは、 [dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)です。 このシステムビューを使用して`request_id` 、クエリテキストに基づいてアクティブまたは最近のクエリのを検索します。  
  
たとえば、次のクエリでは`request_id` 、 `status` `memberAddresses`テーブルからすべての列を選択するクエリのとの現在のが検索されます。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
`request_id`がクエリに対して識別された後、 `dm_pdw_exec_requests`テーブル内の他の情報を使用してクエリの処理を確認するか、または[dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)を使用してクエリ実行の個々のクエリステップの状態を表示します。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
