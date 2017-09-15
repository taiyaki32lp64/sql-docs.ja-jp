---
title: "レッスン 3: マージ パブリケーションへのサブスクリプションの同期 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f80d0e6e39bea34899501368e7c7dfb693be1c6
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>レッスン 3:マージ パブリケーションへのサブスクリプションの同期
このレッスンでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でマージ エージェントを起動して、サブスクリプションを初期化します。 この手順を使用して、パブリッシャーと同期することもできます。 このレッスンを始める前に、前のレッスンの「 [レッスン 2: マージ パブリケーションへのサブスクリプションの作成](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)」を完了している必要があります。  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>同期を開始しサブスクリプションを初期化するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続し、サーバー ノードを展開して、 **[レプリケーション]** フォルダーを展開します。  
  
2.  **[ローカル サブスクリプション]** フォルダーで、 **SalesOrdersReplica** データベースのサブスクリプションを右クリックし、 **[同期の状態の表示]**をクリックします。  
  
3.  **[開始]** をクリックして、サブスクリプションを初期化します。  
  
## <a name="next-steps"></a>次の手順  
ここでは、マージ エージェントを実行し、同期の開始とサブスクリプションの初期化を行いました。 パブリッシャーまたはサブスクライバー側で、 **SalesOrderHeader** テーブルまたは **SalesOrderDetail** テーブルに対しデータの挿入、変更、削除を行い、ネットワーク接続が使用できるときにこの手順でパブリッシャーとサブスクライバーの間のデータを同期した後、もう一方のサーバーの **SalesOrderHeader** テーブルまたは **SalesOrderDetail** テーブルにクエリを実行すると、レプリケートされた変更を確認することができます。  
  
以上で、モバイル クライアントとの間のデータのレプリケーションに関するチュートリアルは完了です。 トランザクション レプリケーションを使用する類似のチュートリアルとして、「 [Tutorial: Replicating Data Between Continuously Connected Servers](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)」も参照してください。  
  
## <a name="see-also"></a>参照  
[スナップショットを使用したサブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[データベースの同期](../../relational-databases/replication/synchronize-data.md)  
[プル サブスクリプションの同期](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
