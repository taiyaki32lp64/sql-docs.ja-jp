---
title: Power View レポートのレポート プロパティの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 812c205c1e612604c0c39a5effb3b9da50308d7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067957"
---
# <a name="configure-reporting-properties-for-power-view-reports"></a>Power View レポートのレポート プロパティの構成
  この補足のレッスンでは、Adventure Works Internet Sales Model プロジェクトのレポートのプロパティを設定します。 レポートのプロパティを使用すると、Power View 内のモデル データの選択や表示をエンド ユーザーが簡単にできるようになります。 また、プロパティを設定して、特定の列やテーブルの非表示や、グラフで使う新しいデータの作成を行います。  
  
 このレッスンを完了して、SharePoint と [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] に統合された [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] インスタンスにモデルを再配置すると、データ ソースの作成、データの接続情報の指定、Power View の起動、モデルを対象としたレポートの設計を実行できます。  
  
 このレッスンでは、Power View レポートの作成方法と使用方法については説明しません。 このレッスンは、Power View でのモデル データの表示に影響を与えるプロパティとその設定に関する概要を表形式モデル作成者に示すことを目的としています。 Power View レポートの作成の詳細については、次を参照してください。[チュートリアル。Power View のサンプル レポートの作成](https://go.microsoft.com/fwlink/?LinkId=221204)です。  
  
 このレッスンを完了するまでに時間を推定するには。**30 分**  
  
## <a name="prerequisites"></a>前提条件  
 この補足のレッスンは表形式モデルの作成チュートリアルの一部であり、チュートリアルでの順番に従って実行する必要があります。 この補足のレッスンの作業を実行する前に、前のレッスンをすべて完了している必要があります。  
  
 この補足のレッスンを完了するには、次の準備も必要です。  
  
-   Adventure Works Internet Sales Model (このチュートリアルで作成済み) が、表形式モードで実行されている Analysis Services インスタンスに配置できる状態になっている、または既に配置済みである。  
  
-   表形式モードで実行されている [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] と [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] に統合されている SharePoint サイトが、Power View レポートをサポートするように構成されている。  
  
-   Adventure Works Internet Sales Model を参照する SharePoint サイト上でデータ接続を作成するための十分な権限がある。  
  
## <a name="model-properties-that-affect-reporting"></a>レポートに影響するモデルのプロパティ  
 表形式モデルを作成するとき、個々の列やテーブルに特定のプロパティを設定して、エンド ユーザーが Power View のレポートをより使いやすくすることができます。 また、データの視覚エフェクトをサポートする追加のモデル データや、レポート クライアントに固有の他の機能を作成することもできます。 ここでは、Adventure Works Internet Sales Model のサンプルにいくつかの変更を加えます。  
  
-   **新しいデータを追加**-にグラフを表示しやすい形式で日付の情報を作成する計算列で DAX 数式を使用して新しいデータを追加します。  
  
-   **エンド ユーザーには不要なテーブルと列の非表示** - **[非表示]** プロパティは、テーブルやテーブルの列をレポート クライアントに表示するかどうかを制御します。 項目は非表示になってもモデルの一部であり、引き続きクエリや計算に使用できます。  
  
-   **クリック 1 回でテーブルを有効にする**-既定も何も起こりません、エンドユーザーが、フィールド リストでテーブルをクリックします。 この動作を変更して、テーブルをクリックするとそのテーブルがレポートに追加されるようにするには、テーブルに含める各列に既定のフィールド セットを設定します。 このプロパティは、エンド ユーザーの使用頻度の高いテーブルの列に設定されます。  
  
-   **必要に応じたグループの設定** - **[一意の行の保持]** プロパティは、列内の値を別のフィールド (識別子フィールドなど) の値によってグループ化するかどうかを決定します。 Customer Name のように重複した値が含まれる列 (たとえば、"John Smith" という顧客が複数存在する可能性があります) では、エンド ユーザーに正しい結果を提供するために、 **[行識別子 (ROWID)]** フィールドでグループ化 (一意の行を保持) することが重要です。  
  
-   **データ型とデータ形式の設定** - 既定では、フィールドをメジャーとして使用できるかどうかを判断するために、Power View は列のデータ型に基づいたルールを適用します。 Power View におけるデータの視覚エフェクトにはそれぞれ、メジャーと非メジャーをどこに配置するかについてのルールもあるので、エンド ユーザーが適切な操作を実行するように、モデル内のデータ型を設定したり、既定値をオーバーライドしたりすることが重要です。  
  
-   **列で並べ替えを設定**プロパティ -、**列による並べ替え**プロパティは、列の値を別のフィールドの値によって並べ替えするかどうを指定します。 たとえば、月の名前を含む Month Calendar 列を Month Number 列によって並べ替えます。  
  
## <a name="hide-tables-from-client-tools"></a>クライアント ツールでのテーブルの非表示  
 Product テーブルには既に Product Category 計算列と Product Subcategory 計算列があるので、クライアント アプリケーションに Product Category テーブルと Product Subcategory テーブルを表示する必要はありません。  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>Product Category テーブルと Product Subcategory テーブルを非表示にするには  
  
1.  モデル デザイナーで、 **Product Category** テーブル (タブ) を右クリックし、 **[クライアント ツールに非表示]** をクリックします。  
  
2.  **Product Subcategory** テーブル (タブ) を右クリックし、 **[クライアント ツールに非表示]** をクリックします。  
  
## <a name="create-new-data-for-charts"></a>グラフ用の新しいデータの作成  
 DAX 式を使用して、モデル内で新しいデータを作成することが必要な場合があります。 ここでは、Date テーブルに 2 つの新しい計算列を追加します。 これらの新しい列は、グラフで使うのに便利な形式の日付フィールドを提供します。  
  
#### <a name="to-create-new-data-for-charts"></a>グラフ用の新しいデータを作成するには  
  
1.  **Date** テーブルを右端までスクロールして、 **[列の追加]** をクリックします。  
  
2.  数式バーで次の式を使用して、2 つの新しい計算列を追加します。  
  
    |列名|[数式]|  
    |-----------------|-------------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |年月|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>既定のフィールド セット  
 既定のフィールド セットは、テーブルの列とメジャーの定義済みリストであり、レポート フィールド リストでテーブルをクリックしたときに、自動的に Power View レポート キャンバスに追加されます。 基本的に、このテーブルが Power View レポート内で視覚化されたときにユーザーに表示される既定の列、メジャー、フィールドの順序を指定できます。  Internet Sales モデルでは、Customer、Geography、Product の各テーブルの既定のフィールド セットと順序を定義します。 含まれるのは、Power View レポートを使用して Adventure Works Internet Sales データを分析するときにユーザーが表示する必要がある、使用頻度の高いこれらの列のみです。  
  
 既定のフィールド セットの詳細については、SQL Server オンライン ブックの「[Power View レポートの既定のフィールド セットの構成 (SSAS テーブル)](tabular-models/power-view-configure-default-field-set-for-reports.md)」を参照してください。  
  
#### <a name="to-set-default-field-set-for-tables"></a>テーブルの既定のフィールド セットを設定するには  
  
1.  モデル デザイナーで、**Customer** テーブル (タブ) をクリックします。  
  
2.  **[プロパティ]** ウィンドウの **[レポートのプロパティ]** の **[既定のフィールド セット]** プロパティで、 **[クリックして編集]** をクリックして **[既定のフィールド セット]** ダイアログ ボックスを開きます。  
  
3.  **[既定のフィールド セット]** ダイアログ ボックスの **[テーブル内のフィールド]** ボックスの一覧で、Ctrl キーを押しながら次のフィールドをクリックし、 **[追加]** をクリックします。  
  
     **[Birth Date]** 、 **[Customer Alternate Id]** 、 **[First Name]** 、 **[Last Name]** 。  
  
4.  **[既定のフィールド (並べ替え順)]** ウィンドウで、[上へ移動] と [下へ移動] を使用して次の順序に並べます。  
  
     **[Customer Alternate Id]**  
  
     **[First Name]**  
  
     **[Last Name]**  
  
     **Birth Date**  
  
5.  **[OK]** をクリックして、 **Customer** テーブルの **[既定のフィールド セット]** ダイアログ ボックスを閉じます。  
  
6.  **Geography** テーブルでも同じ手順を実行し、次のフィールドをこの順序に並べます。  
  
     **市区町村**、 **State Province Code**、**状態リージョン コード**します。  
  
7.  最後に、 **Product** テーブルについても同じ手順を実行し、次のフィールドをこの順序に並べます。  
  
     **Product Alternate Id**、**Product Name**。  
  
## <a name="table-behavior"></a>テーブルの動作  
 [テーブルの動作] プロパティを使用すると、Power View レポートで使用するテーブルについて、さまざまな視覚エフェクトの種類の既定の動作およびグループ化動作を変更できます。 これにより、名前やイメージ、またはタイル、カード、グラフ レイアウトのタイトルなど、識別情報の適切な既定位置を設定できます。  
  
 テーブル動作プロパティの詳細については、「[Power View レポートのテーブル動作プロパティの構成 (SSAS テーブル)](tabular-models/power-view-configure-table-behavior-properties-for-reports.md)」を参照してください。  
  
#### <a name="to-set-table-behavior-for-tables"></a>テーブルの [テーブルの動作] を設定するには  
  
1.  モデル デザイナーで、 **Customer** テーブル (タブ) をクリックします。  
  
2.  **[プロパティ]** ウィンドウの **[テーブルの動作]** プロパティで、 **[クリックして編集]** をクリックして **[テーブルの動作]** ダイアログ ボックスを開きます。  
  
3.  **[テーブルの動作]** ダイアログ ボックスの **[行識別子 (ROWID)]** ボックスの一覧から、 **[Customer Id]** 列を選択します。  
  
4.  **[一意の行の保持]** ボックスの一覧の、 **[First Name]** と **[Last Name]** を選択します。  
  
     このプロパティを設定することで、重複している場合でも一意として扱う必要のある値をこれらの列が提供することを指定します (たとえば、同姓または同名の従業員が複数いる場合など)。  
  
5.  **[既定のラベル]** ボックスの一覧から、 **[Last Name]** 列を選択します。  
  
     このプロパティを設定することで、この列が行データを表す表示名を提供することを指定します。  
  
6.  **Geography** テーブルについても同じ手順を繰り返します。行識別子 (ROWID) として **[Geography Id]** 列を選択し、 **[一意の行の保持]** ボックスの一覧の **[City]** 列を選択します。 このテーブルには、既定のラベルを設定する必要はありません。  
  
7.  **Product** テーブルについても同じ手順を繰り返します。行識別子 (ROWID) として **[Product Id]** 列を選択し、 **[一意の行の保持]** ボックスの一覧の **[Product Name]** 行を選択します。 **[既定のラベル]** には、 **[Product Alternate Id]** を選択します。  
  
## <a name="reporting-properties-for-columns"></a>列の [レポートのプロパティ]  
 列にはいくつかの基本のプロパティと列に固有のレポート プロパティがあり、このプロパティを設定することにより、モデルのレポートをより使いやすくすることができます。 たとえば、ユーザーが必ずしもすべてのテーブルのすべての列を見る必要がない場合もあります。 列の Hidden プロパティを使用して、Product Category と Product Subcategory テーブルの前に、例は、それ以外の場合に表示されているテーブルから特定の列を非表示にすることができます。 [データ形式] や [列で並べ替え] などの他のプロパティも、レポート内の列データの表示に影響を及ぼします。 ここでは、特定の列にいくつかのプロパティを設定します。 操作の必要がない他の列は、以下には表示していません。  
  
 ここでは、さまざまな列のプロパティのうちの一部のみを設定しますが、他にも多くのプロパティがあります。 列のレポート プロパティの詳細については、SQL Server オンライン ブックの「[列のプロパティ (SSAS テーブル)](tabular-models/properties-ssas-tabular.md)」を参照してください。  
  
#### <a name="to-set-properties-for-columns"></a>列のプロパティを設定するには  
  
1.  モデル デザイナーで、 **Customer** テーブル (タブ) をクリックします。  
  
2.  **[Customer Id]** 列をクリックして、 **[プロパティ]** ウィンドウに列のプロパティを表示します。  
  
3.  **[プロパティ]** ウィンドウで、 **[非表示]** プロパティを True に設定します。 **[Customer Id]** 列は、モデル デザイナーではグレーで表示されるようになります。  
  
4.  この手順を繰り返して、以下の各表に指定するように列のレポート プロパティを設定します。 他のプロパティはすべて、既定の設定のままにしておきます。  
  
     **Customer**  
  
    |[列]|プロパティ|値|  
    |------------|--------------|-----------|  
    |[Geography Id]|[非表示]|True|  
    |[Birth Date]|データ形式|短い日付|  
  
     **Date**  
  
    > [!NOTE]  
    >  日付テーブルが日付テーブルの設定として、マークを使用して、モデルの日付テーブルとして選択された、ためにレッスン 7 に。一意の識別子では、日付列の行識別子プロパティとして使用するには、日付テーブルとしてマークと、列と日付のテーブルに日付列は自動的に True に設定して、変更できません。 DAX 式でタイム インテリジェンス関数を使用するときは、日付テーブルを指定する必要があります。 このモデルでは、タイム インテリジェンス関数を使用していくつかのメジャーを作成して、さまざまな期間 (前四半期と現四半期など) の売上データを計算しました。これは KPI にも使用できます。 日付テーブルの指定の詳細については、SQL Server オンライン ブックの「[タイム インテリジェンスで使用する [日付テーブルとしてマーク] の指定 (SSAS テーブル)](tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md)」を参照してください。  
  
    |[列]|プロパティ|値|  
    |------------|--------------|-----------|  
    |date|データ形式|短い日付|  
    |Day Number of Week|[非表示]|True|  
    |Day Name|[列で並べ替え]|Day Number of Week|  
    |Day of Week|[非表示]|True|  
    |Day of Month|[非表示]|True|  
    |Day of Year|[非表示]|True|  
    |Month Name|[列で並べ替え]|Month|  
    |Month|[非表示]|True|  
    |Month Calendar|[非表示]|True|  
    |Fiscal Quarter|[非表示]|True|  
    |Fiscal Year|[非表示]|True|  
    |Fiscal Semester|[非表示]|True|  
  
     **Geography**  
  
    |[列]|プロパティ|値|  
    |------------|--------------|-----------|  
    |[Geography Id]|[非表示]|True|  
    |Sales Territory Id|[非表示]|True|  
  
     **Product**  
  
    |[列]|プロパティ|値|  
    |------------|--------------|-----------|  
    |[Product Id]|[非表示]|True|  
    |Product Alternate Id|[既定のラベル]|True|  
    |Product Subcategory Id|[非表示]|True|  
    |Product Start Date|データ形式|短い日付|  
    |Product End Date|データ形式|短い日付|  
    |Large Photo|[非表示]|True|  
  
     **Internet Sales**  
  
    |[列]|プロパティ|値|  
    |------------|--------------|-----------|  
    |[Product Id]|[非表示]|True|  
    |[Customer Id]|[非表示]|True|  
    |Promotion Id|[非表示]|True|  
    |Currency Id|[非表示]|True|  
    |Sales Territory Id|[非表示]|True|  
    |Order Quantity|データ型<br /><br /> データ形式<br /><br /> 小数点以下表示桁数|10 進数<br /><br /> 10 進数<br /><br /> 0|  
    |Order Date|データ型|短い日付|  
    |Due Date|データ型|短い日付|  
    |Ship Date|データ型|短い日付|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 表形式モデルの再配置  
 モデルを変更したので、再配置する必要があります。 実行するタスクを繰り返すことが本質的に[レッスン 14。デプロイ](lesson-13-deploy.md)します。  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Adventure Works Internet Sales 表形式モデルを再配置するには  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で **[ビルド]** メニューをクリックし、 **[Adventure Works Internet Sales Model の配置]** をクリックします。  
  
     **[配置]** ダイアログ ボックスが表示され、メタデータの配置状況と、モデルに含まれる各テーブルが表示されます。  
  
## <a name="next-steps"></a>次の手順  
 これで、Power View を使用してモデルのデータを表示できるようになりました。 SharePoint サイトの Analysis Services と Reporting Services のアカウントが、モデルを配置した Analysis Services インスタンスに対する読み取り権限を持っていることを確認します。  
  
 モデルを参照する Reporting Services のレポート データ ソースを作成するには、「 [データ モデルの共有データ ソースの作成 (SSRS)](https://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx)」を参照してください。  
  
  
