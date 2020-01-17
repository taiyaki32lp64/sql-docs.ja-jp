---
title: 入れ子になったテーブル (中級者向けデータ マイニング チュートリアル) を伴うビューをソース、データの追加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822781"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>入れ子になったテーブルを伴うデータ ソース ビューの追加 (中級者向けデータ マイニング チュートリアル)
  マーケット バスケット モデルを作成するには、結合データをサポートしているデータ ソース ビューを使用する必要があります。 このデータ ソース ビューは、シーケンス クラスター シナリオでも使用されます。  
  
 このデータ ソース ビューがしていた場合に含まれているため、他のユーザーと異なる、*入れ子になったテーブル*します。 A*入れ子になったテーブル*については、ケース テーブル内の単一行の複数の行が含まれているテーブルです。 たとえば、モデルで顧客の購入行動を分析する場合は、顧客ごとに固有の行があるテーブルをケース テーブルとして使用するのが一般的です。 しかし、1 人の顧客が複数の商品を購入することもあります。また、顧客の一連の購入記録を分析したり、一緒に購入されることの多い商品を分析することが必要になる場合もあります。 モデルを使ってこのような購入記録を論理的に表すには、データ ソース ビューに、顧客ごとの購入記録を一覧表示するテーブルを 1 つ追加します。  
  
 この入れ子になった購入記録テーブルは、多対一のリレーションシップで顧客テーブルに関連付けられます。 入れ子になったテーブルには顧客ごとに複数の行を作成でき、各行には購入された製品 (通常、購入が行われた注文に関する情報が追加されます)、注文時の価格、適用されたプロモーションなどが記録されます。 入れ子になったテーブルの情報は、モデルへの入力または予測可能な属性として使用できます。  
  
 このレッスンでは、次のタスクを実行します。  
  
-   データ ソース ビューを追加する、[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]データ ソース。  
  
-   このビューにケース テーブルと入れ子になったテーブルを追加します。  
  
-   ケース テーブルと入れ子になったテーブルの間に多対一のリレーションシップを指定します。  
  
    > [!NOTE]  
    >  . 説明した手順に正確に従い、ケース テーブルと入れ子になったテーブルの間のリレーションシップを正しく指定して、モデルの処理時にエラーが発生しないようにすることが重要です。  
  
-   データの列がモデルでどのように使用されるかを定義します。  
  
 操作のケースと、入れ子になったテーブルと入れ子になったテーブル キーを選択する方法の詳細については、次を参照してください。[入れ子になったテーブル&#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)します。  
  
### <a name="to-add-a-data-source-view"></a>データ ソース ビューを追加するには  
  
1.  ソリューション エクスプ ローラーで右クリックして**データ ソース ビュー**、し、**新しいデータ ソース ビュー**します。  
  
     データ ソース ビュー ウィザードが開きます。  
  
2.  **[データ ソース ビュー ウィザードへようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **データ ソースの選択**] ページ [**リレーショナル データ ソース**を選択、[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]基本的なデータ マイニング チュートリアル」で作成したデータ ソース。 **[次へ]** をクリックします。  
  
4.  **テーブルおよびビュー**ページで、次の表を選択し、新しいデータ ソース ビューに含める、右矢印をクリックします。  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  **[次へ]** をクリックします。  
  
6.  **ウィザードの完了** ページで、既定では、データ ソース ビューの名前は[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]します。 名を変更して`Orders`、 をクリックし、**完了**します。  
  
     データ ソース ビュー デザイナーが開き、`Orders`データ ソース ビューが表示されます。  
  
### <a name="to-create-a-relationship-between-tables"></a>2 つのテーブル間のリレーションシップを作成するには  
  
1.  データ ソース ビュー デザイナーで、2 つのテーブルを横に並べて配置します (vAssocSeqLineItems テーブルが左で vAssocSeqOrders テーブルが右)。  
  
2.  選択、 **OrderNumber** vAssocSeqLineItems テーブル内の列。  
  
3.  列を vAssocSeqOrders テーブルにドラッグしてに、 **OrderNumber**列。  
  
    > [!IMPORTANT]  
    >  確実にドラッグ、 **OrderNumber**結合の一方の側を表す vAssocSeqOrders ケース テーブルに、結合の"多"側を表す vAssocSeqLineItems の入れ子になったテーブルの列。  
  
     新しい*多対一のリレーションシップ*vAssocSeqLineItems および vAssocSeqOrders テーブルの間に存在するようになりました。 テーブルを正しく結合した場合は、データ ソース ビューに次のように表示されます。  
  
     ![入れ子になったテーブルとケース テーブルの予想される多対一結合](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "入れ子になったテーブルとケース テーブルの予想される多対一結合")  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Market Basket 構造およびモデルの作成&#40;中級者向けデータ マイニング チュートリアル&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>参照  
 [中級者向けデータ マイニング チュートリアル&#40;Analysis Services - データ マイニング&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [マイニング構造 &#40;Analysis Services - データ マイニング&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [マイニング モデル (Analysis Services - データ マイニング)](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
