---
title: SQL Server データベースの警告のセットアップ (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3342af1de84e922ce63848c8fdffe5aa30ec309a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150497"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>SQL Server データベースの警告のセットアップ (Windows)
  システム モニターを使用すると、システム モニター カウンターがしきい値に到達した場合に生成される警告を作成できます。 システム モニターは、この警告に応答して、警告状況を処理するために記述されたカスタム アプリケーションなどのアプリケーションを起動できます。 たとえば、デッドロックの数が特定の値を超えたときに生成される警告を作成できます。  
  
 警告は、Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して定義することもできます。 詳細については、「 [警告](../../ssms/agent/alerts.md)」をご覧ください。  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>SQL Server データベースの警告をセットアップするには  
  
1.  [パフォーマンス] ウィンドウのナビゲーション ツリーで、 **[パフォーマンス ログと警告]** を展開します。  
  
2.  **[警告]** を右クリックし、 **[新しい警告の設定]** をクリックします。  
  
3.  **[新しい警告の設定]** ダイアログ ボックスで、新しい警告の名前を入力し、 **[OK]** をクリックします。  
  
4.  新しい警告のダイアログ ボックスの **[全般]** タブで、 **[コメント]** を追加し、 **[追加]** をクリックして警告にカウンターを追加します。  
  
     各警告には、少なくとも 1 つのカウンターを含む必要があります。  
  
5.  [カウンターの追加] ダイアログ ボックスで、 **[パフォーマンス オブジェクト]** の一覧から SQL Server オブジェクトを選択し、 **[一覧からカウンターを選ぶ]** からカウンターを選択します。  
  
6.  警告にカウンターを追加するには、 **[追加]** をクリックします。 カウンターの追加を続行するか、 **[閉じる]** をクリックして新しい警告のダイアログ ボックスに戻ることができます。  
  
7.  新しい警告のダイアログ ボックスで、 **[Alert when the value is (次の値になったら警告する)]** の一覧の **[Over (超過)]** または **[Under (以下)]** をクリックし、 **[Limit (制限値)]** にしきい値を入力します。  
  
     警告は、カウンターの値がしきい値を超えたとき、またはしきい値以下になったときに生成されます。これは **[Over (超過)]** または **[Under (以下)]** のどちらをクリックしたかによって決まります。  
  
8.  **[Sample data every (データのサンプル間隔)]** ボックスで、サンプリング周期を設定します。  
  
9. **[アクション]** タブで、警告がトリガーされたときに実行される操作を設定します。  
  
10. **[スケジュール]** タブで、警告スキャンの開始と停止のスケジュールを設定します。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベース警告の作成](../performance-monitor/create-a-sql-server-database-alert.md)  
  
  
