---
title: データ マイニング クエリのタイムアウト値の変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 640d07115e2a071bb5d57e87955c11670f4c38b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085889"
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>データ マイニング クエリのタイムアウト値の変更
  リフト チャートの作成時や、予測クエリの実行時には、予測に必要なすべてのデータの生成に時間がかかる場合があります。 クエリがタイムアウトするのを防ぐため、クエリの完了を [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーで待機する時間を制御する値を変更できます。  
  
 既定値は 15 ですが、モデルが複雑な場合やデータ ソースが大規模な場合、これでは十分でない場合があります。 必要に応じて値を大幅に増やし、処理に十分な時間を確保します。 たとえば、 **[クエリ タイムアウト]** を 600 に設定すると、クエリを 10 分間実行し続けることができます。  
  
 予測クエリの詳細については、「 [データ マイニングのクエリ タスクと操作方法](data-mining-query-tasks-and-how-tos.md)」を参照してください。  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>データ マイニング クエリのタイムアウト値の構成  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、 **[ツール]** メニューの **[オプション]** をクリックします。  
  
2.  **[オプション]** ペインで **[ビジネス インテリジェンス デザイナー]** を展開します。  
  
3.  **[クエリ タイムアウト]** ボックスをクリックし、秒数の値を入力します。  
  
## <a name="see-also"></a>参照  
 [データ マイニングのクエリ タスクと操作方法](data-mining-query-tasks-and-how-tos.md)   
 [データ マイニング クエリ](data-mining-queries.md)  
  
  
