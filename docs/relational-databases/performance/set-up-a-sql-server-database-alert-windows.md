---
title: SQL Server データベースの警告のセットアップ (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f76c6f4f4d65273c35dffb1cb17e664fceac0328
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113344"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>SQL Server データベースの警告のセットアップ (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  システム モニターでは、システム モニターのカウンターがしきい値に達したときに発生する警告を作成できます。 システム モニターは、この警告に応答して、警告状況を処理するために記述されたカスタム アプリケーションなどのアプリケーションを起動できます。 たとえば、デッドロックの数が特定の値を超えたときに生成される警告を作成できます。 
  
 警告は、Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して定義することもできます。 詳細については、「 [警告](../../ssms/agent/alerts.md)」を参照してください。  
  
## <a name="set-up-a-sql-server-database-alert"></a>SQL Server データベースの警告をセットアップする  
  
1. **[パフォーマンス]** ウィンドウのナビゲーション ツリーで、 **[パフォーマンス ログと警告]** を展開します。  
  
2. **[警告]** を右クリックし、 **[新しい警告の設定]** を選択します。
  
3. **[新しい警告の設定]** ダイアログ ボックスで、新しい警告の名前を入力し、 **[OK]** を選択します。  
  
4. 新しい警告のダイアログ ボックスの **[全般]** タブで、 **[コメント]** を追加します。 **[追加]** を選択して警告にカウンターを追加します。  
  
     各警告には、少なくとも 1 つのカウンターを含む必要があります。  
  
5. **[カウンターの追加]** ダイアログ ボックスで、 **[パフォーマンス オブジェクト]** 一覧から SQL Server オブジェクトを選択します。 **[一覧からカウンターを選択]** でカウンターを選択します。  
  
6. 警告にカウンターを追加するには、 **[追加]** を選択します。 カウンターの追加を続行するか、 **[閉じる]** を選択して新しい警告のダイアログ ボックスに戻ることができます。  
  
7. 新しい警告のダイアログ ボックスで、 **[次の値になったら警告する]** の一覧の **[超過]** または **[以下]** を選択します。 **[制限値]** にしきい値を入力します。  
  
     警告は、カウンターの値がしきい値を超えたとき、またはしきい値以下になったときに生成されます。これは **[超過]** または **[以下]** のどちらを選択したかによって決まります。  
  
8. **[Sample data every (データのサンプル間隔)]** ボックスで、サンプリング周期を設定します。  
  
9. **[アクション]** タブで、警告がトリガーされたときに実行される操作を設定します。  
  
10. **[スケジュール]** タブで、警告スキャンの開始と停止のスケジュールを設定します。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベース警告の作成](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
