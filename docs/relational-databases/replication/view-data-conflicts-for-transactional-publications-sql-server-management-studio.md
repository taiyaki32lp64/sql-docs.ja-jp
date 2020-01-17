---
title: データの競合の表示 (トランザクション) - SSMS
description: SQL Server Management Studio (SSMS) を使用して、トランザクション レプリケーションのデータの競合を表示します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9b385de9eee9fd1073c2161d0db57fd0287f959c
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321869"
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>トランザクション パブリケーションのデータの競合の表示 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ピア ツー ピア トランザクション レプリケーション、およびキュー更新サブスクリプションを使用するトランザクション レプリケーションでの競合を、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] レプリケーション競合表示モジュールで表示できます。 競合の検出と解決方法については、「[ピア ツー ピア レプリケーションにおける競合検出](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」と「[キュー更新の競合解決オプションの設定 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)」をご覧ください。  
  
 競合データを表示できるかどうかは、レプリケーションの種類および競合の保有期間によって異なります。  
  
-   ピア ツー ピア レプリケーションの場合、ディストリビューション エージェントは、競合を検出すると既定で停止します。 競合エラーはエラー ログに記録されますが、競合データは競合テーブルに記録されないため、競合データを表示できません。 ディストリビューション エージェントが実行の継続を許可されている場合は、競合が検出された各ノードで、競合がローカルでログに記録されます。 詳細については、「 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」の「競合の処理」を参照してください。  
  
-   キュー更新サブスクリプションの場合は、すべての競合のデータを表示できます。 競合データは、競合の保有期間に指定した期間 (既定では 14 日間)、レプリケーション競合表示モジュールで表示できます。 競合の保有期間を設定するには、次のいずれかを実行します。  
  
    -   [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) の @conflict_retention パラメーターに保有期間の値を指定します。  
  
    -   [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) の @property パラメーターに **'conflict_retention'** を指定し、@value パラメーターに保有期間の値を指定します。  
  
### <a name="to-view-conflicts"></a>競合を表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で適切なサーバーに接続し、そのサーバー ノードを展開します。  
  
    -   ピア ツー ピア レプリケーションの場合は、競合の発生したノードがこれに当たります。  
  
    -   キュー更新サブスクリプションの場合は、パブリッシャーがこれに当たります。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  競合を表示するパブリケーションを右クリックしてから、 **[競合の表示]** をクリックします。  
  
4.  **[競合テーブルの選択]** ダイアログ ボックスで、競合を表示するデータベース、パブリケーション、およびテーブルを選択します。  
  
5.  レプリケーション競合表示モジュールでは、以下を実行できます。  
  
    -   上のグリッドの右側のボタンで行をフィルター選択する。  
  
    -   上のグリッドで行を選択して、下のグリッドにその行の情報を表示する。  
  
    -   上のグリッドで複数の行を選択し、 **[削除]** をクリックして、競合メタデータ テーブルから行を削除する。  
  
    -   プロパティ ボタン ( **[...]** ) をクリックし、競合に関係のある列の詳細情報を表示する。  
  
    -   **[この競合の詳細をログに記録する]** を選択して、競合のデータをログ ファイルに記録する。 ファイルの場所を指定するには、 **[表示]** メニューをポイントし、 **[オプション]** をクリックします。 値を入力するか、または参照ボタン ( **[...]** ) をクリックして適切なファイルに移動します。 **[OK]** をクリックして、 **[オプション]** ダイアログ ボックスを閉じます。  
  
6.  レプリケーション競合表示モジュールを閉じます。  
  
## <a name="see-also"></a>参照  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
