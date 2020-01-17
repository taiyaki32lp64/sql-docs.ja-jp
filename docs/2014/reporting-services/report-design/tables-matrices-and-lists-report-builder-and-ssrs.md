---
title: テーブル、マトリックス、および一覧 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.tablix.visibility.f1
- sql12.rtp.rptdesigner.groupproperties.advanced.f1
- "10045"
- sql12.rtp.rptdesigner.groupproperties.filters.f1
- "10039"
- "10104"
- sql12.rtp.rptdesigner.tablixgroup.f1
- sql12.rtp.rptdesigner.tablix.general.f1
- "10047"
- "10044"
- "10046"
- sql12.rtp.rptdesigner.groupproperties.visibility.f1
- "10101"
- sql12.rtp.rptdesigner.groupproperties.sort.f1
- sql12.rtp.rptdesigner.groupproperties.variables.f1
- sql12.rtp.rptdesigner.groupproperties.general.f1
- "10042"
- sql12.rtp.rptdesigner.tablix.sort.f1
- "10041"
- sql12.rtp.rptdesigner.groupproperties.pagebreaks.f1
- "10102"
- "10103"
- "10043"
- sql12.rtp.rptdesigner.tablix.filter.f1
ms.assetid: 9dcf3fc8-bf9c-4a14-a03d-e78254aa4098
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff294adb9108156e08c1d0053d301c0f4cafb0fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104749"
---
# <a name="tables-matrices-and-lists-report-builder-and-ssrs"></a>テーブル、マトリックス、および一覧 (レポート ビルダーおよび SSRS)
  テーブル、マトリックス、および一覧は、行と列で構成されたセルにレポート データを表示するデータ領域です。 セルには通常、テキスト、日付、数字などのテキスト データが含まれていますが、ゲージ、グラフ、または画像などのレポート アイテムも含めることができます。 テーブル、マトリックス、および一覧をまとめて Tablix データ領域と呼ぶことがあります。  
  
 テーブル、マトリックス、および一覧のテンプレートは、セルにデータを表示できる柔軟なグリッドである Tablix データ領域に基づいて構築されます。 テーブルおよびマトリックスのテンプレートでは、セルは行と列で構成されます。 テンプレートは基になる汎用の Tablix データ領域の一種であるため、レポートの作成時に、テンプレート形式を組み合わせてデータを表示し、テーブル、マトリックス、または一覧を変更して別のデータ領域の機能を含めることができます。 たとえば、追加したテーブルがニーズに合わない場合は、列グループを追加してテーブルをマトリックスに変更できます。  
  
 テーブルとマトリックスのデータ領域では、入れ子になったテーブル、マトリックス、一覧、グラフ、およびゲージを含めることで、データの複雑なリレーションシップを表示できます。 テーブルとマトリックスには表形式のレイアウトがあり、各データは 1 つのデータ ソースに基づいて構築された 1 つのデータセットから取得されます。 テーブルとマトリックスの重要な違いとして、テーブルに含めることができるのは行グループのみであるのに対し、マトリックスには行グループと列グループを含めることができます。  
  
 一覧はこれとは多少異なります。 一覧は、自由形式のレイアウトをサポートし、異なるデータセットのデータを使用した複数のピア テーブルまたはマトリックスを含むことができます。 一覧は、請求書などのフォームにも使用できます。  
  
 次の図は、テーブル、マトリックス、または一覧を含んだ簡単なレポートを示しています。  
  
 ![RS_TableMatrixList](../media/rs-tablematrixlist.gif "RS_TableMatrixList")  
  
 テーブル、マトリックス、および一覧をすぐに使用するには、「[チュートリアル:基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../tutorial-creating-a-basic-table-report-report-builder.md)」、「[チュートリアル:マトリックス レポートの作成 &#40;レポート ビルダー&#41;](../tutorial-creating-a-matrix-report-report-builder.md)」、「[チュートリアル:自由形式のレポートの作成 &#40;レポート ビルダー&#41;](../tutorial-creating-a-free-form-report-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  テーブル、マトリックス、および一覧は、レポート パーツとしてレポートとは別にパブリッシュできます。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Table"></a> Table  
 テーブルを使用すると詳細データの表示やデータの行グループへの編成、またはその両方が可能です。 テーブル テンプレートには、テーブル ヘッダー行およびデータの詳細行と共に、3 つの列が含まれます。 次の図では、デザイン画面で初期のテーブル テンプレートが選択されています。  
  
 ![デザイン画面上のテーブル テンプレート、選択](../media/rs-tabletemplatenewselected.gif "デザイン画面上のテーブル テンプレート、選択")  
  
 データは、1 つのフィールドまたは複数のフィールドでグループ化することも、独自の式を記述してグループ化することもできます。 入れ子になったグループや独立した隣接するグループの作成、グループ化されたデータの集計値の表示、グループへの合計の追加などを行うことができます。 たとえば、テーブルに [Category] という名前の行グループがある場合は、各グループの小計とレポートの総計を追加できます。 テーブルを見やすくし、強調するデータを強調表示するには、セルを結合し、書式をデータとテーブルの見出しに適用します。  
  
 最初は詳細データまたはグループ化されたデータを非表示にして、ユーザーが表示するデータを対話的に選択できるドリルダウンの切り替えを含めることもできます。  
  
 詳細については、「[テーブル &#40;レポート ビルダーおよび SSRS& #41;](tables-report-builder-and-ssrs.md)」を参照してください。  
  

  
##  <a name="Matrix"></a> マトリックス  
 PivotTable またはクロス集計と同様に、マトリックスは、行と列にグループ化した集計データ サマリの表示に使用します。 グループの行と列の数は、各行グループおよび列グループに含まれている一意の値の数によって決定します。 次の図では、デザイン画面で初期のマトリックス テンプレートが選択されています。  
  
 ![ツールボックスから追加された新しいマトリックス、選択](../media/rs-matrixtemplatenewselected.gif "ツールボックスから追加された新しいマトリックス、選択")  
  
 データは、複数のフィールドまたは式によって、行グループと列グループにグループ化できます。 実行時にレポート データとデータ領域が組み合わされると、列グループに列、行グループに行がそれぞれ追加され、マトリックスはページ上で縦横に拡大されます。 マトリックス セルには、そのセルが所属する行グループと列グループの交差部分にスコープを設定した集計値が表示されます。 たとえば、マトリックスに行グループ (Category) と売上の合計を表示する 2 つの列グループ (Territory および Year) がある場合、レポートには Category グループ内の各値に対して売上の合計を含む 2 つのセルが表示されます。 セルのスコープは 2 つの交差部分です。つまり、Category および Territory と Category および Year です。 マトリックスには、入れ子になったグループと隣接するグループを含めることができます。 入れ子になったグループには親子リレーションシップ、隣接するグループにはピア リレーションシップがあります。 マトリックス内には、入れ子になった行および列グループの任意のレベルの小計や、すべてのレベルの小計が追加できます。  
  
 マトリックス データを読みやすくし、強調するデータを強調表示するには、セルを結合するか、水平方向および垂直方向に分割し、書式をデータとグループの見出しに適用します。  
  
 ドリルダウン トグルを含めて、最初は詳細データを非表示にすることもできます。ユーザーは、トグルをクリックすることにより、表示するデータの量を調整できます。  
  
 詳細については、次を参照してください。[マトリックス&#40;レポート ビルダーおよび SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)します。  
  

  
##  <a name="List"></a> 一覧  
 一覧は、自由形式のレイアウトの作成に使用します。 グリッド レイアウトのみに制限されず、フィールドは一覧内に自由に配置できます。 一覧は、多数のデータセット フィールドを表示するフォームの設計に使用したり、グループ化されたデータの場合は、複数のデータ領域を並列に表示するコンテナーとして使用したりすることができます。 たとえば、一覧にグループを定義し、テーブル、グラフ、およびイメージを追加し、従業員や患者のレコードを表示する際と同様に、各グループ値についてテーブルまたはグラフィック形式で値を表示することができます。  
  
 ![ツールボックスから追加された新しい一覧、選択](../media/rs-listtemplatenewselected.gif "ツールボックスから追加された新しい一覧、選択")  
  
 詳細については、次を参照してください。[一覧&#40;レポート ビルダーおよび SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)します。  
  

  
##  <a name="PreparingData"></a> データの準備  
 テーブル、マトリックス、および一覧のデータ領域には、データセットのデータが表示されます。 データセットのデータを取得するクエリのデータを準備することも、テーブル、マトリックス、または一覧でプロパティを設定してデータを準備することもできます。  
  
 レポート データセットのデータを取得するのに使用する、 [!INCLUDE[tsql](../../includes/tsql-md.md)]などのクエリ言語でデータを準備するには、データのサブセットのみを含むようにフィルターを適用し、レポートが読みやすくなるように NULL 値や空白を定数に置き換え、データの並べ替えやグループ化を行います。  
  
 レポートのテーブル、マトリックス、または一覧のデータ領域でデータを準備する場合は、データ領域またはデータ領域内のセルのプロパティを設定します。 データのフィルター処理または並べ替えを行うには、データ領域のプロパティを設定します。 たとえば、データを並べ替えるには、並べ替える列と並べ替えの方向を指定します。 フィールドに別の値を表示する場合は、フィールドを表示するセル テキストの値を設定します。 たとえば、フィールドが空または NULL である場合に Blank と表示するには、式を使用して値を設定します。  
  
 詳細については、「[Tablix データ領域に表示するデータの準備 &#40;レポート ビルダーおよび SSRS&#41;](preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs.md)」を参照してください。  
  

  
##  <a name="BuildingConfiguringTableMatrixList"></a> テーブル、マトリックス、または一覧の構築と構成  
 テーブルまたはマトリックスをレポートに追加する場合は、テーブルまたはマトリックス ウィザードを使用するか、レポート ビルダーおよびレポート デザイナーに用意されたテンプレートから手動で構築できます。 一覧は、一覧のテンプレートから手動で構築します。  
  
 ウィザードを使用すると、手順に従ってテーブルやマトリックスを簡単に構築および構成できます。 ウィザードを完了した後、または Tablix データ領域を最初から構築する場合、さらに詳細に構成および調整できます。 データ領域の右クリック メニューで表示されるダイアログ ボックスで、改ページ、ヘッダーとフッターの繰り返しと表示設定、表示オプション、フィルター、並べ替えなどの一般的に使用するプロパティを簡単に設定できます。 ただし、Tablix データ領域にはレポート ビルダーのプロパティ ペインでのみ設定できる追加のプロパティも多数含まれています。 たとえば、テーブル、マトリックス、または一覧のデータセットが空の場合にメッセージを表示するには、プロパティ ペインの NoRowsMessage Tablix プロパティでメッセージ テキストを指定します。  
  

  
##  <a name="ChangingBetweenTablixTemplates"></a> Tablix テンプレート間の切り替え  
 最初に選択した Tablix テンプレートによる制限はありません。 グループ、合計、ラベルなどの追加に伴い、Tablix デザインを変更できます。 たとえば、テーブルから開始し、その後詳細行を削除したり、列グループを追加したりする場合があります。 詳細については、「[Tablix データ領域の柔軟性について &#40;レポート ビルダーおよび SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)」を参照してください。  
  
 Tablix 機能を追加することで、テーブル、マトリックス、または一覧の改良を続けることができます。 Tablix 機能には、詳細データやグループ化されたデータの集計を行および列に表示する機能が含まれます。 入れ子構造のグループ、独立した隣接するグループ、または再帰的なグループを作成できます。 グループ データのフィルター処理や並べ替えが可能なほか、複数のグループ式をグループ定義に含めることにより、グループを簡単に組み合わせることができます。  
  
 さらに、グループの合計、またはデータ領域の総合計を追加することもできます。 行や列を非表示にしてレポートを簡潔化し、ドリルダウン レポートのように非表示のデータ表示をユーザーが切り替えることができるようにすることができます。 詳細については、「 [レポート ページでの Tablix データ領域の表示の制御 &#40;レポート ビルダーおよび SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)」を参照してください。  
  

  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 このセクションでは、レポートでテーブル、マトリックス、および一覧を使用する手順について説明しているトピックの一覧を紹介します。具体的には、行と列のデータの表示、列の追加と削除、セルの結合、および行および列グループの小計を含める方法を示します。  
  
-   [詳細グループの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md)  
  
-   [グループまたは Tablix データ領域への合計の追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
-   [セル内のアイテムの変更 &#40;レポート ビルダーおよび SSRS&#41;](change-an-item-within-a-cell-report-builder-and-ssrs.md)  
  
-   [行の高さまたは列の幅の変更 &#40;レポート ビルダーおよび SSRS&#41;](change-row-height-or-column-width-report-builder-and-ssrs.md)  
  
-   [列の挿入または削除 &#40;レポート ビルダーおよび SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md)  
  
-   [行の挿入または削除 &#40;レポート ビルダーおよび SSRS&#41;](insert-or-delete-a-row-report-builder-and-ssrs.md)  
  
-   [データ領域内のセルの結合 &#40;レポート ビルダーおよび SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
-   [データ領域でのグループの追加または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [グループ単位でのヘッダーとフッターの表示 &#40;レポート ビルダーおよび SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
-   [階段状レポートの作成 &#40;レポート ビルダーおよび SSRS&#41;](create-a-stepped-report-report-builder-and-ssrs.md)  
  
-   [テーブル、マトリックス、または一覧の追加、移動、または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)  
  

  
##  <a name="InThisSection"></a> トピックの内容  
 次の各トピックでは、Tablix データ領域の使用に関する追加情報について説明します。  
  
 [Tablix データ領域 &#40;レポート ビルダーおよび SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)  
 Tablix データ、詳細データ、およびグループ化されたデータの領域、列グループおよび行グループ、静的および動的な行と列など、Tablix データ領域に関連する主な概念について説明します。  
  
 [Tablix データ領域へのデータの追加 &#40;レポート ビルダーおよび SSRS&#41;](adding-data-to-a-tablix-data-region-report-builder-and-ssrs.md)  
 Tablix データ領域に詳細データ、グループ化されたデータ、小計と総計、およびラベルを追加する方法について詳しく説明します。  
  
 [レポート ページでの Tablix データ領域の表示の制御 &#40;レポート ビルダーおよび SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)  
 レポートに表示したときの Tablix データ領域の表示方法を変更するための Tablix データ領域のプロパティについて説明します。  
  
 [行見出しと列見出しの制御 &#40;レポート ビルダーおよび SSRS&#41;](controlling-row-and-column-headings-report-builder-and-ssrs.md)  
 テーブル、マトリックス、または一覧のデータ領域が上下または左右の複数のページにわたる場合、行見出しおよび列見出しの表示を制御する方法について説明します。  
  
 [複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
 親子間のリレーションシップがデータセットのフィールドで表されている再帰型データを表示する方法について説明します。  
  
 [グループについて &#40;レポート ビルダーおよび SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)  
 グループの概要、グループを使用する状況、およびさまざまな Tablix データ領域に使用できるグループについて説明します。  
  

  
## <a name="see-also"></a>参照  
 [データセット フィルター、データ領域フィルター、およびグループ フィルターの追加 (レポート ビルダーおよび SSRS)](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](nested-data-regions-report-builder-and-ssrs.md)   
 [同じデータセットへの複数のデータ領域のリンク &#40;レポート ビルダーおよび SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-parameters-report-builder-and-report-designer.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [ゲージ &#40;レポート ビルダーおよび SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
