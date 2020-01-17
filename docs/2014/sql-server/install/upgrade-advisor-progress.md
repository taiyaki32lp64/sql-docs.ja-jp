---
title: アップグレード アドバイザーの進行状況 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 697f70d4435213a991e55adecb51a98120d8df1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091560"
---
# <a name="upgrade-advisor-progress"></a>アップグレード アドバイザーの進行状況
  アップグレード アドバイザー分析では、選択した各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントの分析を実行する専用アナライザーから開始します。 進捗状況が報告されるようにコンポーネントが分析される、**進行状況** ダイアログ ボックス。  
  
## <a name="options"></a>および  
 **操作**  
 分析対象として選択された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントを指定します。  
  
 **ステータス**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントの進行状況インターフェイスから返された状態値が表示されます。  
  
 **メッセージ**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのアナライザーから返されたエラー、失敗、または成功のメッセージが表示されます。  
  
> [!NOTE]  
>  分析所要時間が非常に長い場合、その分析を停止してアップグレード アドバイザー分析ウィザードを終了してから、そのウィザードを再実行できます。 分析時間を短縮するには、スキャンするコンポーネントを少なくします。  
  
 分析が完了すると、そのレポートがファイルに書き込まれます。 クリックして、レポートを表示する**レポートの起動**をこのページからレポート ビューアを起動します。 後で、レポートを表示する場合は、開く、**アップグレード アドバイザー レポート ビューアー**アップグレード アドバイザーの開始ページから。  
  
> [!NOTE]  
>  以前のレポートはサーバーを分析するたびに保存されています。 保存されるレポートのファイル名には、タイムスタンプが使用されます。 レポート ビューアーでは、保存されている最近 5 件のレポートを表示できます。  
  
## <a name="see-also"></a>参照  
 [方法:アップグレード アドバイザーを起動します。](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [方法:アップグレード アドバイザー分析ウィザードを実行します。](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server コンポーネント](../../../2014/sql-server/install/sql-server-components.md)   
 [アップグレード アドバイザーのユーザー インターフェイス リファレンス](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
