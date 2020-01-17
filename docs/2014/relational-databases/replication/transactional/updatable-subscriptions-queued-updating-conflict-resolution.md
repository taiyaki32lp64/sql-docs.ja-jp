---
title: キュー更新の競合の検出と解決 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b43cdabb83b8f255b315e16b4bbe0d9af1156c51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655338"
---
# <a name="queued-updating-conflict-detection-and-resolution"></a>Queued Updating Conflict Detection and Resolution
  キュー更新サブスクリプションによって複数の場所にある同じデータを変更できるため、パブリッシャーでデータを同期するときに競合が起こる可能性があります。 レプリケーションによって、パブリッシャーとデータの変更を同期するときに競合を検出し、パブリケーションを作成したときに選択した解決方法でこれらの競合を解決します。 発生する可能性がある競合は、次のとおりです。  
  
-   更新および挿入競合。 この競合は、同一のデータが 2 つの異なる場所で変更された場合に発生します。 一方の変更が競合の優先データとなり、他方は非優先データとなります。  
  
-   削除競合。 この競合は、同一行が、ある箇所で削除され、別の箇所で変更された場合に発生します。  
  
 競合の検出と解決は、時間とリソースの消費が大きいプロセスであるため、複数のサブスクライバーがそれぞれ異なるデータのサブセットを変更できるようにデータ パーティションを作成して、アプリケーションの競合を最小限に抑えるようにします。  
  
## <a name="detecting-conflicts"></a>競合の検出  
 パブリケーションを作成してキュー更新を有効にすると、 **newid()** を既定値とする**uniqueidentifier**列 ( **msrepl_tran_version** ) が、レプリケーションによって作成元のテーブルに追加されます。 パブリッシュされたデータがパブリッシャーまたはサブスクライバーで変更されると、行は新しいグローバルな一意識別子 (GUID) を受け取り、新しい行が存在することを示します。 キュー リーダー エージェントは同期のとき、この列を使って競合の有無を確認します。  
  
 キューに登録されたトランザクションは、行の古い値と新しい値を保持しています。 トランザクションがパブリッシャーに適用されると、トランザクションの GUID とパブリケーションの GUID が比較されます。 トランザクションの古い GUID がパブリケーションの GUID と一致した場合は、パブリケーションは更新され、行にはサブスクライバーで作成された新しい GUID が割り当てられます。 トランザクションの GUID でパブリケーションを更新すると、パブリケーションとトランザクションの間で一致する行が得られます。  
  
 トランザクションの古い GUID がパブリケーションの GUID と一致しない場合は、競合が検出されます。 パブリケーションの新しい GUID は、異なる 2 つの行のバージョンが存在することを示します。1 つはサブスクライバーが送信するトランザクションの行で、もう 1 つはパブリッシャーの新しい行です。 この場合、このサブスクライバーのトランザクションを同期する前に、他のサブスクライバーまたはパブリッシャーがパブリケーション内の同一の行を更新しています。  
  
 マージ レプリケーションの場合とは違って、GUID 列を使用するのは行を識別するためでなく、行に変更があったかどうかを調べるためです。  
  
## <a name="resolving-conflicts"></a>競合の解決  
 キュー更新を使用してパブリケーションを作成するときは、競合が検出された場合に使用する競合回避モジュールを選択します。 競合回避モジュールでは、同期中に同じ行の複数のバージョンが検出された場合に、キュー リーダー エージェントで処理する方法を指定します。 パブリケーションにサブスクリプションがなければ、パブリケーションの作成後に競合解決方法を変更できます。 使用可能な競合解決方法は次のとおりです。  
  
-   パブリッシャー優先 (既定値)  
  
-   パブリッシャー優先およびサブスクリプション再初期化  
  
-   サブスクライバー優先  
  
 競合は記録され、競合表示モジュールによって表示可能です。  
  
 **キュー更新の競合解決方法を設定するには**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[キュー更新の競合解決オプションの設定 (SQL Server Management Studio)](../publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
-   レプリケーション Transact-SQL プログラミング: [トランザクション パブリケーションの更新可能なサブスクリプションの有効化](../publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **データの競合を表示するには**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]:[トランザクション パブリケーションのデータの競合の表示 &#40;SQL Server Management Studio&#41;](../view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>パブリッシャー優先  
 競合解決方法がパブリッシャー優先の場合は、トランザクションの一貫性はパブリッシャーのデータに基づいて維持されます。 競合を起こしたトランザクションは、それを開始したサブスクライバーにロールバックされます。  
  
 キュー リーダー エージェントが競合を検出すると、補正コマンドが生成されます。補正コマンドをディストリビューション データベースに通知することで、このコマンドはサブスクライバーへ反映されます。 その後、ディストリビューション エージェントは、競合状態のトランザクションを発信したサブスクライバーに補正コマンドを適用します。 補正アクションによって、パブリッシャーの行に一致するようにサブスクライバーの行が更新されます。  
  
 補正コマンドが適用されるまでは、サブスクライバーにロールバックされるトランザクションの結果を読み取ることができます。 この処理は、ダーティ リード ("READ UNCOMMITTED" 分離レベル) と同じです。 後で発生する従属トランザクションは補正されません。 ただし、トランザクション境界は受け入れられます。そして、トランザクション内のすべてのアクションがコミットされます。競合の場合はロールバックされます。  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>パブリッシャー優先およびサブスクリプション再初期化  
 競合を解決するためにサブスクライバーを再初期化すると、サブスクライバーのトランザクション一貫性が最も高くなります。ただし、パブリケーションのデータ量が多い場合、この再初期化には時間がかかります。  
  
 キュー リーダー エージェントが競合を検出すると、キューに登録された残りのトランザクション (競合状態のトランザクションも含む) は拒否され、サブスクライバーには再初期化のマークが付けられます。 パブリケーションに対して次に作成されるスナップショットは、ディストリビューション エージェントによってサブスクライバーに適用されます。  
  
### <a name="subscriber-wins"></a>サブスクライバー優先  
 サブスクライバー優先の方法による競合の検出は、パブリッシャー優先を更新した前回のサブスクライバー トランザクションを意味します。 この場合、競合が検出されても、サブスクライバーによって送信されたトランザクションは引き続き使用され、パブリッシャーが更新されます。 そのような変更によってもデータの整合性が失われない場合には、サブスクライバー優先の方法が適しています。  
  
## <a name="see-also"></a>参照  
 [Updatable Subscriptions for Transactional Replication](updatable-subscriptions-for-transactional-replication.md)  
  
  
