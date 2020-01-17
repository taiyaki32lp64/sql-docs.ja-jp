---
title: データ マイニング デザイナーで単一クエリの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 795347e0ef2bdee226daff57e85e2b02f8b00c9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66085308"
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>データ マイニング デザイナーでの単一クエリの作成
  単一クエリは、1 つのケースに関する予測を作成する場合に便利です。 単一クエリの詳細については、「 [データ マイニング クエリ](data-mining-queries.md)」を参照してください。  
  
 データ マイニング デザイナーの **[マイニング モデル予測]** タブでは、多様なクエリを作成できます。 デザイナーを使用するか、データ マイニング拡張機能 (DMX) ステートメントを入力することにより、クエリを作成できます。 最初にデザイナーで作成したクエリを、DMX ステートメントを変更するか、WHERE 句や ORDER BY 句を追加することによって変更することもできます。  
  
 クエリ デザイン ビューとクエリ テキスト ビューを切り替えるには、ツール バーの最初のボタンをクリックします。 クエリ テキスト ビューでは、予測クエリ ビルダーによって作成される DMX コードを表示できます。 また、クエリの実行、クエリの変更、および変更済みのクエリの実行も可能です。 ただし、クエリ デザイン ビューに戻ると、変更したクエリは保持されません。  
  
 次のコードは、メーリング対象モデル TM_Decision_Tree に対する単一クエリの例を示しています。  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 以下の手順は、この予測クエリを作成する方法について説明しています。  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>データ マイニング デザイナーを使用して単一クエリを作成するには  
  
1.  データ マイニング デザイナーの **[マイニング モデル予測]** タブをクリックします。  
  
2.  **[マイニング モデル]** テーブルの **[モデルの選択]** をクリックします。  
  
     **[マイニング モデルの選択]** ダイアログ ボックスが開き、現在のプロジェクトにあるすべてのマイニング構造が表示されます。  
  
     予測の作成に使用するモデルを選択します。  
  
     たとえば、このトピックの冒頭に示したサンプル コードを作成するには、TM_Decision_Tree を選択して **[OK]** をクリックします。  
  
3.  **[マイニング モデル予測]** タブのツール バー上の **[単一クエリ]** をクリックします。  
  
     **[単一クエリ入力]** テーブルがタブに表示され、テーブルの列が **[マイニング モデル]** テーブルの列に自動的にマップされます。  
  
4.  **[単一クエリ入力]** テーブルの **[値]** 列で、予測を作成するケースについて説明した値を選択します。  
  
     たとえば、選択**2**の**Number Children At Home**、し、入力`45`の**年齢**します。  
  
5.  **[マイニング モデル]** テーブルの予測可能列をタブの下部にある **[変換元]** 列にドラッグします。必要に応じて、列の別名を入力できます。  
  
     たとえば、 **[Bike Buyer]** を **[変換元]** 列にドラッグします。  
  
6.  クエリに関数を追加するには、 **[変換元]** 列のドロップダウン リストから **[予測関数]** または **[カスタム式]** をクリックします。  
  
     たとえば、 **[予測関数]** をクリックして **[PredictProbability]** を選択します。  
  
7.  **PredictProbability** 行の **[条件と引数]** をクリックし、予測する列の名前と、必要に応じて予測する特定の値を入力します。  
  
     たとえば、「 `[Bike Buyer], 1`」のように入力します。  
  
8.  **PredictProbability** 行の **[別名]** ボックスをクリックし、新しい列を参照する名前を入力します。  
  
     たとえば、「 `ProbableBuyer`」のように入力します。  
  
9. **[マイニング モデル予測]** タブのツール バー上の **[クエリ結果ビューに切り替え]** をクリックします。  
  
     新しい画面が開き、クエリの結果が表示されます。 作成した DMX ステートメントを表示するには、 **[SQL]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [予測クエリ (データ マイニング)](prediction-queries-data-mining.md)  
  
  
