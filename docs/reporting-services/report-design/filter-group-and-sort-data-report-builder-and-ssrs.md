---
title: データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.categorygroupproperties.general.f1
- "10403"
- sql13.rtp.rptdesigner.categorygroupproperties.sorting.f1
- sql13.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10402"
- "10410"
- sql13.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0012f01fead8d6890f8e593f4991cbb0252e3dd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576529"
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)
  レポートでは、式を使用してレポート データの制御、整理、および並べ替えを行うことができます。 既定では、データセットを作成してレポート レイアウトをデザインすると、データセット フィールドやパラメーターなど、レポート データ ペインに表示されるアイテムに基づいて、レポート アイテムのプロパティが式に自動的に設定されます。 グループまたはグループ内の行の並べ替え順序をユーザーが対話的に変更できるように、テーブルまたはマトリックスのセルに対話的な並べ替えボタンを追加することもできます。  
  
-   **フィルター式** フィルター式は、指定された比較に基づいてデータを含めるか除外するかをテストする式です。 フィルターは、データがデータ接続から取得された後にレポート内のデータに適用されます。 フィルターは自由に組み合わせて、レポート サーバーの共有データセット定義、レポート内の共有データセット インスタンスまたは埋め込みデータセット、テーブルやグラフなどのデータ領域、テーブルの行グループやグラフのカテゴリ グループなどのデータ領域グループに追加することができます。  
  
-   **グループ式** グループ式は、データセット フィールドまたはその他の値に基づいてデータをまとめる式です。 レポート レイアウトを作成すると自動的に作成されます。 グループ式はレポート プロセッサによって、データにフィルターが適用された後に、レポート データとデータ領域が組み合わされると評価されます。 グループ式は作成された後にカスタマイズすることができます。  
  
-   **並べ替え式** 並べ替え式は、データ領域でのデータの表示順序を制御する式です。 レポート レイアウトを作成すると自動的に作成されます。 既定では、グループの並べ替え式は、グループ式と同じ値に設定されます。 並べ替え式は作成された後にカスタマイズすることができます。  
  
-   **対話的な並べ替え** ユーザーが列の並べ替え順序を切り替えられるようにするには、テーブルまたはマトリックスの列ヘッダーまたはグループ ヘッダーのセルに対話的な並べ替えボタンを追加します。  
  
 フィルター式、グループ式、または並べ替え式をユーザーがカスタマイズしやすくするために、式を変更してレポート パラメーターへの参照を追加することができます。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)にあります。  
  
 詳細と例については、次のトピックを参照してください。  
  
-   [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
-   [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [レポート ビルダー チュートリアル](../../reporting-services/report-builder-tutorials.md)  
  
-   [Reporting Services チュートリアル (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
-   [レポート サンプル (レポート ビルダーおよび SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> レポートのデータのフィルター処理  
 フィルターは、データ接続から取得されたレポート データを制御するためのレポートのパーツです。 外部データ ソースからデータを取得する前にデータセット クエリを変更してデータをフィルター処理できない場合に、フィルターを使用します。  
  
 可能であれば、レポートに表示する必要があるデータだけを返すデータセット クエリを作成します。 取得および処理する必要があるデータ量を少なくすると、レポートのパフォーマンスの向上に役立ちます。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。  
  
 データが外部データ ソースから取得された後、データセット、データ領域、およびデータ領域グループ (詳細グループを含む) にフィルターを追加できます。 実行時には、フィルターが最初にデータセットに適用され、次にデータ領域に適用された後、グループに (グループ階層の上から順に) 適用されます。 テーブル、マトリックス、または一覧では、行グループ、列グループ、および隣接するグループに対するフィルターが別々に適用されます。 グラフでは、カテゴリ グループと系列グループに対するフィルターが別々に適用されます。 詳細については、「 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)」を参照してください。  
  
 フィルターには、それぞれ *フィルター式*を指定します。 フィルター式には、フィルターの対象となるデータを識別するデータセット フィールドまたは式、演算子、および比較対象の値が含まれます。 それらのデータ値のうちフィルター条件に一致するものだけが、アイテムを処理する際の対象になります。  
  
 レポートのデータをユーザーが制御しやすくするために、フィルター式にパラメーターを含めることができます。 詳細については、「[Parameters コレクションの参照 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)」を参照してください。  
  
 ユーザーごとに表示をカスタマイズするには、組み込みのフィールド UserID への参照をフィルターに含めます。 詳細については、「[組み込み Globals および Users 参照 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)」をご覧ください。  
  
  
##  <a name="Grouping"></a> レポートのデータのグループ化  
 グループを使用すると、レポートのデータを整理して表示したり、集計値を計算したりすることができます。 グループを定義して使用する方法を理解することは、簡潔なレポートの作成に役立ちます。  
  
 グループ式は、次の操作を実行したときに自動的に作成されます。  
  
-   テーブル、マトリックス、グラフのウィザードでデータセット フィールドを配置する、またはマップ ウィザードで対応フィールドを配置する。  
  
-   テーブル、マトリックス、または一覧のグループ化ペインで [行グループ] 領域または [列グループ] 領域にフィールドを追加する。  
  
-   グラフのグラフ データ ペインで [カテゴリ グループ] 領域または [系列グループ] 領域にフィールドを追加する。  
  
-   マップの [レイヤー データ] コンテキスト メニュー項目で、マップ要素を分析データに対応付けるフィールドを指定する。  
  
 グループはレポート定義の一部です。 グループにはそれぞれ名前が割り当てられ、 既定では、そのグループが基づいているデータセット フィールドになります。  
  
 テーブルまたはマトリックスのデータ領域では、複数の行グループおよび列グループを作成できます。 入れ子になったグループ、隣接するグループ、および再帰型階層のグループ (組織図など) を編成して、階層構造でデータを表示できます。  
  
 式のスコープはグループ名で識別されます。 集計を計算するスコープ、データを階層にまとめてドリルダウン レポートの親ノードから子ノードの表示を切り替えるスコープ、複数のデータ領域で同じデータの異なるビューを表示するスコープ、およびテーブル、マトリックス、グラフ、ゲージ、またはマップでサマリ データを視覚化するスコープとして、グループの名前を指定できます。 詳細については、「 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)を表しています。  
  
 複数のデータセット フィールドに基づきグループ化するには、各フィールドをグループ式のセットに追加します。 さらに [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]で独自のグループ式を記述することもできます。 たとえば、値の範囲でグループ化したり、レポート パラメーターを使用してデータ領域のデータのグループ化の方法を選択できるようにしたりすることができます。 詳細については、「 [グループ式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)」を参照してください。  
  
 レポート表示では、各グループまたは各グループ インスタンスの前後に改ページを追加して、各ページのデータ量を減らし、レポート表示のパフォーマンスを管理できます。 詳細については、「[改ページの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)」を参照してください。  
  
 データ領域グループを作成することは、レポートのデータを整理する 1 つの方法です。 データを整理する方法は他にもあり、そのそれぞれに利点があります。 詳細については、「 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)」を参照してください。  
  
### <a name="defining-group-variables"></a>グループ変数の定義  
 グループを定義する場合、スコープがグループであり、入れ子になったグループからアクセスできる式で使用するグループ変数を作成できます。 グループ変数は、グループ インスタンスごとに 1 回計算され、子グループの式からアクセスできます。 たとえば、地域とサブ地域でグループ化されたデータの場合、各地域の税額を計算し、その税額をサブ地域グループの計算に使用できます。  
  
 詳細については、「 [レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md) 」および「 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
### <a name="groups-and-scope-in-data-regions"></a>グループとデータ領域のスコープ  
 同じデータセットのデータを複数の形式で表示するには、各データ領域に同じグループ式を指定します。 たとえば、分類されたデータを表示するときに、すべての詳細データをテーブルで示し、データセット全体に対する各カテゴリの集計を円グラフで視覚化することができます。 詳細については、「 [同じデータセットへの複数のデータ領域のリンク (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
 テーブル、マトリックス、または一覧のセルでデータ領域を入れ子にすると、データのスコープは自動的にそのセルの最も内側のグループ メンバーシップになります。 たとえば、行グループと列グループの両方に存在するセルにグラフを追加するとします。 そのグラフで使用可能なデータは、実行時に最も内側の行グループ インスタンスと最も内側の列グループ インスタンスにスコープが設定されます。 詳細については、「 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
  
##  <a name="Sorting"></a> レポートのデータの並べ替え  
 レポートのデータの並べ替え順序を制御するには、データセット クエリのデータを並べ替えるか、データ領域またはグループの並べ替え式を定義します。 対話的な並べ替えボタンをテーブルおよびマトリックスに追加して、ユーザーが行の並べ替え順序を変更できるようにすることもできます。  
  
 同じレポート内で、3 種類すべての並べ替えを組み合わせて使用できます。 既定では、並べ替え順序は、データがデータセット クエリから返された順序によって決まります。 並べ替え式は、データ領域およびデータ領域グループで適用されます。 対話的な並べ替えは、並べ替え式の後に適用されます。  
  
 集計関数を含む式の結果に並べ替え順序が影響することはほとんどありません。 戻り値が並べ替え順序の影響を受ける集計関数には、First、Last、および Previous があります。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
### <a name="sorting-data-in-a-dataset-query"></a>データセット クエリのデータの並べ替え  
 データセット クエリで並べ替え順序を指定し、レポートのデータが取得される前にデータを事前に並べ替えます。 クエリのデータを並べ替えることによって、レポート プロセッサではなく、データ ソースによって並べ替えが実行されます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースの種類の場合、ORDER BY 句をデータセット クエリに追加できます。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリは、 `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`のように、Sales 列および Region 列を Sales を基準にテーブル SalesOrders から降順で並べ替えます。  
  
> [!NOTE]  
>  すべてのデータ ソースでクエリの並べ替え順序を指定できるわけではありません。  
  
### <a name="sorting-data-with-sort-expressions"></a>並べ替え式を使用したデータの並べ替え  
 レポートのデータがデータ ソースから取得された後にこのデータを並べ替えるには、Tablix データ領域または詳細グループを含むグループで並べ替え式を設定します。 次に、並べ替え式を設定した場合の効果をアイテムごとに説明します。  
  
-   **Tablix データ領域。** データセット フィルターおよびデータ領域フィルターが実行時に適用された後、テーブル、マトリックス、または一覧のデータ領域で並べ替え式を設定して、データ領域のデータの並べ替え順序を制御します。  
  
-   **Tablix データ領域グループ。** 詳細グループを含む各グループの並べ替え式を設定し、グループ インスタンスの並べ替え順序を制御します。 たとえば、詳細グループの場合、詳細行の順序を制御します。 子グループの場合、親グループ内の子グループのグループ インスタンスの順序を制御します。 既定では、グループを作成する際、並べ替え式はグループ式および昇順に設定されます。  
  
     詳細グループが 1 つしかない場合は、データ領域または詳細グループでクエリの並べ替え式の効果が同じになるように定義します。  
  
-   **グラフ データ領域。** カテゴリおよび系列グループの並べ替え式を設定して、データ ポイントの並べ替え順序を制御します。 既定では、データ ポイントの順序とグラフの凡例の色の順序は同じです。 詳細については、「 [グラフの系列の色の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)をクリックします。  
  
-   **マップ レポート アイテム。** 通常、マップ要素に表示するデータはマップによってグループ化されるため、マップのデータ領域のデータを並べ替える必要はありません。  
  
-   **ゲージのデータ領域。** 通常、ゲージには範囲を基準とした単一の値が表示されるため、ゲージのデータ領域のデータを並べ替える必要はありません。 ゲージのデータを並べ替える必要がある場合は、最初にグループを定義し、次にグループの並べ替え式を設定します。  
  
#### <a name="sorting-by-a-different-value"></a>別の値による並べ替え  
 データ領域の行をフィールド値以外の値で並べ替えることもできます。 たとえば、Size というフィールドに、各サイズに対応するテキスト値 (S、M、L、および XL) が含まれているとします。 既定では、Size に基づく行グループの並べ替え式も [Size] になります。 データの並べ替え方法を制御するには、データセット クエリに並べ替え順序を定義するフィールドを追加します。  
  
 また、サイズとその順序を示す値だけを含むデータセットを定義し、 Lookup 関数を使用して並べ替え順序の値を取得するように並べ替え式を変更することもできます。  
  
 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリで、Sizes という名前のデータセットを定義するとします。 このクエリでは、CASE ステートメントを使用して、Size の各値に対して SizeSortOrder という並べ替え順序の値を定義しています。  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 `[Size]`に基づく行グループがあるテーブルで、Lookup 関数を使用してサイズの値に対応する数値フィールドを検索するように、グループの並べ替え式を変更できます。 式は次のようになります。  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 詳細については、「[データ領域内のデータの並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)」および「[Lookup 関数 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-lookup-function.md)」を参照してください。  
  
###  <a name="Interactive"></a> ユーザー向けの対話的な並べ替えの追加  
 テーブルまたはマトリックスでユーザーがレポート データの並べ替え順序を変更できるようにするには、列ヘッダーまたはグループ ヘッダーに対話的な並べ替えボタンを追加します。 ユーザーはそのボタンをクリックして、並べ替え順序を切り替えることができます。 対話的な並べ替えは、ユーザーとの対話が可能な HTML などの表示形式でサポートされています。  
  
 対話的な並べ替えボタンは、Tablix データ領域のセルのテキスト ボックスに追加します。 既定では、すべてのセルにテキスト ボックスが含まれています。 テキスト ボックス プロパティで、並べ替えるテーブルまたはマトリックスのデータ領域の部分 (親グループ値、子グループ値、または詳細行)、並べ替え基準、およびピア関係を持つ他のレポート アイテムに並べ替え式を適用するかどうかを指定します。 たとえば、同じデータセットのビューを表示するテーブルとグラフが四角形内に含まれている場合は、このテーブルとグラフはピア データ領域です。 ユーザーがテーブルの並べ替え順序を切り替えると、グラフの並べ替え順序も切り替わります。 詳細については、「[対話的な並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 [レポートのスクロール時にヘッダーを表示したままにする (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [グループ単位でのヘッダーとフッターの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [テーブルまたはマトリックスへの対話的な並べ替えの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [データ領域にデータがないことを示すメッセージの設定 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [再帰型階層グループの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [グループ単位でのヘッダーとフッターの表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [グラフでのグループの追加または削除 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [グループまたは Tablix データ領域への合計の追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> トピックの内容  
 [グループ式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
  
 [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
  
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> 関連項目  
 [グループについて (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
  
 [複数の再帰型階層グループの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [レポート変数コレクションとグループ変数コレクションの参照 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [グラフ上で複数のデータ範囲を持つ系列の表示 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [同じデータセットへの複数のデータ領域のリンク (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>参照  
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [マップ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [ゲージ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)   
 [インジケーター (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
