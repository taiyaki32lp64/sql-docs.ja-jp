---
title: 'レッスン 6: 計算列の作成 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58ba761f3e32f13ddcf81dc9875057195298c705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078556"
---
# <a name="lesson-6-create-calculated-columns"></a>レッスン 6: 計算列の作成
  このレッスンでは、計算列を追加して、モデル内に新しいデータを作成します。 計算列は、モデル内の既存のデータに基づいて機能します。 詳細については、「[計算列 (SSAS テーブル)](tabular-models/ssas-calculated-columns.md)」を参照してください。  
  
 このレッスンでは、3 つの異なるテーブル内に、5 つの新しい計算列を作成します。 手順は実習ごとに少しずつ異なります。 これは、新しい列を作成したり、それらの名前を変更したり、それらをテーブル内のさまざまな場所へ配置するのには、いくつかの方法があることを示すためです。  
  
 このレッスンを完了するまでに時間を推定するには。**15 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 5: リレーションシップの作成](lesson-4-create-relationships.md)です。  
  
## <a name="create-calculated-columns"></a>計算列の作成  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Date テーブル内に Month Calendar 計算列を作成する  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で、 **[モデル]** メニューをクリックし、 **[モデル ビュー]** をポイントして、 **[データ ビュー]** をクリックします。  
  
     計算列は、モデル デザイナーのデータ ビューでのみ作成できます。  
  
2.  モデル デザイナーで、 **Date** テーブル (タブ) をクリックします。  
  
3.  右クリックし、 **Calendar Quarter**列、およびクリック**列の挿入**します。  
  
     という名前の新しい列**CalculatedColumn1**の左側に挿入される、 **Calendar Quarter**列。  
  
4.  テーブルの上にある数式バーに、以下の数式を入力します。 オートコンプリートを利用すると、列やテーブルの完全修飾名を簡単に入力できるだけでなく、使用可能な関数の一覧も表示できます。  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
     すべての行の計算列に値が入力されます。 テーブルを下にスクロールすると、この列の行が、各行のデータに基づいて、異なる値を保持できることがわかります。  
  
    > [!NOTE]  
    >  エラーが発生した場合、数式内の列名に変更した列名を一致することを確認[レッスン 3。列名の変更](rename-columns.md)します。  
  
5.  この列の名前を変更`Month Calendar`します。  
  
 Month Calendar 計算列は、Month の並べ替え可能な名前を提供します。  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Date テーブル内に Day of Week 計算列を作成する  
  
1.  **Date** テーブルがアクティブな状態のままで、 **[列]** メニューをクリックし、 **[列の追加]** をクリックします。  
  
     新しい列がテーブルの右端に追加されます。  
  
2.  数式バーで、次の数式を入力します。  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
3.  列の名前を変更`Day of Week`します。  
  
4.  列見出しをクリックし、列を **Day Name** 列と **Day of Month** 列の間にドラッグします。  
  
    > [!TIP]  
    >  テーブル内の列を移動することで、列が参照しやすくなります。  
  
 Day of Week 計算列では、曜日を表す、並べ替え可能な名前が提供されます。  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Product テーブル内に Product Subcategory Name 計算列を作成する  
  
1.  モデル デザイナーで、 **Product** テーブルを選択します。  
  
2.  テーブルの右端までスクロールします。 右端にある **Add Column** (斜体) という列の列見出しをクリックします。  
  
3.  数式バーで、次の数式を入力します。  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
4.  列の名前を変更`Product Subcategory Name`します。  
  
 Product Subcategory Name 計算列は、Product テーブル内に、Product Subcategory テーブルの Product Subcategory Name 列のデータを含んだ階層を作成するために使用されます。 階層は、複数のテーブルにまたがって存在することはできません。 階層の作成は、この後のレッスン 7 で行います。  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Product テーブル内に Product Category Name 計算列を作成する  
  
1.  **Product** テーブルがアクティブな状態のままで、 **[列]** メニューをクリックし、 **[列の追加]** をクリックします。  
  
2.  数式バーで、次の数式を入力します。  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
3.  列の名前を変更`Product Category Name`します。  
  
 Product Category Name 計算列は、Product テーブル内に、Product Category テーブルの Product Category Name 列のデータを含んだ階層を作成するために使用されます。 階層は、複数のテーブルにまたがって存在することはできません。  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Internet Sales テーブル内に Margin 計算列を作成する  
  
1.  モデル デザイナーで、 **[Internet Sales]** テーブルを選択します。  
  
2.  新しい列を追加します。  
  
3.  数式バーで、次の数式を入力します。  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
4.  列の名前を変更`Margin`します。  
  
5.  列を、 **Sales Amount** 列と **Tax Amt** 列の間にドラッグします。  
  
 Margin 計算列は、各 (製品) 行の利益率を分析するために使用されます。  
  
## <a name="next-step"></a>次の手順  
 このレッスンを続行するには、次のレッスンに移動します。[レッスン 7: メジャーを作成](lesson-6-create-measures.md)です。  
  
  
