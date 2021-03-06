---
title: グループについて (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10056"
- "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cbce55f34f123c2e615b5ace6c1a1b77b3a494e0
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287480"
---
# <a name="understanding-groups-report-builder-and-ssrs"></a>グループについて (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、グループは、データ領域にバインドされたレポート データセットの名前付きセットです。 グループは基本的に、レポート データセットのビューを整理します。 データ領域のグループはすべて、同じレポート データセットの異なるビューを指定します。  
  
 グループとはどのようなものかを視覚的に理解するために、[プレビュー] で Tablix データ領域を示した次の図を参照してください。 この図では、行グループで製品タイプ別にデータセットが分類され、列グループで地理的領域と年度別にデータセットが分類されています。  
  
 ![Tablix data region areas](../../reporting-services/report-design/media/rs-tablixareas.gif "Tablix data region areas")  
  
 次のセクションでは、グループのさまざまな側面について説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="what-makes-a-group"></a>グループの構成要素  
 グループには、ユーザーが指定した名前とグループ式のセットがあります。 グループ式のセットは、単一のデータセット フィールド参照である場合も、複数の式の組み合わせである場合もあります。 グループ式は実行時に組み合わされ、グループに複数の式がある場合は、グループ内のデータに適用されます。 たとえば、データ領域のデータを整理するデータ フィールドを使用するグループがあるとします。 実行時に、データはまず日付で整理され、日付ごとに他のデータセット値の合計と共に表示されます。  
  
## <a name="when-do-i-create-groups"></a>グループを作成するタイミング  
 ほとんどの場合、データ領域をデザインすると、レポート ビルダーとレポート デザイナーによって自動的にグループが作成されます。 テーブル、マトリックス、または一覧の場合、グループはグループ化ペインにフィールドをドロップすると作成されます。 グラフの場合、グループはグラフのドロップゾーンにフィールドをドロップすると作成されます。 ゲージの場合は、[ゲージのプロパティ] ダイアログ ボックスを使用する必要があります。 テーブル、マトリックス、または一覧では、グループを手動で作成することもできます。 詳細については、「 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)」を参照してください。 レポートの作成時にグループを追加する方法の例については、「[チュートリアル:基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」または「[基本的なテーブル レポートの作成 &#40;SSRS チュートリアル&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)」を参照してください。  
  
## <a name="how-can-i-modify-a-group"></a>グループの変更方法  
 グループを作成したら、フィルターや並べ替え式、改ページ、グループ変数など、スコープ固有のデータを保持するためのデータ領域固有のプロパティを設定できます。 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」を参照してください。  
  
 既存のグループを変更するには、適切なグループ プロパティのダイアログ ボックスを開きます。 グループの名前は変更できます。 また、1 つのフィールドや複数のフィールド、または実行時の値を指定するレポート パラメーターに基づいてグループ式を指定することもできます。 または、人口統計データの年齢範囲を指定する式など、式のセットに基づいてグループを指定することも可能です。 詳細については、「 [グループ式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  グループの名前を変更した場合は、グループの以前の名前を参照するグループ式をすべて手動で更新する必要があります。  
  
## <a name="how-are-groups-organized"></a>グループの編成方法  
 グループの編成を理解すると、同じグループ式を指定して同じデータの別のビューを表示するデータ領域をデザインする際に役立ちます。  
  
 グループはデータ領域ごとに 1 つ以上の階層のメンバーとして内部編成されています。 グループ階層には、入れ子になっている親子グループがあり、隣接するグループがある場合もあります。  
  
 親子グループをツリー構造と考えた場合、各グループ階層はツリー構造のフォレストと見なされます。 Tablix データ領域には、行グループ階層と列グループ階層があります。 行グループ メンバーに関連付けられているデータはページの横方向に展開され、列グループ メンバーに関連付けられているデータはページの下方向に展開されます。 グループ化ペインには、デザイン画面で現在選択されている Tablix データ領域の行グループと列グループのメンバーが表示されます。 詳細については、「[グループ化ペイン &#40;レポート ビルダー&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)」を参照してください。  
  
 グラフ データ領域には、カテゴリ グループ階層と系列グループ階層があります。 カテゴリ グループ メンバーはカテゴリ軸に表示され、系列グループ メンバーは系列軸に表示されます。  
  
 ゲージ データ領域には通常必要ありませんが、ゲージで集計するデータのグループ化方法をグループで指定することができます。  
  
## <a name="what-types-of-groups-are-available-per-data-region"></a>データ領域で使用可能なグループの種類  
 グリッドとして展開されるデータ領域では、要約データを視覚的に表示するデータ領域と異なるグループがサポートされています。 そのため、Tablix データ領域、および Tablix データ領域に基づくテーブル、一覧、およびマトリックスでは、サポートされているグループが、グラフやゲージとは異なります。 次のセクションでは、データ領域の種類ごとにグループ化の種類および目的について説明します。  
  
> [!NOTE]  
>  グループにはさまざまなデータ領域があり、名前も異なりますが、グループの作成方法と使用方法の背景にある原則は同じです。 データ領域にグループを作成する際には、データ領域にリンクされているデータセットの詳細データを編成する方法を指定します。 各データ領域では、グループ化されたデータを表示するグループ構造がサポートされています。  
  
### <a name="groups-in-a-tablix-data-region-details-row-and-column-groups"></a>Tablix データ領域のグループ:詳細グループ、行グループ、列グループ  
 このトピックで前述したとおり、Tablix データ領域を使用すると、行または列ごとのグループにデータを編成できます。 ただし、Tablix データ領域には、行グループと列グループ以外にも使用可能なグループがあります。 このデータ領域で使用できるグループの種類は次のとおりです。  
  
-   **詳細グループ** : 詳細グループは、レポート ビルダーまたはレポート デザイナーがデータセットとデータ領域フィルターを適用した後のレポート データセットの全データで構成されています。 そのため、詳細グループはグループ式がない唯一のグループです。  
  
     詳細グループでは基本的に、クエリ デザイナーでデータセット クエリを実行したときに表示されるデータを指定します。 たとえば、販売注文テーブルのすべての列を取得するクエリがあるとします。 この詳細グループのデータには、テーブルのすべての列のあらゆる行の値がすべて含まれています。 この詳細グループのデータには、作成した計算データセット フィールドのすべての値も含まれます。  
  
    > [!NOTE]  
    >  詳細グループのデータには、データ ソースを計算してクエリに取得した集計であるサーバー集計も含まれます。 既定では、集計関数を使用する式がレポートに含まれていない限り、サーバー集計は、レポート ビルダーおよびレポート デザイナーで詳細データとして扱われます。 詳細については、「 [集計関数](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)」を参照してください。  
  
     既定では、テーブルまたは一覧をレポートに追加すると、レポート ビルダーおよびレポート デザイナーによって詳細グループが自動的に作成され、詳細データを表示する行が追加されます。 既定では、データセット フィールドをこの行のセルに追加すると、[Sales] などのようなフィールドの単純式が表示されます。 データ領域を表示すると、結果セットの各値について詳細行が 1 回繰り返されます。  
  
-   **行グループおよび列グループ** : データを行または列ごとのグループに整理することができます。 行グループはページの縦方向に展開されます。 列グループはページの横方向に展開されます。 グループは、たとえば最初に [Year]、次に [Quarter]、さらに [Month] というように入れ子にできます。 また、たとえば [Territory] でグループ化してから、別に [ProductCategory] でグループ化して、グループを隣接させることもできます。  
  
     データ領域のグループを作成すると、データ領域に行または列が自動的に追加され、これらの行または列を使用したグループ データが表示されます。  
  
-   **再帰型階層グループ** : 再帰型階層グループは、複数のレベルを持つ 1 つのレポート データセットのデータを編成します。 たとえば、再帰型階層グループで、[Employee] に直属する [Employee] などの組織階層を表示することができます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、この種類のレポート データのグループを作成するためのグループのプロパティと組み込み関数が提供されています。 詳細については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
 次の一覧に、各データ領域でのグループの操作方法の概要を示します。  
  
-   **テーブル** : 入れ子になった行グループ、隣接する行グループ、および再帰型階層の行グループ (組織図など) を定義します。 既定では、テーブルには詳細グループが含まれます。 選択したテーブルのグループ化ペインにデータセット フィールドをドラッグして、グループを追加します。  
  
-   **マトリックス** : 入れ子になった行グループと列グループ、および隣接する行グループと列のグループを定義します。 選択したマトリックスのグループ化ペインにデータセット フィールドをドラッグして、グループを追加します。  
  
-   **一覧** : 既定では、詳細グループがサポートされています。 一般的な使用方法として、1 レベルのグループ化がサポートされます。 選択した一覧のグループ化ペインにデータセット フィールドをドラッグして、グループを追加します。  
  
 グループを追加すると、行と列でグループのメンバーシップを反映するようにデータ領域の変更が処理されます。 グループを削除する場合、グループ定義のみを削除する方法と、グループおよび関連付けられているすべての行および列を削除する方法があります。 詳細については、「[Tablix データ領域のセル、行、および列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)」を参照してください。  
  
 詳細またはグループ データの計算で表示または使用するデータを制限するには、グループにフィルターを設定します。 詳細については、「 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)」を参照してください。  
  
 既定では、グループを作成すると、グループの並べ替え式はグループ式と同じです。 並べ替え順を変更するには、並べ替え式を変更します。 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」を参照してください。  
  
#### <a name="understanding-group-membership-for-tablix-cells"></a>Tablix セルのグループ メンバーシップについて  
 Tablix データ領域の行または列のセルは、複数の行グループおよび列グループに属することができます。 集計関数 ( `=Sum(Fields!FieldName.Value`など) を使用するセルのテキスト ボックスで式を定義すると、セルの既定のグループ スコープは所属する最も内側の子グループになります。 セルが行グループと列グループの両方に属する場合、スコープは両方とも最も内側のグループになります。 また、別のデータ セットのグループにスコープを設定した集計された小計を計算する式を記述することもできます。 たとえば、データ領域の列グループ、またはすべてのデータを基準にグループのパーセントを計算することができます ( `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`など)。 詳細については、「[Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)」と「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [グループまたは Tablix データ領域への合計の追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [データ領域内のデータの並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [ドリルダウン アクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
