---
title: 多次元モデル内のメジャーおよびメジャー グループの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- measure groups [Analysis Services], defining
ms.assetid: 1018bb2e-b89b-489e-aead-450dec5dca3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2883a9092f7b84e8dd18954cec631b90a8bbe0e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076250"
---
# <a name="create-measures-and-measure-groups-in-multidimensional-models"></a>多次元モデル内のメジャーおよびメジャー グループの作成
  *メジャー* は、合計値、度数、最小値、最大値、平均値、または自ら作成したカスタム MDX 式のように、数値のデータ値を集計したものです。 *メジャー グループ* は、1 つ以上のメジャーに対応するコンテナーです。 すべてのメジャーは、メジャーが 1 つしかない場合を含め、1 つのメジャー グループ内に存在します。 キューブには、少なくとも 1 つのメジャーとメジャー グループが必要です。  
  
 このトピックのセクションは次のとおりです。  
  
-   [メジャーを作成するための方法](#bkmk_create)  
  
-   [メジャーのコンポーネント](#bkmk_comps)  
  
-   [ファクトとファクト テーブルでのメジャーとメジャー グループのモデリング](#bkmk_modeling)  
  
-   [メジャー グループの粒度](#bkmk_grain)  
  
##  <a name="bkmk_create"></a> メジャーを作成するための方法  
 メジャーは、キューブの静的な要素になることができ、設計時に作成され、キューブがアクセスされるときは常に存在します。 ただし、多次元式 (MDX) を使用して *計算されるメンバー* としてメジャーを定義し、キューブ内の他のメジャーに基づいてメジャーの計算値を算出することもできます。 計算されるメンバーは、セッションまたはユーザーにスコープすることができます。  
  
 メジャーまたはメジャー グループを作成するには、次の方法のいずれかを使用します。  
  
|||  
|-|-|  
|キューブ ウィザード|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でキューブ ウィザードを実行してキューブを作成します。<br /><br /> ソリューション エクスプローラーで **[キューブ]** を右クリックし、 **[新しいキューブ]** を選択します。 これらの手順については、「[多次元モデリング (Adventure Works チュートリアル)](../multidimensional-modeling-adventure-works-tutorial.md)」を参照してください。<br /><br /> 既存のデータ ウェアハウスのテーブルに基づいてキューブを作成すると、メジャーおよびメジャー グループの定義がキューブの作成プロセスの一部として具体化されます。 ウィザードで、キューブ内のメジャーとメジャー グループのオブジェクトのベースとして使用するファクトとファクト テーブルを選択します。|  
|[新しいメジャー] ダイアログ|キューブが既に [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]に存在していることを前提に、キューブ デザイナーでソリューション エクスプローラー内のキューブ名をダブルクリックして開きます。 [メジャー] ペインで、ソース テーブル、列、集計の型を指定し、最上位のノードを右クリックして新しいメジャー グループまたは新しいメジャーを作成します。 この方法を使用するには、構築済みの関数の固定リストから集計の方法を選択することが必要です。 より一般的に使用されている集計の説明については、「 [Use Aggregate Functions](use-aggregate-functions.md) 」を参照してください。|  
|計算されるメンバー|計算されるメンバーについては、いつどのように作成するかを制御できるため、それにより [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でキューブに柔軟性と分析機能が追加されます。 ユーザー セッションの期間中、または調査の一部としての Management Studio では、一時的にのみメジャーが必要になることがあります。<br /><br /> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、[計算] タブを開いて計算されるメンバーを新規作成します。<br /><br /> メジャーを MDX 式のベースにする場合は、この方法を選択します。 詳細については次のトピックを参照してください。[MDX でのメジャーを構築](mdx/mdx-building-measures.md)、[計算](../multidimensional-models-olap-logical-cube-objects/calculations.md)、[多次元モデルの計算](calculations-in-multidimensional-models.md)と[MDX スクリプティングの基礎&#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md).|  
|MDX または XMLA|計算される新しいメジャーを含めるには、SQL Server Management Studio で、MDX または XMLA を実行してデータベースを変更します。 この方法は、ソリューションをサーバーに配置した後の、データのアドホック テストに役立ちます。 「 [Document and Script an Analysis Services Database](document-and-script-an-analysis-services-database.md)」を参照してください。|  
  
##  <a name="bkmk_comps"></a> メジャーのコンポーネント  
 メジャーは、プロパティを持つオブジェクトです。 メジャーは、名前だけでなく、集計の種類と、ソース列またはデータがあるメジャーの読み込みに使用する式が必要です。 メジャーの定義を変更するには、プロパティを設定します。  
  
|||  
|-|-|  
|**source**|ほとんどのメジャーは、AdventureWorks データ ウェアハウス内の Internet Sales (インターネット売上) や Reseller Sales (販売店売上) テーブルにある Sales Amount 列など、外部データ ウェアハウス内のファクト テーブルの数値列に由来していますが、定義する計算全体に基づいてメジャーを新規作成することもできます。<br /><br /> ディメンション テーブルの属性列は、メジャーの定義に使用できますが、これらのメジャーの集計動作は、通常、準加法または非加法です。 準加法の動作の詳細については、「 [準加法の動作の定義](define-semiadditive-behavior.md)」を参照してください。|  
|**集計 (aggregation)**|既定では、各ディメンションに従ってメジャーが集計されます。 ただし、`AggregateFunction` プロパティを使用するとこの動作を変更できます。 一覧については [Use Aggregate Functions](use-aggregate-functions.md) を参照してください。|  
|**Properties**|プロパティの追加説明については [Configure Measure Properties](configure-measure-properties.md) を参照してください。|  
  
##  <a name="bkmk_modeling"></a> ファクトとファクト テーブルでのメジャーとメジャー グループのモデリング  
 ウィザードを実行する前に、メジャーの定義の背後にあるモデリングの原則を理解するのに役立ちます。  
  
 メジャーとメジャー グループは、外部データ ウェアハウスにあるファクトとファクト テーブルを表す多次元オブジェクトです。 ほとんどの場合、メジャーとメジャー グループはデータ ソース ビュー内のオブジェクトに基づくものになります。このオブジェクトは基になるデータ ウェアハウスから作成されます。  
  
 次の図は、 **FactSalesQuota** ファクト テーブルと、このテーブルに関連する **DimTime** および **DimEmployee**という 2 つのディメンション テーブルを表しています。 Adventure Works のサンプル キューブにおいて、これらのテーブルは Sales Quotas メジャー グループの基礎として、および時間と従業員のディメンションの基礎として使用されます。  
  
 ![2 つのディメンション テーブルを持つ FactSalesQuota テーブル](../media/factsalesquota.gif "FactSalesQuota テーブルと 2 つのディメンション テーブル")  
  
 ファクト テーブルには、属性列とメジャー列という 2 つの種類の列が含まれています。  
  
-   属性列は、ディメンション テーブルに外部キー リレーションシップを作成するために使用されます。これにより、ディメンション テーブルに含まれるデータに基づいてメジャー列の定量化可能なデータが編成されます。 属性列は、ファクト テーブルとそのメジャー グループの粒度を定義するためにも使用されます。  
  
-   メジャー列によって、メジャー グループに含まれるメジャーが定義されます。  
  
 キューブ ウィザードを実行すると、外部キーはフィルターで除外されます。選択する残りの列の一覧に、メジャー列と、外部キーとして識別されないメジャー列および属性列が表示されます。 **FactSalesQuote** の例では、 **CalendarYear** 、 **CalendarQuarter** 、および **SalesAmountQuota**がウィザードにより表示されます。 多次元モデルの場合、実行可能なメジャーは **SalesAmountQuota** メジャー列だけとなります。 日付に基づくその他の列は、各クォータの金額を修飾するために存在します。 キューブ ウィザードのメジャーの一覧から他の列、つまり **CalendarYear** と **CalendarQuarter**を除外する (または後ほど、デザイナーでメジャー グループから削除する) 必要があります。  
  
 この説明から除外すべき点は、ウィザードによって提供されるすべての列がメジャーとして役立つわけではないということです。 どの列をメジャーとして使用するかを決定する際は、データの理解とデータの使用方法を信頼して決定してください。 データを調べるには、データ ソース ビュー内のテーブルを右クリックしてください。メジャーとして使用する列を特定するのに役立ちます。 詳細については、「[Explore Data in a Data Source View (Analysis Services)](explore-data-in-a-data-source-view-analysis-services.md)」 (データ ソース ビューでのデータの検索 (Analysis Services)) を参照してください。  
  
> [!NOTE]  
>  すべてのメジャーがファクト テーブルの列に格納されている値から直接派生するわけではありません。 たとえば、Adventure Works DW サンプル キューブの **Sales Quota** メジャー グループに定義されている **Sales Person Count** メジャーは、 **FactSalesQuota** ファクト テーブルの **EmployeeKey** 列にある一意の値のカウント (または個別のカウント) に実際に基づいています。  
  
##  <a name="bkmk_grain"></a> メジャー グループの粒度  
 メジャー グループには、ファクト テーブルによってサポートされている詳細のレベルを参照する、関連付けられている粒度があります。 粒度は、ディメンションへの外部キーのリレーションシップを介して設定されます。  
  
 たとえば、 **FactSalesQuota** ファクト テーブルには、 **DimEmployee** テーブルとの外部キーのリレーションシップがあり、 **FactSalesQuota** テーブルの各レコードは、1 人の従業員と関係付けられます。こうして、Employee ディメンションから表示されたメジャー グループの粒度は個々の従業員のレベルとなります。  
  
 メジャー グループの粒度は、メジャー グループを表示するためのディメンションの最も低いレベルより詳細なレベルには設定できません。ただし、属性を追加して、粒度を荒くすることは可能です。 たとえば、 **FactSalesQuota** ファクト テーブルでは、 **DimTime**テーブルとのリレーションシップの粒度を確立するために **TimeKey**、 **CalendarYear**、および **CalendarQuarter** の 3 列が使用されています。 結果として、時間ディメンションから見たメジャー グループの粒度は、時間ディメンションの最も低いレベルである "日" ではなく、カレンダー四半期になります。  
  
 キューブ デザイナーの **[ディメンションの使用法]** タブを使用すると、特定のディメンションに関してメジャー グループの粒度を指定できます。 ディメンションのリレーションシップの詳細については、「 [Dimension Relationships](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [多次元モデルのキューブ](cubes-in-multidimensional-models.md)   
 [メジャーおよびメジャー グループ](measures-and-measure-groups.md)  
  
  
