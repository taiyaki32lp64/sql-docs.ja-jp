---
title: 'レッスン 7: メジャーの作成 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef207028ab1b4f6bc084f3f4e515ae37630b771d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078431"
---
# <a name="lesson-7-create-measures"></a>レッスン 7: メジャーを作成する
  このレッスンでは、モデルに含められるメジャーを作成します。 前のレッスンで作成した計算列と同様、メジャーは、基本的には、DAX 数式を使用して作成される計算です。 ただし、計算列とは違い、メジャーはユーザーが選択した "*フィルター*" に基づいて評価されます (たとえば、PivotTable 内の行ラベル フィールドに追加された特定の列やスライサーなど)。   フィルター内の各セルの値は、適用されたメジャーによって計算されます。 メジャーは強力で柔軟な計算なので、ほとんどすべてのテーブル モデルに含めて、数値データに対する動的な計算を実行できます。 詳細については、「[メジャー (SSAS テーブル)](tabular-models/measures-ssas-tabular.md)」を参照してください。  
  
 メジャーを作成するには、メジャー グリッドを使用します。 既定では、各テーブルに空のメジャー グリッドがあります。ただし、通常はすべてのテーブルにメジャーを作成することはありません。 メジャー グリッドは、モデル デザイナーのデータ ビューで、テーブルの下に表示されます。 テーブルのメジャー グリッドを表示または非表示にするには、 **[テーブル]** メニューをクリックし、 **[メジャー グリッドの表示]** をクリックします。  
  
 メジャーを作成するには、メジャー グリッド内で空のセルをクリックし、数式バーに DAX 数式を入力します。 Enter キーを押して式の入力を完了すると、そのセルにメジャーが表示されます。 標準の集計関数を使用してメジャーを作成することもできます。その場合は、列をクリックし、ツール バーの [オート SUM] ボタン (**∑**) をクリックします。 オート SUM 機能を使用して作成したメジャーは、その列のすぐ下のメジャー グリッド セルに表示されますが、必要に応じて移動できます。  
  
 このレッスンでは、数式バーに DAX 数式を入力する方法と、オート SUM 機能を使用する方法の両方でメジャーを作成します。  
  
 このレッスンを完了するまでに時間を推定するには。**30 分**  
  
## <a name="prerequisites"></a>前提条件  
 このトピックはテーブル モデリング チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 このレッスンでは、タスクを実行する前に、前のレッスンを完了が必要があります。[レッスン 6:計算列を作成](lesson-5-create-calculated-columns.md)です。  
  
## <a name="create-measures"></a>メジャーを作成する  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>Date テーブル内に Days Current Quarter to Date メジャーを作成するには  
  
1.  モデル デザイナーで、 **Date** テーブルをクリックします。  
  
2.  テーブルの下に空のメジャー グリッドが表示されていない場合は、 **[テーブル]** メニューをクリックし、 **[メジャー グリッドの表示]** をクリックします。  
  
3.  メジャー グリッドで、左上にある空のセルをクリックします。  
  
4.  テーブルの上にある数式バーに、以下の数式を入力します。  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     数式の入力が終了したら、Enter キーを押します。  
  
     左上のセルのメジャーの名前では、すぐに**Measure 1**、結果、その後に**30**します。 メジャー名は、数式バーの数式の前にも表示されます。  
  
5.  数式バーで、メジャーの名前を変更する、名前を強調表示**Measure 1**、入力`Days Current Quarter to Date`、し、ENTER キーを押します。  
  
    > [!TIP]  
    >  数式バーで数式を入力する際には、最初にメジャー名を入力し、続けてコロン (:)、スペース、数式の順に入力することもできます。 この方法を使用すれば、メジャー名を変更する必要はありません。  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>Date テーブル内に Days in Current Quarter メジャーを作成するには  
  
1.  モデル デザイナー内の **Date** テーブルをアクティブな状態にしたまま、メジャー グリッドで、先ほど作成したメジャーの下の空のセルをクリックします。  
  
2.  数式バーで、次の数式を入力します。  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     この式では、最初にメジャー名を入力し、続けてコロン (:) を入力します。  
  
     数式の入力が終了したら、Enter キーを押します。  
  
 未完了の期間と前の期間との間に比較率を作成する場合、数式では、経過した期間の比率を考慮に入れて、それを前の期間内の同じ比率と比較する必要があります。 この場合は、[Days Current Quarter to Date]/[Days in Current Quarter] とすることで、現行期間内の経過比率を割り出すことができます。  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>Internet Sales テーブル内に Internet Distinct Count Sales Order メジャーを作成するには  
  
1.  モデル デザイナーで、 **[Internet Sales]** テーブル (タブ) をクリックします。  
  
     テーブルの下にメジャー グリッドが表示されていない場合は、 **[Internet Sales]** テーブル (タブ) を右クリックし、 **[メジャー グリッドの表示]** をクリックします。  
  
2.  **[Sales Order Number]** 列見出しをクリックします。  
  
3.  ツール バーで、[オート SUM] (**∑**) ボタンの横にある下矢印をクリックし、 **[DistinctCount]** を選択します。  
  
     オート SUM 機能が、DistinctCount 標準集計式を使用して、選択された列に対するメジャーを自動的に作成します。  
  
     メジャー グリッド内の対象列のすぐ下のセルに、メジャー名 ( **Distinct Count Sales Order Number**) が表示されます。 オート SUM 機能を使用して作成したメジャーは、メジャー グリッド内で、関連付けられた列のすぐ下のセルに自動的に配置されます。  
  
4.  メジャー グリッドで新しいメジャーをクリックし、 **[プロパティ]** ウィンドウの **[メジャー名]** に「 **Internet Distinct Count Sales Order**」と入力して名前を変更します。  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>Internet Sales テーブル内に追加のメジャーを作成するには  
  
1.  オート SUM 機能を使用して、次の名前のメジャーを作成します。  
  
    |[メジャー名]|[列]|オート SUM (∑)|[数式]|  
    |------------------|------------|-------------------|-------------|  
    |Internet Order Lines Count|Sales Order Line Number|Count|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|Sum|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|Discount Amount|Sum|=SUM([Discount Amount])|  
    |Internet Total Product Cost|Total Product Cost|Sum|=SUM([Total Product Cost])|  
    |Internet Total Sales|Sales Amount|Sum|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|Sum|=SUM([Margin])|  
    |Internet Total Tax Amt|Tax Amt|Sum|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|Sum|=SUM([Freight])|  
  
2.  メジャー グリッド内で空のセルをクリックし、数式バーを使用して、次の名前のメジャーを作成します。  
  
    > [!IMPORTANT]  
    >  メジャーは次の順序のとおりに作成する必要があります (先行するメジャーは後続のメジャー内の数式から参照されるため)。  
  
    |[メジャー名]|[数式]|  
    |------------------|-------------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
 Internet Sales テーブル用に作成されたメジャーは、ユーザー選択のフィルターによって定義された項目に関する重要な財務データ (売上、コスト、利益率など) を分析するためにも使用できます。  
  
## <a name="next-step"></a>次の手順  
 このチュートリアルを続行するには、次のレッスンに移動します。[レッスン 8: 主要業績評価指標の作成](lesson-7-create-key-performance-indicators.md)です。  
  
  
