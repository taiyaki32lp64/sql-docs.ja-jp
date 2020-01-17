---
title: ミラー化されたデータベースの状態の確認 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5e61bd8ef63baa9a087bcae912b04f653f63b54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753884"
---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>ミラー化されたデータベースの状態の確認 (SQL Server Management Studio)
  データベース ミラーリング セッション中に、 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラーリング]** ページで状態を確認できます。  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>データベース ミラーリング セッションの状態を確認するには  
  
1.  プリンシパル サーバー インスタンスに接続した後、オブジェクト エクスプローラーでサーバー名をクリックして、サーバー ツリーを展開します。  
  
2.  **[データベース]** を展開し、ミラー化するデータベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** を選択し、 **[ミラー]** をクリックします。 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラーリング]** ページが開きます。  
  
4.  ミラー化開始後は、 **[ミラーリング]** ページを選択した時点または **[最新の情報に更新]** ボタンをクリックした時点のデータベース ミラーリング セッションの状態が **[状態]** パネルに表示されます。 表示される状態は次のとおりです。  
  
    |状態|説明|  
    |------------|-----------------|  
    |\<空白>|データベース ミラーリング セッションが存在せず、 **[ミラーリング]** ページに表示する動作情報がありません。|  
    |一時停止|プリンシパル データベースは実行中ですが、ミラー サーバーにログを送信していません。 データベースのミラー コピーは使用できない状態です。|  
    |[接続なし]|プリンシパル サーバー インスタンスから、パートナーまたはミラーリング監視サーバー インスタンス (ある場合) に接続できません。|  
    |[同期中]|ミラー データベースの内容が、プリンシパル データベースの内容に遅れています。 プリンシパル サーバー インスタンスからミラー サーバー インスタンスにログ レコードを送信して、ミラー データベースを更新するための変更を適用しています。<br /><br /> データベース ミラーリング セッションの開始時点では、ミラー データベースとプリンシパル データベースが同期中の状態です。|  
    |[フェールオーバー]|プリンシパル サーバー インスタンスで手動フェールオーバー (役割の交代) を開始しましたが、まだミラーが受け入れていません。|  
    |同期済み|ミラー データベースとプリンシパル データベースには、同一のデータが含まれています。 同期完了の状態のとき *だけ* 、手動および自動フェールオーバーを実行できます。|  
  
## <a name="see-also"></a>参照  
 [ミラーリング状態 &#40;SQL Server&#41;](mirroring-states-sql-server.md)  
  
  
