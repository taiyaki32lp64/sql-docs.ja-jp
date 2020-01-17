---
title: データ マイニング アルゴリズム (SQL Server データ マイニング アドイン) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0bf6c0c1126dff29107636e0956d92d4b314a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086511"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>データ マイニング アルゴリズム (SQL Server データ マイニング アドイン)
  Office 用データ マイニング アドインは、次のデータ マイニング アルゴリズムを使用して分析モデルの作成をサポートします。 すべてのアルゴリズムは、よく知られている機械学習メソッドに基づいており、Microsoft Research によって実装されたものです。  
  
## <a name="algorithms"></a>アルゴリズム  
  
|機械学習メソッド|しくみ|  
|-----------------------------|------------------|  
|Microsoft アソシエーション ルール アルゴリズム|どの製品がともに購入されているか、またはどのイベントがともに発生するかを検出し、おすすめを作成するためのモデルを使用します。<br /><br /> [https://msdn.microsoft.com/library/ms174916.aspx](https://msdn.microsoft.com/library/ms174916.aspx)|  
|Microsoft クラスタリング アルゴリズム|市場セグメントを定義し、関連のある複数の顧客を自動的にグループ化するか、データ内のリレーションシップを見つけてそれ以降のマイニングで使用できるようにします。<br /><br /> [https://msdn.microsoft.com/library/ms174879.aspx](https://msdn.microsoft.com/library/ms174879.aspx)|  
|Microsoft デシジョン ツリー アルゴリズム|データ内のさまざまな要素間で、従来は不明だったリレーションシップを識別し、意思決定を下すためにより適切な情報を提供するか、特定の結果につながる要因を見つけます。<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
|Microsoft 線形回帰アルゴリズム|数値形式の結果に寄与する要因を表す算術式を見つけます。<br /><br /> [https://msdn.microsoft.com/library/ms174824.aspx](https://msdn.microsoft.com/library/ms174824.aspx)|  
|Microsoft ロジスティック回帰アルゴリズム|バイナリ結果に寄与する要素を見つけ、それらの要素が結果にどのような影響を及ぼすかを研究します。<br /><br /> [https://msdn.microsoft.com/library/ms174828.aspx](https://msdn.microsoft.com/library/ms174828.aspx)|  
|Microsoft Naïve Bayes アルゴリズム|データ内のリレーションシップを探索し、結果との関連性が最も強いリレーションシップを見つけます。<br /><br /> [https://msdn.microsoft.com/library/ms174806.aspx](https://msdn.microsoft.com/library/ms174806.aspx)|  
|Microsoft ニューラル ネットワーク アルゴリズム|複数の入力と複数の出力の間に存在する隠されたリレーションシップを見つけます。 探索または予測の目的で使用します。<br /><br /> [https://msdn.microsoft.com/library/ms174941.aspx](https://msdn.microsoft.com/library/ms174941.aspx)|  
|Microsoft Time Series アルゴリズム|履歴データを使用して将来の値を予測します。<br /><br /> [https://msdn.microsoft.com/library/ms174923.aspx](https://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>[詳細設定オプション]  
 Excel 用のデータ マイニング クライアントを使用する場合は、独自のデータ マイニング構造およびモデルを作成したり、アルゴリズムのパラメーターを調整したりすることができます。  
  
 [アルゴリズム パラメーター &#40;SQL Server データ マイニング アドイン&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 これらの詳細オプションを使用してモデルをカスタマイズする方法は 2 つあります。  
  
-   使用して、**データ マイニング クエリ**モデルを作成するウィザード。  
  
-   **データ マイニング クライアント**、ウィザードを起動した後、をクリックして**パラメーター**します。  
  
## <a name="see-also"></a>参照  
 [クエリ&#40;SQL Server データ マイニング アドイン&#41;](query-sql-server-data-mining-add-ins.md)   
 [モデリングの高度な&#40;データ マイニング Excel 用アドイン&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  
