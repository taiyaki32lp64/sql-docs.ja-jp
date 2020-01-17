---
title: 定義、データ ソース ビュー (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d80a58d33cd6475940afaf08de2d251c5646bec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075398"
---
# <a name="defining-a-data-source-view-analysis-services"></a>データ ソース ビューの定義 (Analysis Services)
  データ ソース ビューには、論理モデルで使用されるスキーマが含まれています。[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]多次元データベース オブジェクトつまりキューブ、ディメンション、およびマイニング構造です。 データ ソース ビューとは、XML 形式で格納されている、統合ディメンショナル モデル (UDM) とマイニング構造で使用されるこれらのスキーマ要素のメタデータ定義です。 データ ソース ビューには、次の特徴があります。  
  
-   スキーマ生成に関するトップダウン アプローチに従う場合は、基になる 1 つ以上のデータ ソースから選択したオブジェクトを表すメタデータ、または基になるリレーショナル データ ソースの生成に使用されるメタデータを格納します。  
  
-   1 つ以上のデータ ソースに対して構築できるので、複数のソースからデータを統合する多次元オブジェクトやデータ マイニング オブジェクトを定義できます。  
  
-   基になるデータ ソースに存在せず、そのデータ ソースとは別に存在するリレーションシップ、主キー、オブジェクト名、計算列、およびクエリを含めることができます。  
  
-   クライアント アプリケーションでは表示されず、クエリもできません。  
  
 DSV は、多次元モデルの必須コンポーネントです。 大部分の Analysis Services 開発者は、モデル設計の初期フェーズで DSV を作成し、基になるデータを提供する外部リレーショナル データベースに基づいて少なくとも 1 つの DSV を生成します。 ただし、後のフェーズで DSV を作成し、ディメンションとキューブを作成した後に、スキーマと基になるデータベース構造を生成することもできます。 この 2 番目のアプローチはトップダウン デザインと呼ばれることもあり、プロトタイプや分析モデルの作成によく使用されます。 このアプローチに従う場合は、スキーマ生成ウィザードを使用することによって、Analysis Services のプロジェクトまたはデータベースで定義されている OLAP オブジェクトに基づいて、基になるデータ ソース ビューとデータ ソース オブジェクトを作成します。 DSV の作成方法や作成時期にかかわりなく、すべてのモデルでは、処理開始前に少なくとも 1 つの DSV を用意する必要があります。  
  
 このトピックのセクションは次のとおりです。  
  
 [データ ソース ビューの構成](#bkmk_dsvdef)  
  
 [データ ソース ビュー ウィザードを使用した DSV の作成](#bkmk_startWiz)  
  
 [リレーションシップの名前一致条件の指定](#bkmk_NameMatch)  
  
 [セカンダリ データ ソースの追加](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> データ ソース ビューの構成  
 データ ソース ビューには、次の項目が含まれています。  
  
-   名前と説明  
  
-   次の項目を含む、スキーマ全体の範囲内の 1 つまたは複数のデータ ソースから取得したスキーマのサブセットの定義  
  
    -   テーブル名  
  
    -   列名  
  
    -   データ型  
  
    -   NULL 値の許容  
  
    -   列の長さ  
  
    -   主キー  
  
    -   主キーと外部キーのリレーションシップ  
  
-   次の項目を含む、基になるデータ ソースのスキーマの注釈  
  
    -   テーブル、ビュー、および列の表示名  
  
    -   1 つまたは複数のデータ ソースの列 (スキーマ内のテーブルとして表示) を返す名前付きクエリ  
  
    -   データ ソースの列 (テーブルまたはビュー内の列として表示) を返す名前付き計算  
  
    -   論理主キー (主キーが基になるテーブルに定義されていないか、ビューまたは名前付きクエリに含まれていない場合に必要)  
  
    -   テーブル、ビュー、および名前付きクエリ間の論理主キーと外部キーのリレーションシップ  
  
##  <a name="bkmk_startWiz"></a> データ ソース ビュー ウィザードを使用した DSV の作成  
 DSV を作成するには、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]内のソリューション エクスプローラーでデータ ソース ビュー ウィザードを実行します。  
  
> [!NOTE]  
>  代わりに、ディメンションとキューブを最初に構築し、その後にスキーマ生成ウィザードを使用してモデルに対応する DSV を生成することもできます。 詳細については、「[スキーマ生成ウィザード (Analysis Services)](schema-generation-wizard-analysis-services.md)」を参照してください。  
  
1.  ソリューション エクスプローラーで、[データ ソース ビュー] フォルダーを右クリックし、 **[新しいデータ ソース ビュー]** をクリックします。  
  
2.  外部リレーショナル データベースへの接続情報を提供する、新規または既存のデータ ソース オブジェクトを指定します (ウィザード内で選択できるデータ ソースは 1 つのみです)。  
  
3.  同じページで、 **[詳細設定]** をクリックして特定のスキーマを選択し、フィルターを適用するか、テーブルのリレーションシップ情報を除外します。  
  
     **スキーマの選択**  
  
     複数のスキーマを格納している非常に大規模なデータ ソースの場合は、スペースなしのコンマ区切りリストでどのスキーマを使用するかを選択できます。  
  
     **リレーションシップの取得**  
  
     [データ ソース ビューの詳細オプション] ダイアログ ボックス内の **[リレーションシップを取得する]** チェックボックスをオフにすると、テーブルのリレーションシップ情報を意図的に省略できます。その結果、データ ソース ビュー デザイナー内にある複数のテーブル間でリレーションシップを手動で作成できます。  
  
4.  **使用できるオブジェクトのフィルター処理**  
  
     [使用できるオブジェクト] ボックスの一覧に非常に多くのオブジェクトが含まれている場合、選択条件として文字列を指定する単純なフィルターを適用して一覧を絞り込むことができます。 たとえば、「 **dbo** 」と入力し、 **[フィルター]** ボタンをクリックすると、"dbo" で始まる項目のみが **[使用できるオブジェクト]** ボックスの一覧に表示されます。 フィルターは、(たとえば、"sal"を返します。 sales と給与) の部分の文字列を使用できますが、複数の文字列や演算子を含めることはできません。  
  
5.  テーブルのリレーションシップが設定されていないリレーショナル データ ソースの場合は、 **[名前の一致]** ページが表示され、名前を一致させる適切な方法を選択することができます。 詳細については、このトピックの「 [リレーションシップの名前一致条件の指定](#bkmk_NameMatch) 」セクションを参照してください。  
  
##  <a name="bkmk_secondaryDS"></a> セカンダリ データ ソースの追加  
 複数のデータ ソースに属するテーブル、ビュー、または列を含むデータ ソース ビューを定義するとき、データ ソース ビューに追加するオブジェクトの最初のデータ ソースはプライマリ データ ソースとして指定されます (定義後にプライマリ データ ソースを変更することはできません)。 1 つのデータ ソースのオブジェクトに基づいてデータ ソース ビューを定義した後に、他のデータ ソースのオブジェクトを追加することはできます。  
  
 OLAP 処理またはデータ マイニング クエリで、1 つのクエリに複数のデータ ソースのデータが必要な場合は、プライマリ データ ソースが `OpenRowset` を使用したリモート クエリをサポートしている必要があります。 通常、これは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ソースになります。 たとえば、複数のデータ ソースの列にバインドされている属性を含む OLAP ディメンションを設計する場合は、処理中にこのディメンションを作成する `OpenRowset` クエリが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によって作成されます。 ただし、OLAP オブジェクトを作成できるか、データ マイニング クエリが 1 つのデータ ソースから解決される場合、`OpenRowset` クエリは作成されません。 特定の状況では、属性間の属性リレーションシップを定義して、`OpenRowset` クエリを必要なくすることができます。 属性リレーションシップの詳細については、「 [属性リレーションシップ](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)」、「 [データ ソース ビューでのテーブルまたはビューの追加または削除 (Analysis Services)](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) 」、「 [属性リレーションシップの定義](attribute-relationships-define.md)内のソリューション エクスプローラーでデータ ソース ビュー ウィザードを実行します。  
  
 セカンダリ データ ソースからテーブルおよび列を追加するには、ソリューション エクスプローラーで DSV をダブルクリックしてデータ ソース ビュー デザイナーで開いた後、[テーブルの追加と削除] ダイアログ ボックスを使用して、プロジェクトで定義した他のデータ ソースからオブジェクトを追加します。 詳細については、「 [データ ソース ビューでのテーブルまたはビューの追加または削除 (Analysis Services)](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)内のソリューション エクスプローラーでデータ ソース ビュー ウィザードを実行します。  
  
##  <a name="bkmk_NameMatch"></a> リレーションシップの名前一致条件の指定  
 DSV を作成すると、データ ソース内の外部キー制約に基づいて、テーブル間にリレーションシップが生成されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エンジンで適切な OLAP 処理クエリおよびデータ マイニング クエリを構築するには、これらのリレーションシップが必要です。 ただし、複数のテーブルが含まれているデータ ソースには、外部キー制約がない場合があります。 データ ソースに外部キー制約がない場合は、異なるテーブルの列名を照合する方法を定義するように指示するプロンプトがデータ ソース ビュー ウィザードに表示されます。  
  
> [!NOTE]  
>  名前の一致条件は、基になるデータ ソース内で外部キー リレーションシップが検出されない場合のみ指定するように要求されます。 外部キー リレーションシップが検出された場合は、そのリレーションシップが使用されます。また、DSV に含める追加のリレーションシップ (論理主キーなど) を手動で定義する必要があります。 詳細については、「[データ ソース ビューでの論理リレーションシップの定義 (Analysis Services)](define-logical-relationships-in-a-data-source-view-analysis-services.md)」と「[データ ソース ビューでの論理主キーの定義 (Analysis Services)](define-logical-primary-keys-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
 データ ソース ビュー ウィザードは、ユーザーが指定した名前一致条件を使用して列名を一致させ、DSV 内のさまざまなテーブル間にリレーションシップを作成します。 次の表に示すいずれかの条件を指定できます。  
  
|名前一致条件|説明|  
|----------------------------|-----------------|  
|**[主キーと同一の名前]**|基になるテーブルの外部キー列名は、対象になるテーブルの主キー列名と同じです。 たとえば、外部キー列 `Order.CustomerID` は、主キー列 `Customer.CustomerID`と同じです。|  
|**[対象のテーブル名と同一の名前]**|基になるテーブルの外部キー列名は、対象になるテーブルの名前と同じです。 たとえば、外部キー列 `Order.Customer` は、主キー列 `Customer.CustomerID`と同じです。|  
|**一致先のテーブル名と主キー名の組み合わせ**|基になるテーブルの外部キー列名は、対象になるテーブル名と主キー列名を連結したものと同じです。 区切り記号としてスペースまたはアンダースコアを使用できます。 たとえば、次の外部キーと主キーのペアはすべて一致します。<br /><br /> `Order.CustomerID` 」、「 `Customer.ID`<br /><br /> `Order.Customer ID` 」、「 `Customer.ID`<br /><br /> `Order.Customer_ID` 」、「 `Customer.ID`|  
  
 選択した条件によって、DSV の **NameMatchingCriteria** プロパティの設定が変わります。 この設定によって、ウィザードによる関連テーブルの追加方法が決まります。 また、この設定では、データ ソース ビュー デザイナーを使用してデータ ソース ビューを変更するときに、列をどのように一致させて DSV のテーブル間にリレーションシップを作成するかも決定されます。 **NameMatchingCriteria** プロパティの設定は、データ ソース ビュー デザイナーで変更できます。 詳細については、「[データ ソース ビューのプロパティの変更 (Analysis Services)](change-properties-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
> [!NOTE]  
>  データ ソース ビュー ウィザードを完了したら、データ ソース ビュー デザイナーのスキーマ ペインでリレーションシップを追加または削除できます。 詳細については、「[データ ソース ビューでの論理リレーションシップの定義 (Analysis Services)](define-logical-relationships-in-a-data-source-view-analysis-services.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データ ソース ビューでのテーブルまたはビューの追加または削除 (Analysis Services)](adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビューでの論理主キーの定義 (Analysis Services)](define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビューでの名前付き計算の定義 (Analysis Services)](define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビューでの名前付きクエリの定義 (Analysis Services)](define-named-queries-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビュー内のテーブルまたは名前付きクエリの置換 (Analysis Services)](replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビュー デザイナーでのダイアグラムの操作 (Analysis Services)](work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [データ ソース ビューでのデータの検索 (Analysis Services)](explore-data-in-a-data-source-view-analysis-services.md)   
 [データ ソース ビューの削除 (Analysis Services)](delete-a-data-source-view-analysis-services.md)   
 [データ ソース ビューでのスキーマの更新 (Analysis Services)](refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  
