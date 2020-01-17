---
title: 可用性グループの正常性に対するグループ ポリシーの使用
description: Always On ダッシュ ボードで、可用性グループの正常性の情報の提供に使用される、グループ システム ポリシーを表示する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a48450322a8552720a119ea325ed720669fe5a8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245647"
---
# <a name="evaluate-health-of-the-always-on-availability-group-using-group-policies"></a>グループ ポリシーを使用した Always On 可用性グループの正常性の評価
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 可用性グループのシステム ポリシーは、ユーザーに可用性グループの正常性に関する情報を提供するために Always On ダッシュボードで使用されます。 それらは、可用性グループの運用上の問題の初期のトラブルシューティングに役立ちます。 これらのポリシーは、拡張して Always On ダッシュボードをカスタマイズするために使用したり、目的の正常性に関する情報をレポートするためにすぐに実行したりすることができます。  
  
 可用性グループに 14 のシステム ポリシーがあります。 各ポリシーの詳細については、「[AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md)」を参照してください。  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>可用性グループのシステム ポリシーの表示または評価  
 SQL Server Management Studio (SSMS) で可用性グループのシステム ポリシーを表示または実行するには、次の操作を行います。  
  
1.  **オブジェクト エクスプローラー**で、 **[管理]** 、 **[ポリシー管理]** 、 **[ポリシー]** 、 **[システム ポリシー]** の順に展開します。  
  
2.  ポリシーのいずれかを右クリックし、 **[評価]** をクリックします。 選択したポリシーを評価する場合は、これで終了です。 **[対象の詳細]** ボックスで、 **[表示]** をクリックして、評価の結果の詳細を表示することができます。  
  
3.  すべての可用性グループのシステム ポリシーを表示するには、 **[ページの選択]** ウィンドウで **[ポリシーの選択]** をクリックします。  
  
## <a name="next-steps"></a>次のステップ  
 [Always On の正常性モデル: パート 2:Extending the health model](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)」 (Always On 正常性モデル、パート 2: 正常性モデルの拡張) で提供している GUI のチュートリアルに類似しています。   
  
  
