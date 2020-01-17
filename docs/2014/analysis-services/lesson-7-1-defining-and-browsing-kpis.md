---
title: Kpi の定義と参照 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 648b9a02-1278-4f11-b940-6f0de6a4042d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f5d61b3880474851aa0c7302e402ff2f0ac0a47
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493793"
---
# <a name="defining-and-browsing-kpis"></a>KPI の定義と表示
  主要業績評価指標 (KPI) を定義するには、まず、KPI の名前と、KPI に関連するメジャー グループを定義します。 すべてのメジャー グループ、または単一のメジャー グループを KPI に関連付けることができます。 その後、KPI の次のような要素を定義します。  
  
-   値式  
  
     値式とは、物理的メジャー (売上高など)、計算されるメジャー (利益など)、または KPI 内で多次元式 (MDX) を使用して定義される計算です。  
  
-   目標式  
  
     目標式とは、値、または値に解決される MDX 式です。目標式では、値式が定義するメジャーのターゲットを定義します。 たとえば、企業の経営層が目標とする売上または利益の増加額を目標式にすることができます。  
  
-   状態式  
  
     状態式とは、目標式と比較した値式の現在の状態を評価するために [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用される MDX 式です。 目標式は -1 ～ +1 の範囲で正規化された値です (-1 は非常に悪い、+1 は非常に良い)。 状態式では、目標式と比べた値式の状態を簡単に判別できるようにグラフィックが表示されます。  
  
-   傾向式  
  
     傾向式とは、目標式と比較した値式の現在の傾向を評価するために [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] で使用される MDX 式です。 傾向式を使用すれば、目標式と比べて値式が改善しているか、それとも悪化しているかをビジネス ユーザーがすばやく判別できます。 いずれか 1 つのグラフィックを傾向式に関連付けることで、ビジネス ユーザーは傾向をすばやく把握できるようになります。  
  
 これらの KPI 要素の定義に加えて、いくつかの KPI プロパティも定義します。 定義するプロパティには、表示フォルダー、親 KPI (他の KPI から計算される KPI の場合)、現在の時間メンバー (存在する場合)、KPI の重み (存在する場合)、KPI についての説明などがあります。  
  
> [!NOTE]  
>  KPI の詳しいサンプルについては、[計算ツール] ペインの [テンプレート] タブの KPI サンプル、または **Adventure Works DW 2012** サンプル データ ウェアハウスの KPI サンプルを参照してください。 このデータベースのインストールの詳細については、「 [Analysis Services 多次元モデリング チュートリアル用のサンプル データおよびプロジェクトのインストール](install-sample-data-and-projects.md)」を参照してください。  
  
 このレッスンの実習では、KPI を [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクト内で定義した後、これらの KPI を使用して [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブを表示します。 次の KPI を定義します。  
  
-   Reseller Revenue  
  
     この KPI を使用して、再販業者の実際の売上高を販売ノルマと比較し、売上高が目標にどれだけ近いか、どのような傾向で目標を達成しつつあるかを計測します。  
  
-   Product Gross Profit Margin  
  
     この KPI を使用して、各製品カテゴリの売上総利益率がその具体目標値にどれだけ近いか、およびこの目標の達成傾向を判断します。  
  
## <a name="defining-the-reseller-revenue-kpi"></a>Reseller Revenue KPI の定義  
  
1.  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブのキューブ デザイナーを開いて、 **[KPI]** タブをクリックします。  
  
     **[KPI]** タブにはいくつかのペインがあります。 タブの左側には **[KPI オーガナイザー]** ペインと **[計算ツール]** ペインがあります。 **[KPI オーガナイザー]** ペインで KPI を選択すると、その KPI の詳細が中央の表示ペインに表示されます。  
  
     次の図は、キューブ デザイナーの **[KPI]** タブを示しています。  
  
     ![キューブデザイナーの [Kpi] タブ](../../2014/tutorials/media/l7-kpi-1.gif "キューブデザイナーの [Kpi] タブ")  
  
2.  **[KPI]** タブのツール バーで **[新しい KPI]** ボタンをクリックします。  
  
     次の図のように、空白の KPI テンプレートが表示ペインに表示されます。  
  
     ![表示ウィンドウの空白の KPI テンプレート](../../2014/tutorials/media/l7-kpi-2.gif "表示ウィンドウの空白の KPI テンプレート")  
  
3.  **[名前]** ボックスに「`Reseller Revenue`」と入力し、 **[関連付けられたメジャーグループ]** ボックスの一覧で **[再販業者の売上]** を選択します。  
  
4.  **[計算ツール]** ペインの **[メタデータ]** タブで、 **[Measures]** 、 **[Reseller Sales]** の順に展開します。次に、 **Reseller Sales-Sales Amount** メジャーを **[値式]** ボックスにドラッグします。  
  
5.  **[計算ツール]** ペインの **[メタデータ]** タブで、 **[Measures]** 、 **[Sales Quotas]** の順に展開します。次に、 **Sales Amount Quota** メジャーを **[目標式]** ボックスにドラッグします。  
  
6.  **[状態インジケーター]** ボックスの一覧で **[ゲージ]** が選択されていることを確認します。次に、以下の MDX 式を **[状態式]** ボックスに入力します。  
  
    ```  
    Case  
     When   
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.95  
       Then 1  
     When  
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")<.95  
       And   
      KpiValue("Reseller Revenue")/KpiGoal("Reseller Revenue")>=.85  
       Then 0  
      Else-1  
    End  
    ```  
  
     この MDX 式は、目標達成度を評価する基になります。 この MDX 式では、再販業者の実際の売上が目標の 85% を超えていれば、選択されたグラフィックを値 0 を使用して設定します。 グラフィックとしてゲージが選択されているため、ゲージ内のポインターは空と満杯の中間を指します。 再販業者の実際の売上が 90% を超えている場合、ゲージ上のポインターは空から満杯に向かって 3/4 の位置に示されます。  
  
7.  **[傾向インジケーター]** ボックスの一覧で **[標準の矢印]** が選択されていることを確認します。次に、以下の式を **[傾向式]** ボックスに入力します。  
  
    ```  
    Case  
     When IsEmpty  
      (ParallelPeriod  
       ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
      Then 0    
     When  (  
      KpiValue("Reseller Revenue") -   
       (KpiValue("Reseller Revenue"),   
        ParallelPeriod  
         ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
          /  
          (KpiValue ("Reseller Revenue"),  
           ParallelPeriod  
            ([Date].[Calendar Date].[Calendar Year],1,  
             [Date].[Calendar Date].CurrentMember)))  
           >=.02  
      Then 1  
       When(  
        KpiValue("Reseller Revenue") -   
         (KpiValue ( "Reseller Revenue" ),  
          ParallelPeriod  
           ([Date].[Calendar Date].[Calendar Year],1,  
            [Date].[Calendar Date].CurrentMember))  
           /  
            (KpiValue("Reseller Revenue"),  
             ParallelPeriod  
              ([Date].[Calendar Date].[Calendar Year],1,  
                [Date].[Calendar Date].CurrentMember)))  
            <=.02  
      Then -1  
       Else 0  
    End  
    ```  
  
     この MDX 式は、定義された目標がどのように達成されつつあるかの傾向を評価する基になります。  
  
## <a name="browsing-the-cube-by-using-the-reseller-revenue-kpi"></a>Reseller Revenue KPI を使用したキューブの表示  
  
1.  **の** [ビルド] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]メニューで、 **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **[KPI]** タブのツール バーの **[ブラウザー ビュー]** ボタンをクリックし、 **[再接続]** をクリックします。  
  
     各ディメンションの既定のメンバーの値に基づき、状態ゲージおよび傾向ゲージが再販業者の売上の **[KPI ブラウザー]** ペインに表示され、それと共に値と目標の値が表示されます。 現時点では、どのディメンションのどのメンバーも既定のメンバーとしてまだ定義されていないため、各ディメンションの既定のメンバーは全レベルの全メンバーです。  
  
3.  [フィルター] ペインで、 **[ディメンション]** ボックスの一覧の **[Sales Territory]** をクリックし、 **[階層]** ボックスの一覧の **[Sales Territories]** をクリックし、 **[演算子]** ボックスの一覧の **[等しい]** をクリックします。次に、 **[フィルター式]** ボックスの一覧で **[North America]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
4.  **[フィルター]** ペインの次の行で、 **[ディメンション]** ボックスの一覧の **[Date]** をクリックし、 **[階層]** ボックスの一覧の **[Calendar Date]** をクリックし、 **[演算子]** ボックスの一覧の **[等しい]** をクリックします。次に、 **[フィルター式]** ボックスの一覧で **[Q3 CY 2007]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
5.  **[KPI ブラウザー]** ペイン内の任意の場所をクリックすると、 **Reseller Revenue KPI**の値が更新されます。  
  
     KPI の **[値]** 、 **[目標]** 、および **[状態]** セクションに新しい期間の値が反映されていることがわかります。  
  
## <a name="defining-the-product-gross-profit-margin-kpi"></a>Product Gross Profit Margin KPI の定義  
  
1.  **[KPI]** タブのツール バーの **[フォーム ビュー]** ボタンをクリックして、 **[新しい KPI]** ボタンをクリックします。  
  
2.  **名前** ボックスに「`Product Gross Profit Margin`」と入力し、**関連付けられているメジャーグループ** ボックスの一覧に  **\<All >** が表示されていることを確認します。  
  
3.  **[計算ツール]** ペインの **[メタデータ]** タブで、 **Total GPM** メジャーを **[値式]** ボックスにドラッグします。  
  
4.  **[目標式]** ボックスに、次の式を入力します。  
  
    ```  
    Case  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Accessories]  
        Then .40                   
        When [Product].[Category].CurrentMember   
          Is [Product].[Category].[Bikes]  
        Then .12                  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Clothing]  
        Then .20  
        When [Product].[Category].CurrentMember Is  
          [Product].[Category].[Components]  
        Then .10  
        Else .12              
    End  
    ```  
  
5.  **[状態インジケーター]** ボックスの一覧で **[シリンダー]** をクリックします。  
  
6.  以下の MDX 式を **[状態式]** ボックスに入力します。  
  
    ```  
    Case  
        When KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) >= .90  
        Then 1  
        When KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) <  .90  
             And   
             KpiValue( "Product Gross Profit Margin" ) /   
             KpiGoal ( "Product Gross Profit Margin" ) >= .80  
        Then 0  
        Else -1  
    End  
    ```  
  
     この MDX 式は、目標達成度を評価する基になります。  
  
7.  **[傾向インジケーター]** ボックスの一覧で **[標準の矢印]** が選択されていることを確認します。次に、以下の MDX 式を **[傾向式]** ボックスに入力します。  
  
    ```  
    Case  
    When IsEmpty  
      (ParallelPeriod  
       ([Date].[Calendar Date].[Calendar Year],1,  
           [Date].[Calendar Date].CurrentMember))  
      Then 0    
       When VBA!Abs  
        (  
          KpiValue( "Product Gross Profit Margin" ) -   
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
              ParallelPeriod  
              (   
                [Date].[ Calendar Date].[ Calendar Year],  
                1,  
                [Date].[ Calendar Date].CurrentMember  
              )  
            ) /  
            (  
              KpiValue ( "Product Gross Profit Margin" ),  
              ParallelPeriod  
              (   
                [Date].[ Calendar Date].[ Calendar Year],  
                1,  
                [Date].[ Calendar Date].CurrentMember  
              )  
            )    
          ) <=.02  
      Then 0  
      When KpiValue( "Product Gross Profit Margin" ) -   
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
             ParallelPeriod  
             (   
               [Date].[ Calendar Date].[ Calendar Year],  
               1,  
               [Date].[ Calendar Date].CurrentMember  
             )  
           ) /  
           (  
             KpiValue ( "Product Gross Profit Margin" ),  
             ParallelPeriod  
             (   
               [Date].[Calendar Date].[Calendar Year],  
               1,  
               [Date].[Calendar Date].CurrentMember  
             )  
           )  >.02  
      Then 1  
      Else -1  
    End  
    ```  
  
     この MDX 式は、定義された目標がどのように達成されつつあるかの傾向を評価する基になります。  
  
## <a name="browsing-the-cube-by-using-the-total-gross-profit-margin-kpi"></a>Total Gross Profit Margin KPI を使用したキューブの表示  
  
1.  **[ビルド]** メニューで、 **[Analysis Services Tutorial の配置]** をクリックします。  
  
2.  配置が正常に完了したら、 **[KPI]** タブのツール バーの **[再接続]** をクリックして、 **[ブラウザー ビュー]** をクリックします。  
  
     @No__t_0 KPI が表示され、 **Q3 CY 2007**と**北米**販売区域の kpi 値が表示されます。  
  
3.  **[フィルター]** ペインで、 **[ディメンション]** ボックスの一覧の **[Product]** をクリックし、 **[階層]** ボックスの一覧の **[Category]** をクリックし、 **[演算子]** ボックスの一覧の **[等しい]** をクリックします。次に、 **[フィルター式]** ボックスの一覧で **[Bikes]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
     Q3 CY 2007 の North America における小売店のバイクの売上総利益率が表示されます。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 8 : アクションの定義](lesson-8-defining-actions.md)  
  
  
