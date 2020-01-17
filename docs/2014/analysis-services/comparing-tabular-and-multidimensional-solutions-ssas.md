---
title: テーブルと多次元ソリューションのソリューション (SSAS) の比較 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1da4224387e70ccc76e069aa3ce411dddb79b805
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087769"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>Comparing Tabular and Multidimensional Solutions (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、多次元と表形式の 2 つの方法でデータ モデリングを行えます。 それらの間にはかなり重複している部分がありますが、前進する方法について決定を通知するうえで重要な相違点もあります。 このトピックでは、機能比較を提供し、それぞれのアプローチで一般的なプロジェクト要件にどのように対処しているかを説明します。 たとえば、特定のデータ ソースのサポートが最も重要な考慮事項である場合、データ ソースに関するセクションが、使用するモデリング アプローチを決定するうえで役立ちます。  
  
 このトピックのセクションは次のとおりです。  
  
-   [Analysis Services でのモデリングの概要](#bkmk_overview)  
  
-   [ソリューションの種類ごとのデータ ソースのサポート](#bkmk_ds)  
  
-   [モデルの機能](#bkmk_models)  
  
-   [モデルのサイズ](#bkmk_modelsize)  
  
-   [プログラマビリティと開発者エクスペリエンス](#bkmk_ext)  
  
-   [クエリおよびスクリプト言語のサポート](#bkmk_lang)  
  
-   [セキュリティ機能のサポート](#bkmk_sec)  
  
-   [デザイン ツール](#bkmk_designer)  
  
-   [クライアントおよびレポート アプリケーション](#bkmk_client)  
  
-   [ホスティング プラットフォーム](#bkmk_sharePoint)  
  
-   [多次元および表形式ソリューションのサーバー配置モード](#bkmk_deploymentmode)  
  
-   [次の手順:ソリューションを構築します。](#bkmk_Next)  
  
 詳細については、MSDN の技術記事を参照してください。[SQL Server 2012 Analysis services 表形式または多次元のモデリング エクスペリエンスを選択する](https://go.microsoft.com/fwlink/?LinkId=251588)します。  
  
##  <a name="bkmk_overview"></a> Analysis Services でのモデリングの概要  
 Analysis Services は、モデル開発エクスペリエンスに加え、Analysis Services インスタンスでのデータベース ホスティングを介したモデル配置を提供します。 モデルの種類には、テーブルと多次元が含まれます。 期待されるように、データベース ホスティングはテーブルおよび多次元ソリューションをサポートしますが、データベース ホスティングには PowerPivot for SharePoint も含まれます。  
  
 PowerPivot for SharePoint は、Excel で作成してから SharePoint に保存された Excel データ モデルのホストおよび管理に役立つ、SharePoint の付加的なサービスとして Analysis Services で動作する *SharePoint モードの Analysis Services*です。 このコンテキストでの Analysis Services の役割は、データ モデルのメモリへの読み込み、外部データ ソースからのデータの更新、およびモデルに対するクエリの実行を行うことです。 この構成では、Analysis Services はバック グラウンドで動作します。 Analysis Services へのすべての接続と要求は、SharePoint によって実行されますが、Excel ブックにデータ モデルが含まれている場合にのみ行われます (データ モデルは Excel ブックでは省略可能です)。 Excel では、データ モデルを構築しを SharePoint では、ホストは、プロジェクトの要件に合わせて、表示[Power Pivot:強力なデータ分析、および Excel でデータ モデリング](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)と[PowerPivot for SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)詳細についてはします。  
  
> [!NOTE]  
>  Excel データ モデルとテーブル モデルのアーキテクチャは似ています。 大量のデータをサポートする必要がある、または Excel では使用できないその他のモデルの機能を使用する必要がある場合、Excel データ モデルをテーブル モデルにインポートすることができます。  
  
 テーブル ソリューションと多次元ソリューションは、スタンドアロンの [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] インスタンスで実行される企業の BI プロジェクトを対象としており、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] を使用して作成されます。 どちらのソリューションでも、Excel、Reporting Services のレポート、および Microsoft やサードパーティのその他の BI アプリケーションと簡単に統合できる、高パフォーマンスの分析データベースが得られます。 どちらのソリューションも、Analysis Services をサポートする任意のクライアント アプリケーションで使用できるスタンドアロン データベースになります。  
  
 概略でとらえれば、テーブルと多次元のモデルの間で、次のような特徴が区別されます。  
  
-   多次元のデータ マイニング ソリューションでは、OLAP モデル構造 (キューブとディメンション)、および事前に集計されたデータのプライマリ データ記憶域としてディスクを使用する MOLAP、ROLAP、または HOLAP ストレージを使用します。  
  
-   テーブル ソリューションは、データのモデル化にリレーショナル モデル構造 (テーブル、リレーションシップなど) を使用し、データの格納と計算にメモリ内分析エンジンを使用します。 すべてではないにしても、モデルのほとんどは RAM に格納されます。多くの場合、多次元の対応するものよりもはるかに高速になります。  
  
 新しいプロジェクトの場合は、テーブルを使用するアプローチを最初に検討してください。 テーブル ソリューションは、デザイン、テスト、配置をよりすばやく行うことができます。また、Microsoft の最新のセルフサービス BI アプリケーションで使用するのにも適しています。  
  
##  <a name="bkmk_ds"></a> ソリューションの種類ごとのデータ ソースのサポート  
 多次元とテーブルの両方のモデルとも、外部ソースからインポートしたデータを使用します。 ほとんどの開発者は、モデルの背後のプライマリ データ ソースとして、レポート データ構造をサポートするように設計されたデータ ウェアハウスを使用します。 多くの場合、データ ウェアハウスはスター スキーマまたはスノーフレーク スキーマに基づいており、SSIS を使用して OLTP ソリューションからデータ ウェアハウスにデータを読み込みます。 モデリングは、バックエンド データ ソースとしてデータ ウェアハウスを使用すると、よりシンプルになります。  
  
|**リンク**|**サポートされているオプションの概要**|  
|--------------|--------------------------------------|  
|[サポートされるデータ ソース&#40;SSAS 多次元&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|多次元モデルは、リレーショナル データ ソースからのデータを使用します。|  
|[サポートされているデータ ソース &#40;SSAS テーブル&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|テーブル モデルは、フラット ファイル、データ フィード、ODBC データ プロバイダーを使用してアクセスされるデータ ソースなど、さまざまなデータ ソースをサポートします。|  
  
 どちらのモデリング アプローチも、同じモデル内の複数のデータ ソースからのデータを使用できます。  
  
 モデルの外部にあるモデルのデータをリレーショナル データベースで格納する (データのサイズ要件が非常に大きくなる場合に使用される手法) 必要が生じた場合、データ ソースの種類は SQL Server リレーショナル データベースにする必要があります。 多次元モデルの ROLAP ストレージとテーブル モデルの DirectQuery の両方に、この要件があります。  
  
 **データ サイズ**  
  
 テーブル ソリューションと多次元ソリューションではデータ圧縮が使用されるため、Analysis Services データベースのサイズがデータのインポート元のデータ ウェアハウスに比べて小さくなります。 実際の圧縮は、基になるデータの特性によって異なるので、データが処理されてクエリで使用された後にどの程度のディスクおよびメモリがソリューションに必要なのかを正確に知る方法はありません。 多くの Analysis Services 開発者が使用する目安は、多次元データベースの 1 次記憶域が元のデータの約 3 分の 1 のサイズになるというものです。  
  
 テーブル データベースでは、特にデータの大部分がファクト テーブルからインポートされる場合、データをさらに小さく圧縮できることもあります (約 10 分の 1 のサイズ)。 テーブル ソリューションでは、テーブル データベースがメモリに読み込まれるときに作成される追加のデータ構造により、メモリ要件がディスク上のデータのサイズよりも大きくなります。 負荷が高い場合、どちらのソリューションでも、Analysis Services によるデータのキャッシュ、格納、スキャン、クエリに応じて必要なディスクとメモリが増加すると予想されます。  
  
 大きなデータを必要とするプロジェクトでは、データの要件がモデルの種類の選択を左右する場合もあります。 読み込む必要のあるデータのサイズが数テラバイトに及ぶ場合、そのデータを格納できるだけのメモリがないと、テーブル ソリューションでは要件が満たされない可能性があります。 メモリ内のデータをディスクにスワッピングするページング オプションもありますが、データの量が多い場合は多次元ソリューションの方が適しています。 現在最も大きい実稼働の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] データベースは多次元データベースです。 テーブル ソリューションのメモリ ページング オプションの詳細については、「 [Memory Properties](server-properties/memory-properties.md)」を参照してください。 多次元ソリューションをスケールアウトする方法の詳細については、「 [読み取り専用データベースによる Analysis Services のクエリのスケールアウト](https://go.microsoft.com/fwlink/?LinkId=251711)」を参照してください。  
  
##  <a name="bkmk_models"></a> モデルの機能  
 次の表は、機能の利用の可否をモデルごとにまとめたものです。 Analysis Services がインストール済みという方は、インストールしたサーバー モードの機能を知るうえでの参考にしてください。 Analysis Services のモデル機能をよく知っていて、なおかつ以下のいずれかの機能がビジネス上の要件に含まれる場合は、必要な機能が、構築しようとしているモデルの種類で利用できるかどうかをこの一覧を見て確認できます。  
  
 各モデルの機能の違いの詳細については、MSDN の技術記事「 [SQL Server 2012 Analysis Services のテーブル モデルと多次元モデルの選択](https://go.microsoft.com/fwlink/?LinkId=251588) 」を参照してください。  
  
> [!NOTE]  
>  テーブル モデルは、SQL Server の特定のエディションでサポートされています。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
||||  
|-|-|-|  
||**多次元**|**テーブル**|  
|アクション|[はい](multidimensional-models/actions-in-multidimensional-models.md)|いいえ|  
|集約オブジェクト|[はい](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|いいえ|  
|計算されるメジャー|[はい](multidimensional-models/create-calculated-members.md)|はい|  
|カスタム アセンブリ|[はい](multidimensional-models/multidimensional-model-assemblies-management.md)|いいえ|  
|カスタム ロールアップ|はい|いいえ|  
|Distinct Count|[はい](multidimensional-models/use-aggregate-functions.md)|[はい] (DAX 経由) *|  
|ドリルスルー|[はい](multidimensional-models/actions-in-multidimensional-models.md)|はい|  
|階層|[はい](multidimensional-models/user-defined-hierarchies-create.md)|はい|  
|KPI|[はい](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|はい|  
|リンク メジャー グループ|[はい](multidimensional-models/linked-measure-groups.md)|いいえ|  
|多対多リレーションシップ|[はい](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|いいえ|  
|親子階層|[はい](multidimensional-models/parent-child-dimension.md)|○ (DAX 経由)|  
|[メジャー グループ]|[はい](tabular-models/partitions-ssas-tabular.md)|  
|パースペクティブ|[はい](multidimensional-models/perspectives-in-multidimensional-models.md)|[はい](tabular-models/partitions-ssas-tabular.md)|  
|準加法メジャー|[はい](multidimensional-models/define-semiadditive-behavior.md)|○ (DAX 経由)|  
|翻訳|[はい](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|いいえ|  
|ユーザー定義階層|[はい](multidimensional-models/user-defined-hierarchies-create.md)|はい|  
|[書き戻し]|[はい](multidimensional-models/set-partition-writeback.md)|いいえ|  
  
 \* 場合は、ソリューションが、非常に多数の個別のカウント (何百万顧客 Id) などをサポートする必要がありますまず Tabular してみてください。 このシナリオでは、パフォーマンスが向上する傾向があります。 ホワイト ペーパーでは、個別のカウントについてのセクションを参照して[Analysis Services ケース スタディ。大規模な商用ソリューションにおける表形式モデルを使用して](https://msdn.microsoft.com/library/dn751533.aspx)します。  
  
##  <a name="bkmk_modelsize"></a> モデルのサイズ  
 モデルのサイズ (オブジェクトの総数) は、ソリューションの種類によって変わりません。 ただし、各ソリューションを作成するためのデザイン ツールで、大量のオブジェクトの処理に対応する程度は異なります。 大規模なモデルは、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] で作成すると比較的簡単です。オブジェクト エクスプローラーやソリューション エクスプローラーでオブジェクトを種類別にダイアグラム化したり一覧表示したりするための機能が豊富に揃っているからです。  
  
 何百ものテーブルやディメンションから構成される非常に大きなモデルは、通常、デザイン ツールではなく Visual Studio でプログラムによって作成されます。 詳細については、モデル内のオブジェクトの最大数は、次を参照してください。[最大容量仕様&#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)します。  
  
##  <a name="bkmk_ext"></a> プログラマビリティと開発者エクスペリエンス  
 テーブル モデルと多次元モデルについては、1 つのオブジェクト モデルが両方のモードで共有されます。 AMO と ADOMD.NET では、両方のモードがサポートされます。 どちらのクライアント ライブラリもテーブル構造用に変更されていないため、多次元モデルとテーブル モデルの構造と名前付け規則の間の相互関係を理解しておく必要があります。 手始めとして、AMO to Tabular プログラミング サンプルを確認して、テーブル モデルに対する AMO プログラミングについて学習します。 詳細についてからサンプルをダウンロード、 [codeplex web サイト](https://go.microsoft.com/fwlink/?LinkID=221036)します。  
  
 テーブル ソリューションでは、1 つのソリューションで使用できる model.bim ファイルは 1 つだけです。したがって、すべての作業を 1 つのファイルで行う必要があります。 1 つのソリューションで複数のプロジェクトを使って作業することに慣れている開発チームは、共有テーブル ソリューションを作成する際には作業方法を変更する必要があります。  
  
##  <a name="bkmk_lang"></a> クエリおよびスクリプト言語のサポート  
 Analysis Services には MDX、DMX、DAX、XML/A、ASSL が用意されています。 これらの言語のサポート状況は、モデルの種類によって若干異なります。 クエリとスクリプト言語の要件が重要な検討事項である場合は、次の一覧を参考にしてください。  
  
-   テーブル モデル データベースは、DAX の計算、DAX クエリ、および MDX クエリをサポートします。  
  
-   多次元モデル データベースは、MDX の計算および MDX クエリと ASSL をサポートします。  
  
-   データ マイニング モデルは DMX と ASSL をサポートします。  
  
-   Analysis Services PowerShell は、サーバーとデータベースの管理をサポートします。 モデルの種類 (またはサーバー モード) は、PowerShell コマンドレットを使用する際の要素とはなりません。  
  
 すべてのデータベースは XML/A をサポートします。  
  
##  <a name="bkmk_sec"></a> セキュリティ機能のサポート  
 Analysis Services のすべてのソリューションは、データベース レベルでセキュリティを確保できます。 それよりも詳細なセキュリティ オプションは、モードによって異なります。 きめ細かなセキュリティ設定がソリューションに求められる場合は、構築しようとしているソリューションの種類でサポートされるセキュリティのレベルを次の一覧で確認してください。  
  
-   テーブル モデル データベースには、Analysis Services のロール ベースの権限による行レベルのセキュリティが使用されます。  
  
-   多次元モデル データベースには、Analysis Services のロール ベースの権限によるディメンションおよびセル レベルのセキュリティが使用されます。  
  
 Excel データ モデルは、テーブル モードのサーバーに復元することができます。 ファイルが復元されると、SharePoint から切り離されます (SharePoint の場所からファイルを復元することを想定しています)。これにより、行レベルのセキュリティを含め、テーブルのモデリング機能をほとんどすべて使用することができます。 例外として、リンク テーブルは使用できません。  
  
##  <a name="bkmk_designer"></a> デザイン ツール  
 分析モデルの構築に携わるユーザーごとにデータ モデリングのスキルと技術的な専門知識は大きく異なることが考えられます。 ツールへの慣れやユーザーの専門知識がソリューションの検討対象に含まれる場合は、モデルの作成に関して次の経験を比較します。  
  
|**モデリング ツール**|**使用方法**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|テーブル、多次元、およびデータ マイニングの各ソリューションを作成する目的で使用します。 この作成環境は、Visual Studio シェルを使用して、ワークスペース、プロパティ ペイン、およびオブジェクトのナビゲーションを提供します。 Visual Studio を既に利用している技術系ユーザーのほとんどは、ビジネス インテリジェンス アプリケーションの構築手段としてこのツールを選びます。 詳細については、「 [Tools and applications used in Analysis Services](tools-and-applications-used-in-analysis-services.md) 」をご覧ください。|  
|Excel 2013 以降 (Power Pivot for Excel アドイン付き)|Power Pivot for Excel は、Excel データ モデルを編集および強化するために使用するツールです。 Excel 上で開く別個のアプリケーション ワークスペースを備えていますが、Excel と同じビジュアル要素 (タブ付きページ、グリッド レイアウト、および数式バー) を使用します。 Excel に習熟しているユーザーは、一般的に [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]よりもこのツールを好みます。 参照してください[Power Pivot:強力なデータ分析、および Excel でデータ モデリング](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)します。|  
  
##  <a name="bkmk_client"></a> クライアントおよびレポート アプリケーション  
 以前のリリースでは、モデルの種類の選択は、どのクライアント アプリケーションを使用できるかに影響していましたが、時間の経過と共にそれらは区別されなくなりました。 テーブルおよび多次元のモデルは、Analysis Services データに接続するクライアント アプリケーションに関してほとんどの場合、同等のサポートを提供します。 次の表は、Analysis Services データ モデルを使用できる Microsoft クライアント アプリケーションの一覧を示します。  
  
|**アプリケーション**|**[説明]**|  
|---------------------|---------------------|  
|Excel PivotTable レポート|Excel 機能はテーブルと多次元の両方のモデルで同様ですが、書き戻し (Excel が実装する Analysis Services 機能) は多次元のみでサポートされています。|  
|Reporting Services RDL レポート|レポート ビルダーまたはレポート デザイナーのいずれかで作成した RDL レポートは、Analysis Services モデルだけでなく、PowerPivot for SharePoint 上でホストされる Excel データ モデルも使用できます。|  
|PerformancePoint ダッシュボード|SharePoint では、PerformancePoint ダッシュ ボードは Excel データ モデルを含むすべての Analysis Services データベースに接続できます。 詳細については、「 [データ接続の作成 (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkdID=218155)」を参照してください。|  
|Office 365 または Power BI サイトでの [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]|テーブル モデルのみです。|  
|SharePoint オンプレミスでの [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] (SharePoint からの ClickOnce アプリケーションとして) は、Analysis Services キューブまたはテーブル モデルのいずれかを使用できます。|  
  
##  <a name="bkmk_deploymentmode"></a> 多次元ソリューションとテーブル ソリューションのサーバー配置モード  
 Analysis Services インスタンスは、サーバーの操作コンテキストを設定する 3 つのモードのいずれかでインストールされます。 サーバーに配置できるソリューションの種類は、インストールするサーバー モードによって決まります。 モード間の主な違いはストレージとメモリのアーキテクチャですが、それ以外にも違いは存在します。 3 つのサーバー モードについて次の表で簡単に説明します。 詳細については、「[Analysis Services インスタンスのサーバー モードの決定](instances/determine-the-server-mode-of-an-analysis-services-instance.md)」を参照してください。  
  
|配置モード|説明|  
|---------------------|-----------------|  
|0 - 多次元およびデータ マイニング|Analysis Services の既定のインスタンスに配置する多次元およびデータ マイニング ソリューションを実行します。 配置モード 0 は、Analysis Services のインストールの既定値です。 詳細については、「 [Install Analysis Services in Multidimensional and Data Mining Mode](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)」を参照してください。|  
|1 - PowerPivot for SharePoint|Excel データ モデルのアクセスでは、Analysis Services は SharePoint の内部コンポーネントです。 Analysis Services は配置モード 1 でインストールされ、SharePoint 環境の Excel Services からのみ要求を受け入れます。 詳しくは、「 [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)」をご覧ください。|  
|2 - テーブル|配置モード 2 用に構成されている Analysis Services のスタンドアロン インスタンスでテーブル ソリューションを実行します。 詳細については、「 [Install Analysis Services in Tabular Mode](instances/install-windows/install-analysis-services.md)」を参照してください。|  
  
 サーバー モデルは置き換えることはできないことに注意してください。 インストール時に、サーバー操作用のモードを選択します。 すべてのワークロードをサポートするため、複数のインスタンス (サーバー モードごとに 1 つ) をインストールする必要があります。  
  
##  <a name="bkmk_sharePoint"></a> ホスティング プラットフォーム  
 マイクロソフトには、データ、アプリケーション、レポート、およびコラボレーションをホストするためのいくつかの方法論があります。 このセクションでは、各ホスティング プラットフォームに関する Analysis Services の相互運用性について説明します。  
  
|**プラットフォーム**|**[説明]**|  
|------------------|---------------------|  
|Microsoft Azure|Azure 仮想マシンでは、サポートされるすべてのバージョンおよびエディションの Analysis Services を実行できます。 Azure SQL データベース (オンプレミスのリレーショナル データベース エンジンとほとんど同じ機能を提供する Azure のサービス) とは対照的に、Azure には Analysis Services に対応するものはありません。 Azure VM での Analysis Services のインストール、構成、および実行だけが、Azure ベースのオプションです。|  
|Office 365|Office 365 の Excel Online は、オンプレミスで実行されるテーブルと多次元のモデルへのリモート接続をサポートします。|  
|Office 365 の Power BI サイト|Power BI サイトでは、Power View レポートはオンプレミスで実行するテーブル データ モデルに接続できます。|  
|オンプレミス サーバー (SharePoint と SQL Server のインスタンス)|オンプレミス データベース サーバー (つまり、インストールされた Analysis Services が存在する SQL Server インスタンス) は、引き続きレポートおよびクライアント アプリケーションで Analysis Services データを使用できるようにするための主な手段となっています。 テーブル、多次元、およびデータ マイニング ソリューションは、SharePoint に依存せず、ネットワーク上の Analysis Services インスタンスで実行されます。<br /><br /> SQL Server は、PowerPivot データ アクセスおよびテーブル データ アクセスのサポートを追加することによって SharePoint と統合されます。 SharePoint と SQL Server の統合に対する投資は、各製品から使用される機能の数を最大にすると増大します。 SharePoint がある場合は、PowerPivot データ アクセスを有効にし、ネットワーク サーバー上の外部 Analysis Services インスタンスで実行されるテーブル データベースにアクセスするための PowerPivot .bism 接続ファイルを取得するために、SQL Server PowerPivot for SharePoint をインストールすることができます。<br /><br /> SharePoint と SQL Server の両方がある場合は、以下のサービスとアプリケーションの組み合わせをサポートすることができます。<br /><br /> Analysis Services モデル (テーブルまたは多次元のいずれか)<br /><br /> 中間層の SharePoint Services (SharePoint の Excel Services や Reporting Services、または PerformancePoint Services)<br /><br /> より深いデータ分析と探索用のブラウザー クライアントまたはリッチ クライアント (Excel)。|  
  
##  <a name="bkmk_Next"></a> 次の手順:ソリューションを構築します。  
 各ソリューションの基本的な違いがわかったら、以下のチュートリアルで、各ソリューションの作成手順を学ぶことができます。 以下のリンクをクリックすると、手順を説明するチュートリアルが表示されます。  
  
-   テーブル モデルを作成するには、「[テーブル モデリング (Adventure Works チュートリアル)](tabular-modeling-adventure-works-tutorial.md)」を使用します。  
  
-   多次元モデルを作成するには、「[多次元モデリング (Adventure Works チュートリアル)](multidimensional-modeling-adventure-works-tutorial.md)」を使用します。  
  
-   データ マイニング モデルを作成するには、「 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)」を使用します。  
  
-   PowerPivot モデルを作成するには、「 [PowerPivot for Excel チュートリアル](https://go.microsoft.com/fwlink/?LinkId=251135)」を使用します。  
  
## <a name="see-also"></a>参照  
 [Analysis Services インスタンス管理](instances/analysis-services-instance-management.md)   
 [新しい Analysis Services と Business Intelligence の新機能](what-s-new-in-analysis-services.md)   
 [新機能については&#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [PowerPivot の新機能新機能](https://go.microsoft.com/fwlink/?LinkId=238141)   
 [SQL Server 2012 用 PowerPivot のヘルプ](https://go.microsoft.com/fwlink/?LinkID=220946)   
 [PowerPivot BI セマンティック モデル接続&#40;.bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [共有データ ソースを作成および管理する (Reporting Services の SharePoint 統合モード)](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  
