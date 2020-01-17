---
title: データベース スナップショットと AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cba02aa87e800391ffba3c791c1ee4341462c3f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814658"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>AlwaysOn 可用性グループを含むデータベース スナップショット (SQL Server)
  データベース スナップショットは、可用性グループ内のプライマリ データベースまたはセカンダリ データベースに作成できます。 レプリカのロールは "プライマリ" または "セカンダリ" とし、"解決中" 状態でないことが必要です。  
  
 データベース スナップショットの作成は、データベースの同期状態が "同期中" または "同期済み" であるときに実行することをお勧めします。 ただし、データベースの同期状態が "同期されていません" であっても、データベース スナップショットを作成することはできます。  
  
 セカンダリ レプリカがプライマリ レプリカから切断された (DISCONNECTED 状態) 場合、セカンダリ レプリカ上のデータベース スナップショットは引き続き実行できます。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の一部の条件が原因で、ソース データベースとそのデータベース スナップショットが再起動され、一時的にユーザーの接続が切断されます。 このような条件は次のとおりです。  
  
-   同じサーバー インスタンスで現在のプライマリ レプリカがオフラインになり、オンラインに戻ったため、または可用性グループのフェールオーバーが発生したため、プライマリ レプリカでロールが変更される場合  
  
-   データベースがセカンダリ ロールに移行する場合  
  
 データベース スナップショットをホストする可用性レプリカがフェールオーバーされると、データベース スナップショットは、そのデータベース スナップショットが作成されたサーバー インスタンス上に残ります。 ユーザーは、フェールオーバーの発生後、このスナップショットを引き続き使用できます。パフォーマンスを重視する環境の場合は、手動フェールオーバー モード用に構成するセカンダリ レプリカによってホストされるセカンダリ データベース上にのみデータベース スナップショットを作成することをお勧めします。  このセカンダリ レプリカに可用性グループを手動でフェールオーバーすると、データベース スナップショットの新しいセットを別のセカンダリ レプリカ上に作成し、クライアントを新しいデータベース スナップショットに再出力して、プライマリ データベースからすべてのデータベース スナップショットを削除できます。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Database Snapshots &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
