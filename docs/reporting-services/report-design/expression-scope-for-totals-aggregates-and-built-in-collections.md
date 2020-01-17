---
title: 合計、集計、および組み込みコレクションの式のスコープ | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a8d24287-8557-4b03-bea7-ca087f449b62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c822f0b6a3a17ccba2afbaf8bf0a9e4a4e2f7b12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65579820"
---
# <a name="expression-scope-for-totals-aggregates-and-built-in-collections"></a>合計、集計、および組み込みコレクションの式のスコープ
  式の作成に関して、 *スコープ* という用語は、さまざまな文脈で用いられています。 スコープは、式を評価するのに使用するデータ、表示されたページのテキスト ボックスのセット、または表示と非表示を切り替えることのできるレポート アイテムのセットを示します。 *スコープ* という用語は、式の評価、集計関数の構文、条件付き表示に関連したトピックと、これらの領域に関連したエラー メッセージで使用されます。 次の説明を参考にして、どの意味で *スコープ* が適用されているかを区別してください。  
  
-   **データ スコープ** データ スコープは、レポート プロセッサがレポート データとレポート レイアウトを組み合わせ、テーブルやグラフなどのデータを表示するデータ領域を作成する場合に使用するスコープの階層です。 データ スコープを理解することで、次のような操作を行う場合に目的の結果を得ることができます。  
  
    -   **集計関数を使用する式を作成する** 集計するデータを示します。 レポート内の式の場所は、集計計算のスコープに含まれるデータに影響します。  
  
    -   **テーブルまたはマトリックスにスパークラインを追加する** グラフの軸の範囲の最小値と最大値を示し、テーブルまたはマトリックスの入れ子になったインスタンスを揃えます。  
  
    -   **テーブルまたはマトリックスにインジケーターを追加する** ゲージのスケールの最小値と最大値を示し、テーブルまたはマトリックスの入れ子になったインスタンスを揃えます。  
  
    -   **並べ替え式を作成する** 複数の関連レポート アイテムの並べ替え順序を同期するために使用できるコンテナー スコープを示します。  
  
-   **セル スコープ** セル スコープは、セルが属する Tablix データ領域内の行グループと列グループのセットです。 各 Tablix セルには、既定でテキスト ボックスが含まれます。 テキスト ボックスの値は式です。 セルの場所によって、式の集計計算に指定できるデータ スコープが決まります。  
  
-   **レポート アイテムのスコープ** レポート アイテムのスコープは、表示されたレポート ページのアイテムのコレクションを表します。 レポート プロセッサは、データとレポート レイアウト要素を組み合わせ、コンパイル済みのレポート定義を生成します。 この処理中に、テーブルやマトリックスなどのデータ領域は、レポート データをすべて表示するように必要に応じて拡張されます。 次にコンパイル済みレポートがレポート レンダラーによって処理されます。 レポート レンダラーによって、各ページに表示されるレポート アイテムが決まります。 レポート サーバーでは、各ページは表示する操作に応じて表示されます。 レポートをエクスポートする場合は、すべてのページが表示されます。 レポート アイテム スコープを理解することで、次のような操作を行う場合に目的の結果を得ることができます。  
  
    -   **切り替えアイテムを追加する** レポート アイテムの表示を制御する切り替えを追加するためのテキスト ボックスを示します。 切り替えは、切り替えるレポート アイテムのスコープ内にあるテキスト ボックスにのみ追加できます。  
  
    -   **ページ ヘッダーおよびページ フッターに式を作成する** 表示されたページ上のテキスト ボックスまたは他のレポート アイテムで使用できる式の値を示します。  
  
 スコープを理解することで、式を正しく作成し、目的の結果を得ることができます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DataScope"></a> データ スコープとデータ階層について  
 データ スコープは、レポート データのセットを示します。 データ スコープには、固有の包含関係を持つ自然階層が存在します。 階層の上位のスコープには、下位の階層のスコープが含まれます。 次のデータ スコープの一覧では、最もデータの多いものから順に階層について説明します。  
  
-   **データセット フィルターが適用された後のデータセット** データ領域、またはレポート本文内のレポート アイテムにリンクされたレポート データセットを示します。 集計には、データセットのフィルター式が適用された後の、レポート データセットのデータが使用されます。 つまり、共有データセットの場合は、共有データセットの定義内のフィルターとレポート内の共有データセットのインスタンス内のフィルターの両方になります。  
  
-   **データ領域** データ領域のフィルター式および並べ替え式が適用された後のデータ領域のデータを示します。 データ領域の集計を計算する際にはグループ フィルターが使用されません。  
  
-   **グループ フィルターが適用された後のデータ領域のグループ** 親グループと子グループにグループ式およびグループ フィルターが適用された後のデータを示します。 テーブルの場合は、行グループと列グループになります。 グラフの場合は、系列グループとカテゴリ グループになります。 スコープの包含関係を明確にするため、各親グループにはその子グループが含まれています。  
  
-   **入れ子になったデータ領域** 入れ子になったデータ領域が追加されたセルのコンテキストで、入れ子になったデータ領域のフィルター式と並べ替え式が適用された後の、そのデータ領域のデータを示します。  
  
-   **入れ子になったデータ領域の行グループと列グループ** 入れ子になったデータ領域のグループ式とグループ フィルターが適用された後のデータを示します。  
  
 コンテナー スコープと包含されるスコープを理解しておくことは、集計関数を含んだ式を作成する場合に重要です。  
  
##  <a name="Aggregates"></a> セル スコープと式  
 スコープを指定すると、集計計算に使用するデータがレポート プロセッサに対して示されます。 式と式の場所に応じて、有効なスコープは *コンテナー スコープ*(親スコープとも呼ばれます) または *包含されるスコープ*(子または入れ子になったスコープとも呼ばれます) になります。 一般に、集計計算では個々のグループ インスタンスを指定することはできません。 すべてのグループ インスタンスの集計は指定できます。  
  
 レポート プロセッサはレポート データセットのデータと Tablix データ領域を組み合わせ、グループ式を評価し、グループ インスタンスを表すのに必要な行と列を作成します。 各 Tablix セル内のテキスト ボックスにある式の値は、セル スコープのコンテキストで評価されます。 Tablix の構造によっては、セルは複数の行グループおよび列グループに属することができます。 集計関数では、以下のいずれかのスコープを使用して、使用するスコープを指定できます。  
  
-   **既定のスコープ** レポート プロセッサが式を評価する場合に計算のスコープ内にあるデータ。 そのセルまたはデータ ポイントが属している最も内側のグループ セットが既定のスコープとなります。 Tablix データ領域では、行グループと列グループをセットに含めることができます。 グラフ データ領域の場合は、カテゴリ グループと系列グループにセットを含めることができます。  
  
-   **名前付きスコープ** 式のスコープ内にあるデータセット、データ領域、またはデータ領域グループの名前。 集計計算では、コンテナー スコープを指定できます。 行グループと列グループの両方の名前付きスコープを 1 つの式で指定することはできません。 式が集計の集計に使用される場合を除き、包含されたスコープを指定することはできません。  
  
     次の式は、SellStartDate と LastReceiptDate の間にある年数を生成します。 これらのフィールドは、DataSet1 と DataSet2 の異なる 2 つのデータセットに含まれます。 集計関数である [First 関数 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-first-function.md) は、DataSet1 にある SellStartDate の最初の値と、DataSet2 にある LastReceiptDate の最初の値を返します。  
  
    ```  
    =DATEDIFF("yyyy", First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   **ドメイン スコープ** 同期スコープとも呼ばれます。 入れ子になったデータ領域の式の評価に適用されるデータ スコープの種類。 ドメイン スコープはすべてのグループ インスタンスの集計を示すのに使用されるため、入れ子になったインスタンスを揃えて簡単に比較できます。 たとえば、値を並べるには、テーブルに埋め込まれたスパークラインの範囲と高さを揃えます。  
  
 レポートの場所によっては、スコープを指定する必要があります。 たとえば、デザイン画面上のテキスト ボックスには、 `=Max(Fields!Sales.Value,"Dataset1")`のように、使用するデータセットの名前を指定する必要があります。 その他の場所には、暗黙的な既定のスコープが存在します。 たとえば、グループ スコープ内でテキスト ボックスの集計を指定しない場合は、既定の集計 First が使用されます。  
  
 各集計関数のトピックには、使用可能なスコープが一覧表示されます。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
##  <a name="Examples"></a> テーブル データ領域の集計式の例  
 既定以外のスコープを指定する式を作成するには練習が必要です。 次の図と表は、さまざまなスコープを理解するのに役立ちます。 図は、年度、四半期、および販売区域ごとの販売品目の数量を表した販売情報テーブル内の各セルの名称を示したものです。 行グループと列グループの構造を表示する行ハンドルと列ハンドルの視覚的な手掛かりが、入れ子になったグループを示しています。 テーブルの構造は次のとおりです。  
  
-   テーブル ヘッダー。コーナー セルと列グループ ヘッダーを含む 3 つの行を含んでいます。  
  
-   2 つの入れ子になった行グループ。Cat という名前のカテゴリと SubCat という名前のサブカテゴリに基づいています。  
  
-   2 つの入れ子になった列グループ。Year という名前の年と Qtr という名前の四半期に基づいています。  
  
-   Totals というラベルが付いた 1 つの静的な合計列。  
  
-   1 つの隣接する列グループ。Territory という名前の販売区域に基づいています。  
  
 販売区域グループの列ヘッダーは、表示目的で 2 つのセルに分割されています。 最初のセルには販売区域の名前と合計、2 番目のセルには各販売区域のすべての売上に対して貢献した割合を計算したプレースホルダー テキストが表示されます。  
  
 ![rs_BasicTableSumCellScope](../../reporting-services/report-design/media/rs-basictablesumcellscope.gif "rs_BasicTableSumCellScope")  
  
 DataSet1 というデータセットと Tablix1 というテーブルがあるとします。 次の表は、セルのラベル、既定のスコープ、および例を示しています。 プレースホルダー テキストの値は式の構文に示されます。  
  
|セル|既定のスコープ|プレースホルダーのラベル|テキストまたはプレースホルダーの値|  
|----------|-------------------|------------------------|--------------------------------|  
|C01|Tablix1|[Sum(Qty)]|集計とスコープ<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C02|外部列グループ "Year"|[Year]<br /><br /> ([YearQty])|`=Fields!Year.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C03|Tablix1|[Sum(Qty)]|Totals<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C04|ピア列グループ "Territory"|([Total])|Territory<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C05|内部グループ "Qtr"|[Qtr]<br /><br /> ([QtrQty])|Q<br /><br /> `=Fields!Qtr.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C06|ピア列グループ "Territory"|[Territory]<br /><br /> ([Tty])<br /><br /> [Pct]|`=Fields!Territory.Value`<br /><br /> `=Sum(Fields!Qty.Value)`<br /><br /> `=FormatPercent(Sum(Fields!Qty.Value,"Territory")/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C07|外部行グループ "Cat"|[Cat]<br /><br /> [Sum(Qty)]|`=Fields!Cat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C08|C07 と同じ|||  
|C09|外部行グループ "Cat" と内部列グループ "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C10|C07 と同じ|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Tablix1"),0) & " of " & Sum(Fields!Qty.Value,"Tablix1")`|  
|C11|外部行グループ "Cat" と列グループ "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Territory"),0) & " of " & Sum(Fields!Qty.Value,"Territory")`|  
|C12|内部行グループ "Subcat"|[Subcat]<br /><br /> [Sum(Qty)]|`=Fields!SubCat.Value`<br /><br /> `=Sum(Fields!Qty.Value)`|  
|C13|内部行グループ "Subcat" と内部列グループ "Qtr"|[Sum(Qty)]|`=Sum(Fields!Qty.Value)`|  
|C14|内部行グループ "Subcat"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Sum(Fields!Qty.Value)/Sum(Fields!Qty.Value,"Cat"),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
|C15|内部行グループ "Subcat" と列グループ "Territory"|<\<Expr>>|`=Sum(Fields!Qty.Value) & ": " & FormatPercent(Code.CalcPercentage(Sum(Fields!Qty.Value),Sum(Fields!Qty.Value,"Cat")),0) & " of " & Sum(Fields!Qty.Value,"Cat")`|  
  
 Tablix データ領域にある視覚的な合図の解釈に関する詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。 Tablix データ領域に関する詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。 式や集計に関する詳細については、「[レポートでの式の使用 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)」および「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
  
##  <a name="Sparklines"></a> スパークラインのスケールの同期  
 テーブルまたはマトリックス内で入れ子になっているスパークライン グラフの横軸の値を時間全体で比較するには、カテゴリ グループの値を同期します。 この処理を軸を揃えるといいます。 軸を揃えるオプションを選択すると、レポートには軸の最小値と最大値が自動的に設定され、各カテゴリに存在しない集計値のプレースホルダーが含まれます。 これにより、スパークライン内の値は各カテゴリ間で揃えられ、集計データの各行の値を比較できます。 このオプションを選択すると、 *ドメイン スコープ*に対する式の評価のスコープも変更されます。 入れ子になったグラフのドメイン スコープを設定すると、凡例にある各カテゴリの色の割り当ても間接的に制御されます。  
  
 たとえば、毎週の傾向を示すスパークラインに、3 か月間の売上データと 12 か月間の売上データを持つ都市が 1 つずつあるとします。 スケールを同期しないと、最初の都市のスパークラインには 3 つのバーしか表示されず、これらのバーの幅は非常に広くなり、2 番目の都市の 12 か月分のバーと同じスペースをとることになります。  
  
 詳細については、「[テーブル内のグラフまたはマトリックスでのデータの整列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="Indicators"></a> インジケーターの範囲の同期  
 インジケーターのセットに使用するデータ値を指定するには、スコープを指定する必要があります。 インジケーターを含むデータ領域のレイアウトに応じて、スコープまたはコンテナー スコープを指定します。 たとえば、売上カテゴリに関連付けられたグループ ヘッダー行で、矢印セット (上、下、横向き) はしきい値に対して相対的な売上値を示すことができます。 コンテナー スコープは、インジケーターを含んでいるテーブルまたはマトリックスの名前です。  
  
 詳細については、「 [同期スコープの設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/set-synchronization-scope-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="Page"></a> ページ ヘッダーまたはページ フッターのスコープの指定  
 レポートのページごとに異なるデータを表示するには、表示されたページに必ず含まれるレポート アイテムに式を追加します。 レポートは表示されるとき複数のページに分割されるため、ページに存在するアイテムを判別できるのは、表示している間だけです。 たとえば、詳細行にあるセルは、ページ上に多数のインスタンスを持つテキスト ボックスを含んでいます。  
  
 このため、ReportItems というグローバル コレクションが用意されています。 これは、現在のページ上のテキスト ボックスのセットです。  
  
 詳細については、「[ページ ヘッダーとページ フッター &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)」および「[ReportItems コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md)」を参照してください。  
  
  
##  <a name="Toggles"></a> ドリルダウンと条件付き表示の切り替えアイテムの指定  
 切り替えは、正符号と負符号の画像で表され、テキスト ボックスに追加したり、クリックして他のレポート アイテムを表示または非表示にすることができます。 ほとんどのレポート アイテムのプロパティの **[表示]** ページでは、切り替えを追加するレポート アイテムを指定できます。 切り替えアイテムは、表示または非表示にするアイテムよりも上位のコンテナー スコープ内にある必要があります。  
  
 Tablix データ領域で、テキスト ボックスをクリックしてテーブルを展開し詳細なデータを表示するドリルダウン効果を作成するには、グループの **[表示]** プロパティを設定し、コンテナー グループに関連付けられたグループ ヘッダー内のテキスト ボックスを切り替えとして選択する必要があります。  
  
 詳細については、「 [アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="Sort"></a> 並べ替え順序を同期する並べ替え式の指定  
 対話的な並べ替えボタンをテーブル列に追加すると、共通のコンテナー スコープを持つ複数のアイテムの並べ替えを同期できます。 たとえば、並べ替えボタンをマトリックス内の列ヘッダーに追加し、コンテナー スコープをマトリックスにバインドされたデータセットの名前として指定します。 並べ替えボタンをクリックすると、マトリックス行が並べ替えられるだけでなく、同じデータセットにバインドされたグラフのグラフ系列グループも並べ替えられます。 この方法により、そのデータセットに依存するすべてのデータ領域を同期して、同じ並べ替え順で表示することができます。  
  
 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="Nulls"></a> セルの NULL 値または 0 の非表示  
 多くのレポートでは、グループにスコープが設定された計算でゼロ (0) または NULL 値を含むセルが多数生成される場合があります。 レポートを見やすくするためには、集計値が 0 の場合に空白を返す式を追加します。 詳細については、「 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)のように、使用するデータセットの名前を指定する必要があります。  
  
  
## <a name="see-also"></a>参照  
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [テキストとプレースホルダーの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
