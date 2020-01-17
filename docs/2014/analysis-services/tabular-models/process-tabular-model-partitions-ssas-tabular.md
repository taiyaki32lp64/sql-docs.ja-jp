---
title: テーブル モデル パーティション (SSAS テーブル) の処理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4cabfe4f0d28bb74ae1fae0b84de758e7dca565
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066832"
---
# <a name="process-tabular-model-partitions-ssas-tabular"></a>テーブル モデル パーティションの処理 (SSAS テーブル)
  パーティションは、テーブルを論理的な部分に分割します。 各パーティションは、他のパーティションとは個別に処理 (更新) できます。 このトピックのタスクでは、 **で** [パーティションの処理] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ダイアログ ボックスを使用して、モデル データベースでパーティションを処理する方法について説明します。  
  
###  <a name="bkmk_create_new"></a> パーティションを処理するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、処理対象のパーティションが存在するテーブルを右クリックして **[パーティション]** をクリックします。  
  
2.  **[パーティション]** ダイアログ ボックスの **[パーティション]** で、[処理] ボタンをクリックします。  
  
3.  **パーティションの処理**  ダイアログ ボックスで、**モード**ボックスの一覧で、次のプロセス モードのいずれかを選択します。  
  
    |モード|説明|  
    |----------|-----------------|  
    |**既定の処理**|パーティション オブジェクトの処理状態を検出して、未処理または部分的に処理されたパーティション オブジェクトを完全に処理された状態にするために必要な処理を実行します。 空のテーブルとパーティションのデータが読み込まれ、階層、計算列、およびリレーションシップが構築または再構築されます。|  
    |**完全処理**|パーティション オブジェクトとそこに含まれているすべてのオブジェクトを処理します。 既に処理されたオブジェクトに対して完全処理を実行すると、そのオブジェクト内のすべてのデータが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって削除されてから、オブジェクトが処理されます。 この種の処理は、構造上の変更をオブジェクトに加えた場合に必要となります。|  
    |**データの処理**|階層またはリレーションシップを再構築したり、計算列とメジャーを再計算したりせずに、パーティションまたはテーブルにデータを読み込みます。|  
    |**消去の処理**|パーティションからすべてのデータを削除します。|  
    |**追加の処理**|パーティションを新しいデータで増分更新します。|  
  
4.  **[処理]** チェックボックス列で、選択したモードで処理するパーティションを選択し、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [テーブル モデル パーティション (SSAS テーブル)](partitions-ssas-tabular.md)   
 [テーブル モデル パーティションの作成および管理 (SSAS テーブル)](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
