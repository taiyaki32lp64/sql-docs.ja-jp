---
title: 'SQL Server: Transactions オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Transactions
- Transactions object
ms.assetid: 85240267-78fd-476a-9ef6-010d6cf32dd8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c7dffaac161a61496c296ec99ec1f9ad2e1951a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182985"
---
# <a name="sql-server-transactions-object"></a>SQL Server: Transactions オブジェクト
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **Transactions** オブジェクトは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスでアクティブになっているトランザクションの数を監視するカウンターと、スナップショット分離による **tempdb**への行バージョン ストアなど、アクティブなトランザクションによるリソースへの影響を監視するためのカウンターを提供します。 トランザクションは、論理的な 1 つの作業単位です。つまり、一連の操作であり、すべて成功するか、データの論理的な整合性を維持するためにデータベースからすべて消去されるかのいずれかの結果になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内のデータへの変更は、すべてトランザクションで行われます。  
  
 スナップショット分離レベルを使用できるようにデータベースを設定している場合は、データベース内の各行に加えられた変更の記録を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で管理する必要があります。 行が変更されるたびに、変更前の状態の行のコピーが **tempdb**内の行バージョン ストアに記録されます。 **Transaction** オブジェクトの多くのカウンターは、 **tempdb**内の行バージョン ストアのサイズと増加率の監視に使用できます。  
  
 **Transactions** オブジェクトのカウンターは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の 1 つのインスタンス内のすべてのトランザクションを報告します。  
  
 次の表では、 **SQLServer:Transactions** のカウンターについて説明します。  
  
|SQL Server Transactions のカウンター|説明|  
|--------------------------------------|-----------------|  
|**Free Space in tempdb (KB)**|**tempdb**の使用可能な領域 (KB)。 スナップショット分離レベルのバージョン ストアと、この [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスで作成された新しいすべての一時オブジェクトの両方を保持するには、十分な空き領域が必要です。|  
|**Longest Transaction Running Time**|現在のトランザクションの中で最も長くアクティブになっているトランザクションが開始してから現在までの継続時間 (秒)。 このカウンターがアクティビティを示すのは、データベースが READ COMMITTED スナップショット分離レベルの場合のみです。 データベースが他の分離レベルの場合、アクティビティはログに記録されません。|  
|**NonSnapshot Version Transactions**|スナップショット分離レベルを使用していない現在アクティブなトランザクションのうち、データ変更を行ったトランザクションの数。データを変更すると、 **tempdb** のバージョン ストアに行バージョンが生成されます。|  
|**Snapshot Transactions**|スナップショット分離レベルを使用している現在アクティブなトランザクションの数。<br /><br /> 注:**Snapshot Transactions** オブジェクト カウンターは、`BEGIN TRANSACTION` ステートメントが発行されたときではなく、最初のデータ アクセスが行われたときに応答します。|  
|**トランザクション**|現在アクティブなトランザクションの数。すべての種類が含まれます。|  
|**Update conflict ratio**|この 1 秒間で更新の競合が発生した、スナップショット分離レベルを使用しているトランザクションの割合。 更新の競合が発生するのは、別のトランザクションによって最後に変更が行われ、スナップショット分離レベルのトランザクションの開始時にはコミットされていなかった行に対して、スナップショット分離レベルのトランザクションが変更を試行したときです。|  
|**Update Snapshot Transactions**|スナップショット分離レベルを使用し、データを変更した現在アクティブなトランザクションの数。|  
|**Version Cleanup rate (KB/s)**|**tempdb**のスナップショット分離のバージョン ストアから行バージョンが削除される比率 (KB/秒)。|  
|**Version Generation rate (KB/s)**|**tempdb**のスナップショット分離のバージョン ストアに新しい行バージョンが追加される比率 (KB/秒)。|  
|**Version Store Size (KB)**|スナップショット分離レベルの行バージョンを格納するために使用している、 **tempdb** 内の領域 (KB)。|  
|**Version Store unit count**|**tempdb**のスナップショット分離のバージョン ストアでアクティブになっているアロケーション ユニットの数。|  
|**Version Store unit creation**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの起動後に、スナップショット分離のバージョン ストアで作成されたアロケーション ユニットの数。|  
|**Version Store unit truncation**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの起動後に、スナップショット分離のバージョン ストアから削除されたアロケーション ユニットの数。|  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
